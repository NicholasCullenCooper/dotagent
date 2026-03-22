---
name: reproduction
description: Establish a reliable way to reproduce a bug, regression, or suspicious behavior. Use when a problem report exists but cannot yet be verified on demand.
---

# Reproduction

## What this is for

Use this skill to turn a vague issue report into a repeatable failure that can be debugged and verified.

## When to use it

- a bug report is incomplete
- an issue happens only in some environments
- a flaky problem needs a tighter trigger
- a fix cannot be trusted because the original problem is not reproducible

## Gather first

- observed behavior versus expected behavior
- environment details: branch, version, config, inputs, timing
- issue reports, logs, screenshots, or failing requests
- any clues about frequency or preconditions

## Workflow

1. Restate the issue in a way that can be falsified.
2. Capture the exact environment and starting state.
3. Enumerate candidate triggers: inputs, sequence, data shape, timing, permissions, config.
4. Build the smallest repeatable path to the failure.
5. Reduce noise by stripping unrelated steps.
6. Record the reproduction as a short checklist, script, or failing test where practical.
7. Re-run it until the success rate is understood: deterministic, intermittent, or not yet reliable.

## Decision rules and tradeoffs

- Prefer the shortest path that still triggers the issue.
- A flaky reproduction is still useful if you can state the hit rate and conditions.
- If a failing test is feasible, it is usually the best long-term reproduction artifact.
- Do not force a synthetic reproduction that no longer resembles the real issue.

## Failure modes and common mistakes

- skipping environment details and chasing the wrong branch or config
- bundling too many steps and obscuring the real trigger
- confusing correlation with a reliable trigger
- claiming a fix without reusing the same reproduction path

## Output guidance

Return environment, exact steps, expected result, actual result, and reliability of the reproduction.