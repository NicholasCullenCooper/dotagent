---
name: code-review
description: Review code changes for correctness, regressions, maintainability, and missing tests. Use when auditing a diff, pull request, or freshly implemented change.
---

# Code Review

## What this is for

Use this skill to review code with a bias toward finding real risk, not performing style theater.

## When to use it

- before merge
- after an AI-generated implementation
- after a risky refactor or dependency bump
- when a change feels correct but has not been challenged yet

## Gather first

- the diff or changed files
- the behavior the change is supposed to preserve or introduce
- failing tests, incidents, or issue context if this is a bug fix
- nearby code that defines the expected pattern

## Workflow

1. Read the change end to end before judging details.
2. Determine what behavior changed and what behavior is assumed unchanged.
3. Inspect the surrounding code, not just the diff, to verify those assumptions.
4. Look for high-value failure classes:
   - incorrect logic or edge cases
   - missing validation or error handling
   - broken invariants across call boundaries
   - performance regressions on hot paths
   - missing or misleading tests
5. Check whether the change aligns with local patterns where those patterns are deliberate.
6. Classify feedback as must-fix, should-fix, or optional.

## Decision rules and tradeoffs

- Prefer correctness over local neatness.
- Flag missing tests when behavior changed or risk increased.
- Do not require new abstractions unless duplication or complexity justifies them.
- A suspicious pattern is not a finding until you can explain the failure mode.

## Failure modes and common mistakes

- reviewing style while missing behavior regressions
- trusting the diff without reading the dependent codepath
- treating every inconsistency as a bug
- giving vague advice without a concrete reason
- failing to distinguish a blocker from a preference

## Output guidance

Return findings first, ordered by severity. Include evidence and likely impact. Keep summary short.