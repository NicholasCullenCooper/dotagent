---
name: repo-onboarding
description: Build a working mental model of an unfamiliar repository quickly and safely. Use when starting work in a new codebase or an unfamiliar subsystem.
---

# Repo Onboarding

## What this is for

Use this skill to get productive in a new repository without guessing how it is organized.

## When to use it

- first session in a repository
- entering a new subsystem
- taking over maintenance of neglected code
- preparing to plan or implement a change in unfamiliar terrain

## Gather first

- root docs and agent-facing files
- top-level folders and build surface
- test and CI entrypoints
- recent change history in the relevant area

## Workflow

1. Read the root guidance first: `AGENTS.md`, README, and adjacent docs.
2. Map the repository shape: app code, libraries, scripts, infra, tests, docs.
3. Identify the execution loop: install, run, test, lint, build, release.
4. Trace one representative feature or request path through the code.
5. Note naming conventions, module boundaries, and obvious hotspots.
6. Capture unknowns before editing anything non-trivial.

## Decision rules and tradeoffs

- Prefer learning the existing shape over imposing a fresh architecture too early.
- Find the nearest working pattern before inventing a new one.
- Read enough code to act confidently, but do not disappear into endless exploration.
- When the repo lacks docs, treat code, tests, and CI as the source of truth.

## Failure modes and common mistakes

- editing before understanding the execution loop
- assuming a familiar stack implies familiar conventions
- over-reading low-value files while missing the active codepath
- confusing generated files or build output for primary source

## Output guidance

Return the repo shape, execution surface, key conventions, likely hotspots, and open questions that still matter.