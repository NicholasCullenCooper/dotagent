# /ship-a-bug-fix

## Intent

Take a failing behavior from report to verified fix without skipping reproduction, diagnosis, or
release risk.

## Use when

- a user reports a bug
- a test exposes a regression
- production behavior diverges from the expected contract

## Sequence

1. Use `skills/reproduction` to make the failure concrete.
2. Use `skills/root-cause-analysis` and `skills/debugging` to isolate the trigger and fault.
3. Run `/implement` for the smallest reliable fix.
4. Use `skills/testing` to convert the failure into regression coverage when practical.
5. Run `/review` on the changed surface and `/release` if the fix affects rollout, compatibility, or rollback.

## Exit criteria

- the original failure is reproducible or its absence is explained with evidence
- root cause is identified rather than guessed
- the fix is validated at the right level
- rollout and rollback concerns are explicit when they matter