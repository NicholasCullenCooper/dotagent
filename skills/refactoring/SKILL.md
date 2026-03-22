---
name: refactoring
description: Improve structure and maintainability without changing intended behavior. Use when code is hard to understand, duplicate, or brittle, but the external behavior should stay stable.
---

# Refactoring

## What this is for

Use this skill to make code easier to change without turning a cleanup pass into an uncontrolled rewrite.

## When to use it

- duplication is causing bugs or drag
- a module is hard to reason about
- naming and structure obscure behavior
- a new feature keeps colliding with weak boundaries

## Gather first

- the code under change
- the pain points driving the refactor
- the behaviors and interfaces that must remain stable
- the existing tests and validation surface

## Workflow

1. Define the specific problem the refactor is meant to solve.
2. Mark the invariants: public API, side effects, performance envelope, compatibility constraints.
3. Break the refactor into small, behavior-preserving steps.
4. Prefer extraction, renaming, simplification, and dead code removal before architectural surgery.
5. Run targeted checks after each material step when possible.
6. Stop when the identified problem is solved; do not keep polishing for sport.

## Decision rules and tradeoffs

- Prefer local improvements over new abstraction layers.
- Duplicate code is acceptable when the shared abstraction would be harder to change.
- If a refactor changes behavior, treat that part as a feature or bug fix and validate it separately.
- Preserve naming and structure patterns that help the existing team, even if you would choose differently from scratch.

## Failure modes and common mistakes

- mixing cleanup, feature work, and behavior changes in one pass
- extracting abstractions too early
- renaming aggressively without improving clarity
- touching every nearby file because the code is now open

## Output guidance

Return the refactor goal, invariants preserved, structural changes made, validation run, and intentionally deferred cleanup.