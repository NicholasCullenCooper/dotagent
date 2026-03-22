# CLAUDE.md

Claude Code compatibility shim for this registry.

Read `AGENTS.md` first. It is the primary source of reusable workflow guidance.

For Claude Code usage:

- Treat `agents/` as candidate subagent definitions or role briefs.
- Treat `commands/` as workflow entrypoints that can become slash commands if needed.
- Treat `skills/` as the main reusable library.
- Keep repo-specific conventions in the target repository, not in this registry.

If a Claude-specific feature conflicts with the reusable registry shape, prefer the reusable shape
unless the compatibility win is strong and recurring.
