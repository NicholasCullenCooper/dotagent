---
name: root-cause-analysis
description: Trace a defect or incident back to the first incorrect decision, state, or assumption. Use when a symptom is known but the underlying cause is still unclear.
---

# Root Cause Analysis

## What this is for

Use this skill when the immediate symptom is obvious but the real failure source is not.

## When to use it

- repeated bugs in the same area
- incidents with multiple visible symptoms
- regressions where the triggering change is unclear
- failures caused by configuration, environment, sequencing, or stale assumptions

## Gather first

- the symptom and where it appears
- a timeline of relevant changes or events
- system boundaries involved
- available evidence: logs, traces, failing tests, metrics, reports

## Workflow

1. Write the observed symptom in one sentence.
2. Map the path backward from the symptom to the data, decision, or side effect that produced it.
3. At each step, ask what had to be true for the next failure to happen.
4. Stop at the earliest point where the system departed from intended behavior.
5. Separate contributing factors from the primary root cause.
6. Identify the lowest-cost fix that corrects the cause rather than masking the result.
7. Identify one prevention mechanism: test, validation, monitoring, or process correction.

## Decision rules and tradeoffs

- A root cause should explain the symptom chain, not just correlate with it.
- Multiple contributing factors do not automatically mean multiple root causes.
- Favor fixes that remove a class of failure rather than patch one manifestation.
- If evidence is incomplete, state the best-supported cause and what would confirm it.

## Failure modes and common mistakes

- stopping at the last broken function instead of the first broken assumption
- confusing trigger with cause
- bundling every contributing factor into one muddy explanation
- proposing prevention steps that would not have caught this case

## Output guidance

Return symptom, causal chain, root cause, contributing factors, corrective fix, and prevention step.