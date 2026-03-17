# dotagent

Personal AI agent configuration — universal instructions, skills, and rules for coding agents.

This repo is the global registry for [SDF (Shadow Directory Framework)](https://github.com/NicholasCullenCooper/syncdotfile). SDF mounts these files into any Git repository via symlinks, invisible to version control.

## What's here

```
AGENTS.md       Universal agent instructions (Codex, OpenCode, any tool that reads AGENTS.md)
CLAUDE.md       Claude Code-specific conventions
```

## How it works

```bash
# One-time setup: clone this repo as your SDF registry
sdf init https://github.com/NicholasCullenCooper/dotagent.git

# In any project: mount your agent context
cd my-project
sdf mount

# Your global AGENTS.md, CLAUDE.md, etc. appear at the project root.
# Git ignores them. Your agent reads them. Edits sync back here.

# When done
sdf unmount    # removes symlinks, restores any originals
```

## Philosophy

These instructions encode how I work with AI coding agents:

- **Discuss before implementing.** Agents should present options and decision points, not silently pick an approach.
- **No commits without approval.** The human reviews and merges.
- **Test what matters.** Pure functions, state stores, branching logic always get tests. Thin wrappers don't.
- **Feature branches only.** Never push to main directly. PRs for everything.
- **Flag uncertainty.** Stop and ask rather than guessing. A wrong assumption costs more than a question.
- **Docs stay in sync.** If code changes behavior, the docs update in the same commit.

The universal instructions apply to every project. Project-specific context (build commands, architecture, stack conventions) stays committed in each repository.

## Adding files

Drop any file into this repo and `sdf pull` + `sdf mount` will make it available in all your projects:

- `.cursorrules` — Cursor editor rules
- `.github/copilot-instructions.md` — GitHub Copilot instructions
- `skills/*.md` — Prompt templates for specific tasks (debugging, code review, refactoring)
- `.factory/droids/*.md` — Factory droid configurations

## Syncing

```bash
# Pull latest (after editing on another machine or via GitHub)
sdf pull

# Push local changes (after an agent improves a file through a symlink)
sdf push
```
