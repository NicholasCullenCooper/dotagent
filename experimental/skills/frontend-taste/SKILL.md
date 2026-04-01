---
name: frontend-taste
description: "Experimental: Encode design taste — anti-patterns, aesthetic constraints, and quality baselines — into frontend work so AI-generated UI does not default to generic slop. Use when building, reviewing, or polishing user-facing interfaces."
---

# Frontend Taste

> **Status**: Experimental. Mount with `--include-ignored` to try.

## What this is for

AI-generated frontends default to safe, generic output. This skill encodes specific aesthetic constraints and anti-patterns so that generated UI has intentional design choices rather than default ones. It is not a design system — it is a set of bias corrections and quality gates.

## When to use it

- Building new UI where you want the output to look designed, not generated.
- Reviewing AI-generated frontend code for visual quality.
- Polishing an existing interface that feels bland or generic.
- Any time the output looks like "every AI demo ever."

## When to skip it

- Backend work, API design, infrastructure.
- You have a full design system or Figma mocks to implement against.
- The work is functional (admin panels, internal tools) where aesthetics are secondary.

## Gather first

- Visual references if available (screenshots, URLs, mood boards).
- The project's existing design language (colors, typography, spacing conventions).
- Framework constraints (React, Vue, Svelte, plain HTML — this skill is framework-agnostic).

## The AI Slop Test

Before shipping any UI, check for these tells. If more than two are present, the output needs work:

- [ ] Inter or system-ui as the only typeface with no intentional pairing.
- [ ] Purple-to-blue gradients with no connection to the brand.
- [ ] Gray text on colored backgrounds (poor contrast, reads as unfinished).
- [ ] Cards nested inside cards nested inside cards.
- [ ] Uniform border-radius on everything (the "pillow" look).
- [ ] Stock-photo hero with centered text overlay.
- [ ] Excessive whitespace with no visual rhythm or tension.
- [ ] Every section is a centered container with max-width: 1200px.
- [ ] Hover effects that add box-shadow and translateY(-2px) on every element.
- [ ] Color palette is "SaaS blue" — #3B82F6 and its friends.

These are not universally wrong — they are signals that no design decision was made.

## Anti-patterns by category

### Typography
- **Do not** use a single font weight across the entire page.
- **Do not** default to 16px for everything. Establish a type scale.
- **Do** create hierarchy through size, weight, and spacing — not just bold.
- **Do** limit to two typefaces maximum. One is often enough.
- **Do** use fluid type (clamp) for responsive sizing rather than breakpoint jumps.

### Color
- **Do not** pick a primary color and lighten/darken it for every shade.
- **Do not** use pure black (#000) on pure white (#fff) — it is harsh.
- **Do** use tinted neutrals that relate to your primary color.
- **Do** apply the 60-30-10 rule: 60% dominant, 30% secondary, 10% accent.
- **Do** check contrast ratios (WCAG AA minimum: 4.5:1 for text).

### Layout and spacing
- **Do not** center everything. Asymmetry creates visual interest.
- **Do not** use the same padding/margin everywhere. Establish a spacing scale (4px base).
- **Do** use a consistent grid but break it intentionally for emphasis.
- **Do** create visual rhythm — alternating dense and spacious sections.
- **Do** let content breathe at the edges. Full-bleed elements create drama.

### Motion
- **Do not** animate everything. Motion should draw attention to what matters.
- **Do not** use linear easing — it looks mechanical. Use ease-out for entrances, ease-in for exits.
- **Do** keep durations short: 100ms for micro-interactions, 300ms for transitions, 500ms max for page-level.
- **Do** respect `prefers-reduced-motion`. Remove non-essential animation entirely.
- **Do** use motion to communicate state changes, not for decoration.

### Interaction
- **Do not** forget hover, focus, active, and disabled states. Every interactive element needs all four.
- **Do not** rely on hover alone — touch devices have no hover.
- **Do** make focus rings visible and intentional (not the browser default, not hidden).
- **Do** use the popover API and anchor positioning for tooltips and dropdowns where supported.

## Constraint prompting

When generating UI, provide constraints up front rather than hoping for good output. Structure:

```
Design constraints:
- Visual thesis: [one sentence describing the intended feel]
- Typography: [specific fonts and scale]
- Color: [palette with roles — dominant, secondary, accent]
- Layout: [grid approach, key breakpoints]
- Motion: [intent — minimal, expressive, functional only]
- Hard rules: [non-negotiable constraints from the anti-patterns above]
```

This is more effective than post-hoc critique. Tell the AI what you want before it generates, not after.

## Design DNA extraction (optional)

When working from visual references, extract design tokens before generating:

1. **Tokens** (measurable): colors, type scale, spacing scale, border-radius, shadows, breakpoints.
2. **Style** (qualitative): aesthetic feel, visual language, composition approach, brand voice.
3. **Effects** (technical): background treatments, scroll behaviors, cursor effects, micro-interactions.

Capture these as a structured reference (JSON, markdown table, or design tokens file) and use them as constraints for generation. This turns subjective "make it look like that" into reproducible specifications.

## Verification

After generating UI:

1. Run the AI Slop Test checklist.
2. Check at three viewports: mobile (375px), tablet (768px), desktop (1440px).
3. Verify all interactive states exist (hover, focus, active, disabled).
4. Check contrast ratios on text elements.
5. If the page has motion, verify it respects `prefers-reduced-motion`.

## Decision rules

- Constraints before generation beats critique after generation.
- One strong typeface with clear hierarchy beats two typefaces with no hierarchy.
- Visual tension (asymmetry, contrast, density variation) beats uniformity.
- Removing a default is a design decision. Adding a flourish is often not.
- When in doubt, look at a reference you admire and extract what makes it work.

## Failure modes

- **Applying all anti-patterns as rigid rules.** These are defaults for when no design direction exists. If you have a design system, follow it — even if it uses Inter and border-radius.
- **Over-designing functional interfaces.** Admin panels and internal tools should prioritize clarity over aesthetics.
- **Adding motion for delight without purpose.** Every animation should answer "what does this help the user understand?"
- **Ignoring accessibility for aesthetics.** Low-contrast text is not a design choice — it is a bug.

## References

See `references/` directory for deeper guidance on:
- [typography.md](references/typography.md) — Type scale, font pairing, fluid type, OpenType features
- [color.md](references/color.md) — Color spaces, tinted neutrals, dark mode strategy
- [spatial.md](references/spatial.md) — Spacing scale, container queries, z-index
- [motion.md](references/motion.md) — Duration rules, easing, perceived performance
- [interaction.md](references/interaction.md) — States, focus management, keyboard patterns

## Output

UI code that passes the AI Slop Test and reflects intentional design choices. Not "beautiful" in the abstract — appropriate, intentional, and well-crafted for the specific context.
