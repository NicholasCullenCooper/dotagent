# CLAUDE.md — Claude-specific universal instructions

This file supplements AGENTS.md with Claude Code-specific conventions.

## Memory

- Read AGENTS.md for cross-tool standards (working style, testing policy, git workflow).
- Project-specific context (build commands, architecture) lives in each repo's own docs.

## Claude-specific behavior

- Use `gh` CLI for GitHub operations (issues, PRs, labels).
- Use `git diff --cached` before every commit to review changes.
- When creating files, prefer the project's established directory structure.
- When uncertain about a library API, use `/docs` or web search before guessing.

## Commit messages

Format: `<type>: <description>`

Types: `feat`, `fix`, `refactor`, `test`, `docs`, `chore`, `style`

Include test counts when tests are added: `feat: add user validation (12 tests)`
