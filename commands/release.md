# /release

## Intent

Prepare a change set or repository for release with explicit validation and rollback awareness.

## Expected inputs

- release target or version, if known
- release scope
- deployment or publication constraints

## Execution steps

1. Confirm what is shipping and what is excluded.
2. Check versioning, changelog, and release notes inputs.
3. Run release-critical validation.
4. Identify migration steps, rollout notes, and rollback needs.
5. Summarize the release state in a way another maintainer can trust.

## Output shape

- release scope
- validation status
- outstanding blockers
- release notes summary
- rollback or mitigation notes