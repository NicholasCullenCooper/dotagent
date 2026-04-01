---
name: persistent-planning
description: Maintain a persistent plan, findings, and progress on the filesystem so work survives context limits, session breaks, and handoffs. Use when executing multi-step work that exceeds a single context window or spans sessions.
---

# Persistent Planning

## What this is for

Your context window is RAM — fast but volatile. The filesystem is disk — persistent and recoverable. This skill offloads planning state to the filesystem so that work continues cleanly across context resets, session breaks, and agent handoffs.

## When to use it

- Work that will take more than ~30 minutes of agent time.
- Multi-step tasks where losing track of progress would mean wasted effort.
- Handoffs between sessions or agents working on the same task.
- Any time you have been asked to pick up where a previous session left off.

## When to skip it

- Quick, self-contained tasks (single file fix, config change, one-shot question).
- Work where the entire plan fits comfortably in a single prompt.

## The three files

Maintain these in the project root or a designated planning directory:

### `task_plan.md` — The plan

The single source of truth for what you are doing and where you are.

```markdown
# Task Plan

## Goal
[One sentence: what success looks like]

## Current Phase
[Which phase you are in right now]

## Phases

### Phase 1: [Name]
- **Status**: complete | in-progress | pending
- **Tasks**:
  - [x] Task description
  - [ ] Task description

### Phase 2: [Name]
...

## Key Questions
[Unresolved questions that may affect the plan]

## Decisions Made
[Choices and their rationale — critical for handoffs]

## Errors Encountered
[What went wrong and how it was resolved]
```

### `findings.md` — Research and discovery

Everything you learn that is not the plan itself: code structure, API behavior, dependency constraints, user requirements clarified mid-task.

```markdown
# Findings

## Requirements
[Clarified or discovered requirements]

## Research
[What you investigated and what you found]

## Technical Decisions
[Implementation choices with rationale]

## Issues
[Problems discovered, whether resolved or not]
```

### `progress.md` — Session log

A running log of what happened, not what should happen. Enables cold-start recovery.

```markdown
# Progress

## Session Log
- [timestamp] Started phase 1
- [timestamp] Completed task X — [brief note]
- [timestamp] Blocked on Y — see Findings

## Test Results
[Latest test output or summary]

## Error Log
[Errors, stack traces, and resolution status]
```

## Workflow

### 1. Create the plan before starting work

Read the task. Write `task_plan.md` with phases and tasks broken into concrete, verifiable steps. Each task should be small enough that you can tell whether it succeeded.

### 2. Read the plan before every major action

Before starting a new task, re-read `task_plan.md`. This is non-negotiable. Context degrades over long sessions — the plan on disk is more reliable than your memory of it.

### 3. Write findings as you discover them

When you learn something — a constraint, a bug, a design decision — write it to `findings.md` immediately. Do not accumulate findings in context hoping to write them later.

**The 2-action rule**: after every 2 investigation or exploration actions (file reads, searches, tool calls), check whether you have findings worth writing down. If yes, write them before continuing.

### 4. Update progress after completing work

After completing a task or hitting a blocker, update `progress.md` and mark the task in `task_plan.md`. This is how the next session (or agent) picks up cleanly.

### 5. Recover from context resets

When starting fresh (new session, context cleared, handoff):

1. Read `task_plan.md` — understand the goal and current phase.
2. Read `progress.md` — understand what already happened.
3. Read `findings.md` — understand what was discovered.
4. Resume from the current phase without repeating completed work.

**Five-question reboot check:**
- What is the goal?
- What phase am I in?
- What was the last completed task?
- Are there unresolved blockers?
- What is the next concrete step?

If you cannot answer all five from the files, the files need updating before proceeding.

## Context budget guidance

Quality degrades as context fills. Rough thresholds:

| Context usage | Quality | Action |
|---|---|---|
| 0–30% | Peak | Normal work |
| 30–50% | Good | Increase filesystem offloading |
| 50–70% | Degrading | Finish current task, write state, consider fresh context |
| 70%+ | Poor | Stop. Write everything to disk. Resume in fresh context. |

When orchestrating subagents or parallel work, give each executor a fresh context loaded only with the plan and the specific task — not the full session history.

## Decision rules

- The plan is a living document. Update it when reality diverges from the original plan — do not silently deviate.
- If a task turns out to be more complex than expected, split it in the plan before continuing.
- If you hit the same error 3 times, stop. Write the error and what you have tried to `findings.md`. Escalate or change approach.
- Findings are append-only during a session. Do not delete findings even if they turn out to be wrong — mark them as superseded.

## Failure modes

- **Not reading the plan before acting.** You will repeat work or contradict earlier decisions.
- **Accumulating context instead of writing to disk.** When the session resets, everything in context is lost.
- **Plans that are too vague to execute.** "Implement the feature" is not a task. "Add the /mount endpoint that accepts a profile name and returns the file list" is.
- **Forgetting to update progress.** The next session will not know where you stopped.
- **Treating the plan as sacred.** Plans change. Update the plan when reality changes, rather than working around a stale plan.

## Output

Three maintained files (`task_plan.md`, `findings.md`, `progress.md`) that enable any agent or session to pick up the work cold. The files themselves are the output — not a summary, not a status message.
