---
name: debugging
description: Diagnose and fix failures using evidence, reproduction, and targeted verification. Use when tests fail, runtime behavior is wrong, or an issue is not yet explained.
---

# Debugging

## What this is for

Use this skill to move from symptom to verified fix without guessing.

## When to use it

- failing tests or builds
- runtime exceptions
- regressions after a recent change
- flaky or intermittent behavior
- incidents reproduced from logs or reports

## Gather first

- exact error output or observed bad behavior
- reproduction steps and whether they still work
- recent changes in the affected area
- logs, traces, or metrics that narrow the failure path

## Workflow

1. State the failure in precise terms.
2. Confirm whether it reproduces now. If not, say so explicitly.
3. Establish the narrowest failing path you can observe.
4. Identify the first wrong state, wrong branch, or wrong assumption.
5. Form hypotheses and test them one by one.
6. Fix the smallest point that corrects the underlying defect.
7. Re-run a targeted validation step.
8. Note what guard, test, or instrumentation would have caught this earlier.

## Decision rules and tradeoffs

- Prefer direct evidence over intuition.
- Logging is useful when it narrows a hypothesis, not when it sprays noise.
- Roll back a recent change only when the evidence points there or the blast radius demands it.
- A fix is incomplete if the original failure mode has not been rechecked.

## Failure modes and common mistakes

- fixing the visible crash but leaving corrupted state untouched
- skipping reproduction and debugging blind
- changing multiple variables at once and losing causality
- relying on one stack trace without tracing data flow
- declaring success without a focused recheck

## Output guidance

Return the failure, root cause, evidence, fix, and verification result. If the issue is not fully resolved, say what still blocks certainty.