# /ship-a-feature

## Intent

Take a scoped feature from request to verified change without losing planning, test coverage, or
review discipline.

## Use when

- adding user-visible behavior
- making a cross-file enhancement
- landing non-trivial internal capability work

## Sequence

1. Start with `/plan` to pin down target behavior, constraints, and non-goals.
2. Use `skills/repo-onboarding` if the area is unfamiliar.
3. Run `/implement` with the smallest cohesive change set.
4. Use `skills/testing` to add or update the right validation for the contract that changed.
5. Run `/review` before treating the work as complete.
6. Use `/release` when the change has deployment, migration, compatibility, or communication risk.

## Exit criteria

- the target behavior and non-goals stayed stable through implementation
- the change is validated at the right level
- review has covered regressions and behavioral risk, not just style
- follow-up work is separated from the shipped scope