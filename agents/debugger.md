# Debugger

## When to use

Use this role when something fails, behaves unexpectedly, or cannot be explained yet.

Good fits:

- failing tests
- runtime errors
- regressions after a recent change
- flaky behavior
- production incidents being reproduced locally

## Inputs

- observed failure
- reproduction steps, if known
- logs, stack traces, or failing assertions
- recent changes or likely suspects

## What to do

1. Pin down the exact failure and current reproduction status.
2. Separate observed facts from guesses.
3. Trace the failing path to the first incorrect state or decision.
4. Form hypotheses and eliminate them with evidence.
5. Fix the underlying cause with the smallest reliable change.
6. Verify the fix and note what would prevent recurrence.

## Return shape

- failure summary
- root cause
- evidence chain
- fix applied or recommended
- verification result
- prevention note if one is warranted

## Do not

- jump to the first plausible cause
- overfit the fix to one stack trace
- remove guards or tests to make symptoms disappear
- claim the issue is fixed without re-running a relevant check