# Security

This repository contains reusable workflow instructions for coding agents.

That makes it lower risk than arbitrary executable tooling, but not risk-free. Agent-facing
instructions can still encourage unsafe behavior if they are poorly written, over-permissive, or
copied from untrusted sources.

## Security posture

- Keep the core registry markdown-first and portable.
- Do not add scripts, installers, or generated automation without a clear need.
- Treat external examples as research input, not copy-paste source material.
- Prefer workflows that preserve human review around destructive or irreversible actions.

## Contribution expectations

When adding or changing content:

1. Avoid instructions that normalize unsafe defaults.
2. Avoid hidden assumptions about credentials, production access, or bypassed review.
3. Avoid telling agents to fetch and execute remote code blindly.
4. Call out approval points where a workflow could become destructive.
5. Keep examples minimal and explicit about risk.

## Future expansion

If this repository later grows scripts, hooks, installers, or generated assets, it should also grow
stronger validation and review processes to match.

Until then, the main defense is deliberate scope control and careful review of agent-facing
instructions.