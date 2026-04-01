---
name: parallel-agents
description: "Experimental: Orchestrate multiple agents working in parallel using git worktrees and task partitioning. Use when the work can be decomposed into independent streams that benefit from concurrent execution."
---

# Parallel Agents

> **Status**: Experimental. Mount with `--include-ignored` to try.

## What this is for

Some work decomposes into independent streams that can run concurrently — different features, different files, different test suites. This skill provides patterns for orchestrating parallel agent execution using git worktrees for isolation and structured task partitioning for coordination.

## When to use it

- A plan has tasks marked `(P)` for parallelizable.
- Multiple independent changes need to land in the same timeframe.
- Code review can be split by concern (security, performance, correctness) and run concurrently.
- A large investigation benefits from exploring multiple hypotheses simultaneously.

## When to skip it

- Tasks are sequential — each depends on the output of the previous one.
- The work is small enough that parallelism adds overhead without saving time.
- You are in a single-agent environment that does not support subagent spawning.

## Gather first

- A plan with clearly identified parallel vs. sequential tasks.
- Understanding of which files each stream will touch (to avoid merge conflicts).
- The project's branching conventions.

## Isolation via worktrees

Each parallel agent gets its own git worktree — an isolated working copy with its own branch:

```bash
# Create worktrees for parallel streams
git worktree add ../project-stream-a -b stream-a
git worktree add ../project-stream-b -b stream-b
```

Worktrees share the same git history but have independent working directories. Agents cannot step on each other's files.

### Rules for worktree-based parallelism

- **One worktree per agent.** Never share a worktree between concurrent agents.
- **Name branches descriptively.** `feat/add-mount-endpoint` not `stream-1`.
- **Merge back to the base branch** when the stream completes, not before.
- **Clean up worktrees** after merging: `git worktree remove ../project-stream-a`.

## Task partitioning

### Good decomposition

Split by:
- **Feature boundary** — each agent implements a different feature end-to-end.
- **Layer boundary** — one agent handles the API, another handles the UI (only when interfaces are pre-agreed).
- **Review concern** — security review, performance review, correctness review run in parallel.
- **Investigation hypothesis** — each agent explores a different theory about a bug.

### Bad decomposition

Do not split:
- **Tightly coupled tasks** — if agent A's output changes agent B's input, they are sequential.
- **Shared-state modifications** — two agents editing the same file will create merge conflicts.
- **Tasks with unclear interfaces** — if the agents need to coordinate on contracts mid-execution, run them sequentially.

## Orchestrator pattern

The orchestrator (main agent or human) is responsible for:

1. **Partition tasks** — assign work to streams based on dependencies and file ownership.
2. **Define interfaces** — if streams need to connect (e.g., API endpoint + client), specify the contract before spawning.
3. **Spawn agents** — one per worktree, each with:
   - The plan (or relevant subset).
   - The specific tasks assigned to this stream.
   - Any interface contracts to implement against.
   - Instructions to commit incrementally and not deviate from scope.
4. **Collect results** — when all streams complete, review each branch.
5. **Merge and integrate** — merge branches, resolve conflicts, run integration tests.

### Orchestrator budget rule

The orchestrator should use at most 15% of total context for coordination. If you are spending more than that on orchestration overhead, the decomposition is too fine-grained.

## Parallel code review

A common and practical use of parallel agents:

| Reviewer | Focus | Trigger |
|---|---|---|
| Correctness | Logic errors, edge cases, missing validation | Always |
| Testing | Coverage gaps, weak assertions, flaky patterns | Always |
| Security | Auth, injection, data exposure, permissions | When auth/user-input code changed |
| Performance | N+1 queries, missing indexes, unnecessary computation | When data access patterns changed |
| Architecture | Coupling, abstraction level, component boundaries | When structure changed |

Each reviewer operates independently on the same diff. An orchestrator merges findings, deduplicates, and prioritizes.

### Confidence gating

When merging parallel review findings:

- Suppress findings below 0.6 confidence (except critical/P0 findings at 0.5+).
- Boost confidence by +0.1 when multiple independent reviewers flag the same issue.
- Separate pre-existing issues from new issues introduced by the change.

## Execution patterns

### Wave-based execution

Group tasks by dependency level. Execute each wave in parallel, then synchronize before the next wave.

```
Wave 1 (parallel): [Task A] [Task B] [Task C]  ← no dependencies
        ↓ sync
Wave 2 (parallel): [Task D] [Task E]            ← depends on wave 1
        ↓ sync
Wave 3 (sequential): [Task F]                    ← depends on D and E
```

### Fresh context per executor

Each spawned agent gets a clean context loaded with:
- The plan (or relevant subset).
- Its assigned tasks only.
- Key findings from previous waves (if applicable).
- Nothing else.

This prevents context degradation. An orchestrator with 70% context utilization can still spawn executors at 0%.

## Decision rules

- Parallelism pays off at 3+ independent tasks. Below that, orchestration overhead usually exceeds the time saved.
- If two tasks touch the same file, make them sequential or merge them into one task.
- Pre-agree on interfaces before spawning parallel streams. Discovering interface mismatches during merge is expensive.
- Fail fast — if a parallel stream hits a blocker, surface it to the orchestrator immediately rather than working around it.

## Failure modes

- **Over-decomposition.** Too many parallel streams create merge hell and coordination overhead. Start with 2-3 streams.
- **Shared file conflicts.** Two agents editing the same file. Always check file ownership before partitioning.
- **Missing interface contracts.** Agents build to different assumptions. Define contracts explicitly before spawning.
- **Silent deviation.** An agent deviates from the plan but does not report it. Require incremental commits and scope-check at merge.
- **Orchestrator bloat.** The orchestrator accumulates context from all streams and degrades. Keep the orchestrator thin — it coordinates, it does not do the work.

## Output

Merged branches with integrated code, passing tests, and resolved conflicts. For parallel reviews: a deduplicated, prioritized list of findings.
