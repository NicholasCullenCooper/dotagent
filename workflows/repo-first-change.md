# /repo-first-change

## Intent

Get productive in an unfamiliar repository and land one safe change without over-scaffolding.

## Use when

- starting in a new repository
- picking up an unfamiliar subsystem
- inheriting a codepath from another team

## Sequence

1. Start with `skills/repo-onboarding` to map the execution loop and likely hotspots.
2. Use `/plan` once the affected path and constraints are clear.
3. Run `/implement` for the smallest useful change.
4. Use `skills/testing` to choose the narrowest validation that can catch regressions.
5. Run `/review` before calling the work complete.

## Exit criteria

- the repository shape and execution loop are understood well enough to explain
- the first change follows local conventions rather than imposing new ones
- validation matches the risk of the change
- open questions are explicit instead of silently ignored