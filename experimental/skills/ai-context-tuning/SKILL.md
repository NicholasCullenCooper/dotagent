---
name: ai-context-tuning
description: Experimental skill for optimizing AI agent context — tuning AGENTS.md, skills, and instructions for better agent output quality.
---

# AI Context Tuning

## Status

Experimental. This skill is not included in default profiles. Mount explicitly with `--include-ignored` or by path to try it.

## When to use

- Agent output quality is inconsistent or declining
- You're setting up a new repo's AI configuration for the first time
- You want to audit which instructions are helping vs. adding noise
- Context window is getting crowded and you need to trim

## Workflow

1. **Audit current context.** List all files the agent sees (AGENTS.md, CLAUDE.md, mounted skills, MCP tool descriptions). Estimate total token count.

2. **Identify noise.** Look for:
   - Redundant instructions (same rule stated in 3 files)
   - Stale instructions (reference removed features or old conventions)
   - Overly general guidance ("write clean code") that doesn't change behavior
   - Tool descriptions consuming tokens but rarely invoked

3. **Rank by impact.** For each instruction:
   - Does removing it change agent behavior? Test by removing and running the same task.
   - Does it address a recurring failure mode? Keep it.
   - Is it specific enough to act on? If not, make it concrete or remove it.

4. **Consolidate.** Merge overlapping instructions. Move project-specific rules to a single AGENTS.md section rather than scattering across files.

5. **Test.** Run the same 3-5 representative tasks before and after changes. Compare output quality, not just whether it "looks right."

## Decision rules

- Fewer, sharper instructions beat many vague ones.
- Context that addresses a real failure mode is worth the tokens.
- Context that "might help someday" is not worth the tokens.
- When in doubt, remove and see if quality drops. It usually doesn't.

## Anti-patterns

- Adding instructions reactively after every bad output without testing if they help.
- Copy-pasting someone else's full AGENTS.md without adapting to your project.
- Using AI to generate AI instructions without human review of the result.
