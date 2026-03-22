---
name: dependency-upgrades
description: Upgrade dependencies with a bias toward compatibility, verification, and rollback clarity. Use when bumping libraries, SDKs, frameworks, or transitive packages that may affect behavior.
---

# Dependency Upgrades

## What this is for

Use this skill to handle dependency changes as behavior changes, not bookkeeping.

## When to use it

- direct package or library bumps
- framework upgrades
- SDK version changes
- security-driven updates
- lockfile refreshes that pull new transitive behavior

## Gather first

- current and target versions
- changelog, migration notes, and breaking-change docs
- affected import surface and runtime paths
- tests or validation that cover the integration points

## Workflow

1. Identify why the upgrade is happening: security, bug fix, feature need, support window, or alignment.
2. Read the official upgrade notes before editing code.
3. Determine the narrowest set of packages to change.
4. Inspect the codepaths that rely on the upgraded behavior.
5. Apply compatibility fixes deliberately rather than opportunistically rewriting nearby code.
6. Run targeted checks around the touched integration points, then broader checks if needed.
7. Summarize any migration notes, behavior changes, and rollback concerns.

## Decision rules and tradeoffs

- Prefer isolated upgrades over combined toolchain churn unless versions are coupled.
- Security fixes can justify a faster upgrade, but they do not justify skipping verification.
- Lockfile-only changes are still risky if native bindings, code generation, or runtime behavior shifts.
- If the upgrade requires broad API rewrites, split mechanical migration from behavioral cleanup when possible.

## Failure modes and common mistakes

- upgrading without reading release notes
- changing too many packages at once
- trusting compile success as runtime compatibility proof
- mixing upgrade work with unrelated cleanup
- failing to document the new baseline or migration caveats

## Output guidance

Return versions changed, behavior impact, validation performed, migration notes, and rollback concerns.