---
name: performance-investigation
description: Investigate slow paths, resource spikes, or scaling regressions with measurement and targeted fixes. Use when performance is a problem but the bottleneck is not yet verified.
---

# Performance Investigation

## What this is for

Use this skill to find and improve meaningful bottlenecks without cargo-cult optimization.

## When to use it

- user-visible slowness
- CPU, memory, or I/O spikes
- regressions after a change
- query latency or throughput problems
- hot paths that are known but not yet measured well

## Gather first

- the symptom: latency, throughput, memory growth, startup time, render cost, query duration
- a baseline or comparison point
- reproduction conditions and input sizes
- available profiling, tracing, or metrics tools

## Workflow

1. Define the metric that matters.
2. Reproduce the performance issue under known conditions.
3. Measure before changing anything.
4. Narrow the bottleneck to a concrete path, callsite, query, loop, or allocation pattern.
5. Test candidate fixes against the measured bottleneck.
6. Re-measure after the change under comparable conditions.
7. Record the tradeoff introduced by the fix, if any.

## Decision rules and tradeoffs

- Do not optimize unmeasured code because it looks slow.
- Prefer changes that improve the dominant bottleneck rather than shaving negligible overhead.
- A readability hit needs a real performance win to justify it.
- If the main constraint is external latency or infrastructure, code tweaks may not be the right lever.

## Failure modes and common mistakes

- changing code before establishing a baseline
- comparing measurements taken under different conditions
- optimizing incidental work while ignoring the dominant bottleneck
- keeping a complex optimization whose benefit cannot be shown

## Output guidance

Return the metric, baseline, bottleneck, fix, new measurement, and any readability or maintenance tradeoffs.