# AGENTS.md — Universal Agent Instructions

Guidance for AI coding agents (Claude Code, GitHub Copilot, Codex, OpenCode, Cursor, etc.).

This file contains cross-project standards. Project-specific context (build commands,
architecture, conventions) belongs in a separate file committed to each repository
(e.g., `CLAUDE.md`, `PROJECT.md`, or the project-specific section of a local `AGENTS.md`).

---

## Working Style

- **Discuss before implementing** non-trivial features. Present decision points and options.
- **No commits without explicit user approval.**
- **Flag uncertainty** — stop and ask rather than guessing.
- **Fetch external library docs** before implementing. Don't rely on training data for APIs.
- After completing tasks, follow the "After Completing Tasks" checklist below.

### Before Writing Code

1. **List decision points** — Before implementing non-trivial features, identify choices and
   present them: "Here are the decisions I'd make. Want to discuss any of these?"
   Include: data structures, naming, patterns, dependencies, tradeoffs.

2. **Present options, don't just pick** — When multiple valid approaches exist, explain each
   with pros/cons rather than choosing one silently.

3. **Ask clarifying questions** — If requirements are ambiguous, ask rather than assume.
   Better to pause than to build the wrong thing.

4. **Work in small chunks** — For larger features, break into phases:
   - Phase 1: Discuss approach → get approval
   - Phase 2: Implement core → review
   - Phase 3: Iterate

### During Implementation

5. **No commits without explicit approval** — Wait for "go ahead", "commit this", or similar
   before running `git commit`.

6. **Flag uncertainty** — If unsure about something mid-implementation, stop and ask rather
   than guessing.

7. **Explain non-obvious choices** — When you make a decision, briefly note why.

### After Completing Tasks

8. **Update task tracking** — Mark completed tasks, add any new follow-up tasks discovered.

9. **Close issues** — If the completed task has a corresponding issue, close it:

   ```bash
   gh issue close <number>
   ```

10. **Update feature tracking docs** — Follow the project's "After Completing Tasks" checklist.

11. **Update ADRs when behavior changes** — If implementation changes documented behavior,
    update the relevant ADR.

12. **Keep docs in sync** — Before finishing any task that touched documentation, verify
    related docs are updated.

---

## When to Write Tests

New code needs tests. Passing existing tests only proves nothing regressed — it says nothing
about whether the new code works.

**Always test:**

- Pure functions and conversion layers (parsers, mappers, sorting, validation)
- State stores (state transitions, action side effects)
- DB query functions (CRUD, edge cases, constraints)
- Algorithms with branching logic (dedup, scoring, inference, routing)
- Bug fixes — write a failing test first, then fix

**Test if non-trivial:**

- Hooks with logic beyond simple state reads (debounce, subscriptions, derived state)
- Integration points (IPC contracts, adapter layers)
- Complex UI components with conditional rendering or user interactions

**Skip testing:**

- Thin wrapper components that only compose other components with props
- One-liner re-exports or type definitions
- Purely declarative config (static arrays, route definitions)

**Rule of thumb:** If a module has `if/else`, `switch`, `map/filter/reduce`, or async
orchestration, it should have tests. If it's just plumbing, it doesn't need its own test file.

**For AI agents:** When you create a new module that falls in the "always test" category, write
tests in the same PR. Don't defer to a separate "add tests" step. When modifying an existing
tested module, update or add tests to cover the new behavior. Include test counts in commit
messages when tests are added or updated.

---

## General Code Principles

- Prefer editing existing files over creating new ones
- No secrets, API keys, or credentials in committed files
- Prefer the project's established patterns over importing new libraries
- When in doubt about a convention, look at how existing code does it

---

## Git Workflow

### Branching

All work happens on feature branches, never directly on `main`. Feature branches use
the `feat/` prefix scoped to a version phase:

```
feat/v0.4a-fix-broken-features
feat/v0.4b-quick-capture
feat/v0.5a-activity-instrumentation
```

### Merging to Main

1. **Ensure checks pass** (lint, typecheck, tests)
2. **Create a pull request**
3. **Stop and tell the user** — give them the PR URL and wait for them to merge it
4. When the user confirms the PR is merged:
   - `git checkout main && git pull origin main`
   - `git push origin --delete feat/branch-name`
   - `git branch -d feat/branch-name`

Never merge locally — always through a PR so the merge is tracked. Never merge the PR yourself —
the user reviews and merges.

### Starting a New Phase

1. `git checkout main && git pull`
2. `git checkout -b feat/v0.Xn-description`
3. `git push -u origin feat/v0.Xn-description` (on first commit)

---

## Feature Tracking

```
docs/plan/roadmap.md     → all versions, high-level feature lists (source of truth)
docs/plan/v0.X-*.md      → detailed planning per version
TODO.md                  → current version execution (flat checkbox list)
TODO.md ## Deferred      → parking lot for deferred items across all versions
GitHub Issues            → agent backlog only (version-free, independent, grab-and-go)
```

- **Checkboxes:** `[ ]` not started, `[x]` done, `[d]` deferred, `[b]` backlogged (linked Issue)
- **`[b]` marker** — independent work an agent can tackle anytime. Always has a GitHub Issue.
- **`[d]` marker** — deferred to a later version. No issue needed.
- GitHub Issues are only for agent-safe backlog items, not a mirror of the roadmap.

### GitHub Labels

| Label           | Purpose                                     |
| --------------- | ------------------------------------------- |
| `agent-backlog` | In the agent queue, not yet picked up       |
| `agent-safe`    | Can be implemented without design decisions |
| `critical`      | Blocks other work                           |
| `nice-to-have`  | Quality-of-life improvement                 |

### Creating Backlog Issues

```bash
gh issue create --title "Short description" --label "agent-backlog,agent-safe" --body "..."
```

Mark as `[b]` in TODO.md with a link to the issue.

### Roadmap Section Structure

```markdown
## v0.X — Title

Overview paragraph.

### Features (competitive reference)

### Features (unique)

### Exit Criteria

### Notes
```

### Version Transitions

When a version's exit criteria are all met:

**1. Close the outgoing version**

- **roadmap.md**: Add `✅` to the version heading, mark all feature rows 🟢, check all
  exit criteria `[x]`, update version history table
- **GitHub Issues**: Close any issues completed during the version
- **TODO.md**: Add `(archived)` marker to the version heading, leave all checkboxes as-is

**2. Update the Deferred section**

- Move any `[d]` items from the closing version into `## Deferred` in TODO.md with
  `(from v0.Y)` annotation
- `[b]` items stay where they are — tracked via GitHub Issues

**3. Open the incoming version**

- **roadmap.md**: Add `Current:` prefix to the new version heading
- **TODO.md**: Create new `## v0.X` section at the top
- Review `## Deferred` — promote items that fit the new version

**4. Commit and push**

- Single commit: `docs: archive v0.X, open v0.Y — version transition`
- Push directly to `main` (transition is docs-only, no PR needed)

---

## Planning Lessons

### Document Behaviors, Not Just Data Structures

Plans should specify:

1. **Data model** — What fields exist on types
2. **UI elements** — What buttons/controls exist
3. **Behaviors** — What happens when users interact

When planning features with semantic relationships, explicitly document:

- What happens on edge creation (side effects on source/target nodes)
- What triggers AI assistance
- How action buttons differ from manual interactions

---

## What NOT to Do

- Do not commit secrets, API keys, or .env files
- Do not make large refactors while implementing a feature — separate concerns into separate PRs
- Do not add new dependencies without justification
- Do not silently make architectural decisions — surface them for discussion
- Do not push to `main` directly
