# /refactor

## Intent

Improve structure, clarity, or maintainability without changing intended behavior.

## Expected inputs

- scope of refactor
- pain points being addressed
- behavior that must remain stable

## Execution steps

1. Confirm why the refactor is needed.
2. Define the invariants that cannot change.
3. Make changes in small, reviewable steps.
4. Avoid mixing unrelated cleanup into the same pass.
5. Verify behavior with tests or targeted checks.

## Output shape

- refactor goal
- invariants preserved
- structural changes made
- verification result
- follow-up debt intentionally left out