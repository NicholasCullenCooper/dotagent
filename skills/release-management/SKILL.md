---
name: release-management
description: Prepare and validate a release with explicit scope, risk review, and rollback awareness. Use when tagging, deploying, or handing off a release candidate.
---

# Release Management

## What this is for

Use this skill to turn a pile of changes into a releasable unit that another maintainer can assess quickly.

## When to use it

- preparing a versioned release
- assembling release notes
- validating a release candidate
- reviewing rollout and rollback readiness

## Gather first

- release scope and version target
- included changes and known exclusions
- required checks: tests, builds, migrations, packaging, deployment prerequisites
- rollout constraints and rollback options

## Workflow

1. Confirm what is actually in scope.
2. Verify that versioning and changelog inputs are consistent.
3. Run release-critical validation rather than every possible check blindly.
4. Review migration steps, compatibility risks, and operational dependencies.
5. Draft release notes that describe user-visible changes and important caveats.
6. State rollback or mitigation steps for the highest-risk changes.

## Decision rules and tradeoffs

- Shipping fewer clear changes is safer than shipping an unclear bundle.
- If release-critical checks are failing, do not hide behind a long backlog of non-blocking issues.
- Release notes should reflect behavior and operator impact, not commit-message trivia.
- A rollback plan matters most when schema, data, deployment order, or external integrations changed.

## Failure modes and common mistakes

- unclear scope
- release notes that omit breaking or operationally relevant behavior
- treating green unit tests as sufficient for packaging or deployment changes
- no rollback note for risky migrations or one-way changes

## Output guidance

Return release scope, validation status, blockers, operator notes, and rollback posture.