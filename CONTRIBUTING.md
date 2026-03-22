# Contributing

This repository is a reusable workflow registry, not a general prompt dump.

Contributions should improve utility, clarity, or portability across repositories.

## Before adding a file

Ask these questions first:

1. Is this reusable across many repositories?
2. Is this better as an agent, a command, a workflow, or a skill?
3. Does an existing file already cover the need well enough?
4. Is the value based on real usage, not hypothetical completeness?
5. Would this still make sense without a specific stack, company, or project?

If the answer to any of those is no, it probably does not belong here yet.

## What belongs where

### `agents/`

Add a file here when you need a focused role definition.

Good fit:

- a read-only explorer
- a debugger with a specific return shape
- a reviewer with explicit priorities

Bad fit:

- another name for an existing role
- a workflow that should be a command
- broad domain knowledge that belongs in a skill

### `commands/`

Add a file here when users need a repeatable workflow entrypoint.

Good fit:

- plan
- implement
- review
- refactor
- release

Bad fit:

- long reference material
- domain knowledge
- commands that only make sense in one repository

Commands should stay thin. They should start a workflow, not restate an entire skill.

### `workflows/`

Add a file here when you need an outcome-level route through several existing registry assets.

Good fit:

- ship a bug fix from repro to review
- land a feature with planning, testing, and release checks
- make a first safe change in an unfamiliar repo

Bad fit:

- a workflow that just renames an existing command
- long-form domain guidance that belongs in a skill
- a one-off sequence that has not shown recurring value

### `skills/`

Add a skill when the task needs a reusable method, decision framework, or domain playbook.

Every skill should explain:

- what it is for
- when to use it
- what to gather first
- the step-by-step workflow
- the key decision rules
- the common failure modes

## Skill anatomy

Use this shape unless there is a strong reason not to:

```text
skills/<skill-name>/SKILL.md
```

Use lowercase hyphenated names.

Keep `SKILL.md` focused. When a skill becomes too large, split out supporting files for:

- examples
- templates
- scripts
- detailed reference material

Do that only when the supporting files materially improve usability.

## Maturity

Use this maturity model when deciding whether something belongs in the repo.

- `core`: stable, broadly useful, and worth mounting by default
- `candidate`: useful idea, but not yet proven enough for a new permanent file
- `experimental`: active exploration that should stay out of the committed default surface

Bias toward improving an existing file before creating a new `candidate` artifact.

## Quality bar

- Prefer operational guidance over theory.
- Keep files concise, but not shallow.
- Preserve a consistent direct voice.
- Avoid slogans, branding language, and vague exhortations.
- Do not add nouns-swapped files that differ only in wording.
- Keep repo-specific commands, architecture, and domain rules out of this registry.

## Review checklist

Before opening a change, verify:

1. The new file has a distinct job.
2. The content is actionable, not ceremonial.
3. It does not duplicate an existing file.
4. It remains cross-repo and mostly stack-agnostic unless deliberately scoped.
5. Its maturity level is justified and not inflated.
6. It reflects current ecosystem direction without copying a marketplace repo's complexity.

## What not to optimize for

Do not grow this repository just to imitate large ecosystem catalogs.

This repo does not need, by default:

- a plugin marketplace
- generated search indexes
- a giant skill catalog
- bundles for every imaginable role
- tool-specific wrappers for every agent host

Those patterns are valid in larger repositories. They should only be added here if dotghost usage
creates a real need.