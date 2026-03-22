# /implement

## Intent

Take a scoped task from request to verified change.

## Expected inputs

- target behavior
- constraints or non-goals
- relevant files, issue links, or failing checks

## Execution steps

1. Inspect the affected codepath.
2. Confirm the smallest effective change.
3. Implement with local conventions intact.
4. Update tests or docs when the behavior changes.
5. Run the best available validation.
6. Report exactly what changed and what remains uncertain.

## Output shape

- summary of implemented change
- files touched
- validation performed
- residual risks or follow-ups