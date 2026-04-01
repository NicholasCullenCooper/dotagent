---
name: spec-driven-dev
description: Drive implementation from structured specifications — requirements, design, and tasks — so the code follows the spec rather than the other way around. Use when building features that need alignment between intent and implementation.
---

# Spec-Driven Development

## What this is for

Specifications are the source of truth. Code implements the spec; the spec does not document the code. This skill provides a lightweight workflow for producing specifications that are precise enough to implement against and flexible enough to evolve during development.

## When to use it

- Building a new feature where the requirements are not yet written down.
- Enhancing existing behavior where the intended change needs to be agreed before coding.
- Working in a team where multiple people (or agents) need to understand what to build.
- Brownfield work where you need to understand the current state before proposing changes.

## When to skip it

- The change is mechanical and fully described by a single sentence.
- You already have an approved spec or plan from a prior brainstorming session.
- You are fixing a bug with a clear reproduction — use debugging and reproduction skills instead.

## Gather first

- Output from brainstorming (requirements doc, design notes) if available.
- Existing specs, PRDs, or design documents for the area.
- The current codebase state — especially for brownfield work.
- Project conventions for where specs live (e.g., `docs/specs/`, `openspec/changes/`, `.kiro/specs/`).

## Artifacts

Spec-driven dev produces up to four artifacts. Not every feature needs all four — match ceremony to scope.

### Requirements (`requirements.md`)

What the system must do. Each requirement is:

- **Numbered** (R1, R2, ...) for stable cross-referencing.
- **Testable** — you can write a pass/fail check for it.
- **Behavior-focused** — describes what happens, not how it is implemented.

Structure each requirement with acceptance criteria. The EARS format works well for precision:

| Pattern | Template | Use when |
|---|---|---|
| Event-driven | WHEN [event] the system SHALL [response] | Triggered behavior |
| State-driven | WHILE [state] the system SHALL [behavior] | Ongoing conditions |
| Unwanted behavior | IF [condition] THEN the system SHALL [response] | Error handling, edge cases |
| Optional | WHERE [feature enabled] the system SHALL [behavior] | Configurable features |
| Ubiquitous | The system SHALL [behavior] | Always-on constraints |

You do not need to use EARS for every requirement. Use it when precision matters; use plain language when the meaning is already clear.

### Design (`design.md`)

How the system will satisfy the requirements. Includes:

- **Context** — what exists today and what is changing.
- **Goals and non-goals** — what this design is and is not trying to achieve.
- **Decisions** — choices made, with rationale. Include rejected alternatives and why.
- **Risks and trade-offs** — what could go wrong, what you are accepting.
- **Open questions** — honest gaps, with owners if applicable.

Diagrams are welcome when they clarify (flows, component boundaries, data models). Do not add diagrams for decoration.

### Tasks (`tasks.md`)

The implementation plan derived from the design. Each task is:

- **Small** — completable in one focused session.
- **Ordered** — respecting dependencies. Mark parallelizable tasks with `(P)`.
- **Traceable** — references the requirements it satisfies (e.g., `_Requirements: R1, R3_`).

```markdown
## 1. Setup
- [ ] 1.1 Create module structure — _Requirements: R1_
- [ ] 1.2 (P) Add configuration schema — _Requirements: R2_

## 2. Core implementation
- [ ] 2.1 Implement handler — _Requirements: R1, R3_
- [ ] 2.2 Add validation — _Requirements: R4_
```

### Proposal (`proposal.md`) — optional

For larger changes, a short (1-2 page) document explaining **why** this work should happen before investing in full specs. Covers: the problem/opportunity, what changes, expected impact. Useful when the work needs approval before detailed specification.

## Workflow

### For greenfield work

1. **(Optional) Write a proposal** if the work needs buy-in first.
2. **Write requirements** — testable, numbered, behavior-focused.
3. **Write design** — decisions, trade-offs, component boundaries.
4. **Generate tasks** — ordered, parallelism-marked, requirements-traced.
5. **Implement against the tasks** — check off as you go.
6. **Validate** — verify each requirement's acceptance criteria is met.

### For brownfield work

1. **Analyze the current state** — read the code, understand existing behavior and patterns.
2. **Identify the gap** — what needs to change, what can be reused, what conflicts.
3. **Assess approach options** — Extend existing code? Build new? Hybrid? Estimate effort (S/M/L/XL) and risk (High/Medium/Low) for each.
4. **Write delta requirements** — only the changes. Use `ADDED`, `MODIFIED`, `REMOVED` sections rather than rewriting the full spec.
5. **Proceed with design → tasks → implement** as above.

## Evolving specs

Specs are living documents, not contracts carved in stone.

- Update specs when reality diverges — do not silently deviate.
- Use delta format (`ADDED`, `MODIFIED`, `REMOVED`) for evolving requirements.
- Archive completed specs rather than deleting them. A dated archive folder (`archive/YYYY-MM-DD-feature-name/`) preserves history without cluttering active work.
- When a design decision changes during implementation, update the design doc with the new decision and rationale.

## Decision rules

- Requirements describe **what**, design describes **how**, tasks describe **when**. Keep them separated.
- If you find yourself writing implementation details in requirements, move them to design.
- If a requirement is not testable, it is not a requirement — rewrite it or demote it to a goal.
- Prefer fewer, sharper requirements over exhaustive lists. Five precise requirements beat twenty vague ones.
- The spec does not need to be perfect before you start implementing. It needs to be good enough that you know what "done" means for the first batch of tasks.

## Failure modes

- **Specs that describe the code instead of the behavior.** "The function takes a string parameter" is implementation. "The system accepts a profile name and returns matching files" is a requirement.
- **Waterfall ceremony on a two-hour task.** Match artifact depth to scope. A small feature might only need requirements and tasks — no design doc, no proposal.
- **Specs that never get updated.** A stale spec is worse than no spec. If the code and spec disagree, one of them is wrong — figure out which.
- **Skipping brownfield analysis.** Jumping to requirements without understanding the current state leads to specs that conflict with existing behavior.
- **Requirements without acceptance criteria.** "The system should be fast" is not verifiable. "Response time under 200ms at p95" is.

## Output

One or more spec artifacts (requirements, design, tasks, optionally proposal) in the project's convention location. The artifacts should be specific enough that another agent or developer could implement against them without additional context.
