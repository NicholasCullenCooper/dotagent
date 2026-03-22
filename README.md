# dotagent

dotagent is a reusable agent workflow registry intended to be mounted by dotghost into many
repositories.

It is not a project template. It is a shared workflow layer: a clean root `AGENTS.md`, a small
set of reusable agent roles, a compact command vocabulary, a thin workflow layer, and a sharp
skills library that can be applied across codebases.

## What this registry is for

Use this repository to keep cross-repo workflow guidance in one place.

Good fits:

- implementation habits that work across stacks
- code review, debugging, testing, and release workflows
- reusable agent roles such as explore, review, or debug
- command-style entrypoints for repeatable work
- outcome-level workflows such as bug fix or first change
- onboarding guidance for unfamiliar repositories

Bad fits:

- a repo's build commands
- codebase architecture notes
- product rules
- stack-specific requirements that only apply to one repository

Those belong in the mounted repository itself.

## How dotghost should use it

dotghost should mount this registry into target repositories so the agent-visible files appear at
the repo root.

The expected mounted shape is:

```text
AGENTS.md
CLAUDE.md
agents/
commands/
workflows/
skills/
```

The registry can also carry dotghost control-plane files such as `dotghost.profiles.json`. Those are
consumed by dotghost but are not mounted into target repositories.

The mounted repository can then add its own local guidance alongside this registry. In practice,
that means:

- this registry provides reusable workflow defaults
- the target repo provides local facts, commands, architecture, and exceptions

## What AGENTS.md does

`AGENTS.md` is the root entrypoint. It explains the registry's philosophy, boundaries, and how the
other directories relate to each other.

Keep it short. If `AGENTS.md` turns into a giant policy dump, the registry has started to rot.

This repository also follows the broader Agent Skills direction: skills are directory-based,
portable, and able to grow supporting files only when warranted.

## What belongs where

### agents/

Focused role definitions.

Use this directory for execution personas or subagent briefs such as:

- explore a codebase without editing
- implement a scoped change
- review changes for risk
- debug a failing path
- research an unfamiliar dependency or pattern

These files should define when to use the role, what inputs it needs, what it should return, and
what it should avoid.

### commands/

Repeatable workflow entrypoints.

Use this directory for tasks that recur across repositories and benefit from a stable sequence,
such as planning, implementation, review, refactoring, debugging, and release preparation.

Commands should stay thin. They start a workflow; they should not duplicate the entire skill
library.

### workflows/

Outcome-level compositions.

Use this directory for short, cross-repo paths that stitch together existing commands and skills,
such as:

- taking a bug from report to verified fix
- landing a feature with planning, testing, and review
- getting productive in an unfamiliar repository and making a first safe change

Workflows should stay short. They are route maps, not long-form reference material.

### skills/

Reusable playbooks.

This is the most important directory. Each skill should explain:

- what it is for
- when to use it
- what to gather first
- the workflow to follow
- the decision rules that matter
- the common failure modes

Skills are stored as `skills/<name>/SKILL.md` so they can grow support files later without
changing the overall structure.

## Extending the registry safely

Add a new file only when repeated usage shows a real gap.

Before adding something new:

1. Check whether the need is better handled by an existing skill.
2. Decide whether the new artifact is an agent, a command, a workflow, or a skill.
3. Keep the scope narrow enough that the file has a distinct job.
4. Avoid synonyms. If two files differ only in tone, one of them should not exist.
5. Keep repo-specific facts out of the registry.

Use these rules:

- add an agent when the work benefits from a distinct role or boundary
- add a command when users need a repeatable entrypoint
- add a workflow when the same end-to-end outcome spans several registry assets
- add a skill when the task needs a reusable method or decision framework

For contribution expectations and review criteria, see `CONTRIBUTING.md`.

## Reusable versus repo-specific guidance

Keep reusable here:

- review methods
- debugging workflows
- release checklists
- refactoring habits
- onboarding methods

Keep repo-specific elsewhere:

- exact test and build commands
- architectural decisions for one codebase
- service ownership and deployment details
- local product and domain rules

## Current layout

```text
AGENTS.md
CLAUDE.md
dotghost.profiles.json
agents/
	debugger.md
	explore.md
	implementer.md
	researcher.md
	reviewer.md
commands/
	debug.md
	implement.md
	plan.md
	refactor.md
	release.md
	review.md
workflows/
	repo-first-change.md
	ship-a-bug-fix.md
	ship-a-feature.md
skills/
	code-review/SKILL.md
	debugging/SKILL.md
	dependency-upgrades/SKILL.md
	performance-investigation/SKILL.md
	refactoring/SKILL.md
	release-management/SKILL.md
	reproduction/SKILL.md
	repo-onboarding/SKILL.md
	root-cause-analysis/SKILL.md
	testing/SKILL.md
```

## Maturity model

Keep the maturity model small:

- `core`: stable and broadly useful; safe for the default mounted surface
- `candidate`: promising, but not yet proven enough to deserve a permanent new file
- `experimental`: active idea or narrow pattern that should not expand the default surface yet

Current committed content should be assumed `core` unless stated otherwise. For now, maturity is a
review rule, not a directory tree. If dotghost later gains strong selective mounting, that can
change deliberately.

dotghost profiles provide a second lever: they let this registry expose named mount surfaces without
turning maturity into folder sprawl.

## Design stance

This registry favors fewer, stronger files over broad, shallow coverage.

If a future addition looks like template theater, the right move is usually to stop, merge it into
an existing file, or wait until real usage proves it deserves its own slot.

## Why this is not a marketplace repo

Many state-of-the-art collections now include plugin marketplaces, installer CLIs, searchable web
catalogs, generated indexes, and bundle guides.

Those are useful patterns when the repository itself is the product.

dotagent has a different job:

- it is a central mounted registry for dotghost
- it should stay easy to understand at the file level
- it should not require an installer or catalog layer to be useful

If repeated usage later proves that bundles, catalogs, or machine-readable indexes would improve
the mounted experience, they can be added deliberately rather than by imitation.
