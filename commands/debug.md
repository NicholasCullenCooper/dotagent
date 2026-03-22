# /debug

## Intent

Diagnose and resolve a concrete failure with evidence.

## Expected inputs

- failure description
- reproduction steps, if known
- logs, stack traces, failing tests, or recent changes

## Execution steps

1. Confirm the failure and reproduction status.
2. Isolate the failing path.
3. Form and test hypotheses against evidence.
4. Fix the root cause, not the visible symptom.
5. Verify the outcome with a targeted check.
6. Record any prevention step worth keeping.

## Output shape

- root cause summary
- evidence chain
- fix or recommended fix
- verification result
- remaining uncertainty