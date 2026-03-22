---
name: testing
description: Choose and add the right validation for a change. Use when implementing features, fixing bugs, or assessing whether current coverage is enough.
---

# Testing

## What this is for

Use this skill to decide what to test, at what level, and with what scope.

## When to use it

- adding or changing behavior
- fixing a bug
- reviewing whether coverage matches risk
- converting a manual reproduction into an automated check

## Gather first

- what behavior changed or might regress
- where the logic lives
- existing test types in the repository
- runtime constraints: slow integration environment, missing fixtures, external dependencies

## Workflow

1. Identify the contract that matters: input/output, state transition, side effect, or integration boundary.
2. Pick the narrowest test level that can catch the failure reliably.
3. Add or update tests around changed behavior, not just happy paths.
4. Cover the critical branch, edge condition, or regression trigger.
5. Run the most targeted useful subset first, then broader checks if warranted.

## Decision rules and tradeoffs

- Prefer fast, local tests for pure logic.
- Use integration tests when the behavior depends on boundaries between modules or services.
- Use end-to-end coverage sparingly for workflows that cannot be trusted at lower levels.
- A bug fix is stronger when the original failure becomes a test.
- Do not add broad snapshot or golden tests when a tighter assertion would do.

## Failure modes and common mistakes

- writing tests that mirror the implementation instead of the contract
- adding only happy-path tests for risky logic
- using slow end-to-end tests to cover unit-level behavior
- updating snapshots without checking whether the behavior should have changed

## Output guidance

Return what was tested, why that level was chosen, what cases were covered, and what remains untested by design.