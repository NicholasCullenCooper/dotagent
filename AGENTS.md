# AGENTS.md

Reusable workflow registry for coding agents mounted into many repositories by dotghost.

This file is the root entrypoint. It explains how to use the registry without mixing in
project-specific build commands, architecture notes, or stack details. Those belong in the
target repository.

## Registry model

- `AGENTS.md`: the top-level operating brief and decision boundary.
- `agents/`: focused agent roles for isolated execution modes or subagent definitions.
- `commands/`: repeatable workflow entrypoints for common tasks.
- `workflows/`: outcome-level paths that compose commands and skills.
- `skills/`: reusable task playbooks and domain guidance. This is the main library.

Use the smallest unit that fits the task:

- Use `AGENTS.md` for broad working rules.
- Use an agent when the work benefits from a distinct role or tighter boundaries.
- Use a command when the task is a repeatable workflow entrypoint.
- Use a workflow when the outcome reliably spans several commands or skills.
- Use a skill when the task needs a reusable playbook, decision rules, and tradeoffs.

## Operating principles

- Prefer concrete action over vague planning.
- Preserve repository conventions before introducing your own.
- Fix root causes, not symptoms.
- Keep changes minimal, local, and reversible.
- Validate changes when possible with tests, linters, builds, or targeted checks.
- Separate reusable workflow guidance from repo-specific guidance.
- Ask when a decision is materially ambiguous, irreversible, or expensive to unwind.
- Do not create broad scaffolding without evidence that the repo needs it.

## Working boundary

This registry is reusable on purpose. It should contain:

- workflows that apply across many repos
- review and debugging methods
- implementation and release habits
- onboarding patterns for unfamiliar codebases

It should not contain:

- a specific repo's build commands
- local architecture facts
- product rules
- stack-specific mandates unless they are clearly scoped inside a skill

Put repo-specific guidance in the mounted repository, usually as a local `AGENTS.md`, nested
`AGENTS.md` files, or project docs committed with the code.

## Directory map

```text
agents/   focused execution roles
commands/ repeatable workflow entrypoints
workflows/ outcome-level paths through the registry
skills/   reusable playbooks and decision frameworks
```

## Usage

- Start here to understand the registry's intent and boundaries.
- Reach for `skills/` first when a task needs a concrete method.
- Use `commands/` to standardize recurring workflows like planning, review, or release.
- Use `workflows/` for common end-to-end outcomes like landing a feature or shipping a bug fix.
- Use `agents/` when a tool supports custom subagents or when a human wants a clear role split.

## Workflow layer

Workflows live in `workflows/` and sit one level above commands and skills.

- Keep workflows short and compositional.
- Point to existing commands and skills instead of restating them.
- Add a workflow only when the same multi-step path recurs across repositories.

Good fits are outcomes such as first change in an unfamiliar repo, bug fix, or feature delivery.

## Skill shape

Skills live in `skills/<name>/SKILL.md` on purpose.

- Keep the main `SKILL.md` focused on the workflow itself.
- Add supporting files only when a skill genuinely needs examples, scripts, templates, or reference
	material.
- Do not create support files as ceremony.

This follows the direction of the wider Agent Skills ecosystem while keeping the starter registry
lightweight.

## Maturity model

Use a small maturity vocabulary to keep the registry sharp.

- `core`: stable, broadly useful, and appropriate for the default mounted surface.
- `candidate`: promising, but needs more repeated usage before it earns a permanent standalone slot.
- `experimental`: active idea or narrow pattern that should stay out of the main surface until it hardens.

Default to `core` only when the artifact has broad cross-repo value. Avoid turning maturity into extra
directory sprawl until dotghost actually needs selective mounting for it.

## Packaging stance

This repository is a mounted registry first, not a marketplace catalog.

- Do not optimize the structure around one tool's plugin system.
- Do not add generated catalogs, installers, or bundle metadata unless dotghost usage proves they
	are needed.
- Favor portable markdown assets over harness-specific glue.

## Quality bar

- Be concise, but not shallow.
- Prefer operational guidance over theory.
- Avoid tool-specific ceremony unless it improves compatibility in practice.
- Expand the registry only after repeated use proves the gap is real.
