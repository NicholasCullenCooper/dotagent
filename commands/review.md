# /review

## Intent

Review a change set for bugs, regressions, missing tests, and operational risk.

## Expected inputs

- diff, branch, PR, or target files
- review focus, if any

## Execution steps

1. Read the changes and surrounding code.
2. Check behavior before style.
3. Look for correctness, security, performance, and maintenance risks.
4. Check whether tests match the changed behavior.
5. Separate must-fix findings from optional improvements.

## Output shape

- findings ordered by severity
- evidence for each finding
- open questions or assumptions
- brief summary only after findings