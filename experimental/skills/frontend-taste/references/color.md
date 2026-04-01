# Color Reference

## Color spaces

Use OKLCH for perceptually uniform color manipulation:

```css
/* OKLCH: lightness, chroma, hue */
--primary: oklch(0.65 0.25 250);      /* Saturated blue */
--primary-light: oklch(0.85 0.12 250); /* Same hue, lighter */
--primary-dark: oklch(0.45 0.20 250);  /* Same hue, darker */
```

OKLCH maintains perceived brightness when you shift hue — HSL does not. A "50% lightness" yellow in HSL looks much brighter than a "50% lightness" blue.

## Tinted neutrals

Never use pure gray. Tint your neutrals toward your primary color:

```css
/* Instead of gray-100 through gray-900 */
--neutral-50:  oklch(0.97 0.005 250);  /* Almost white, hint of blue */
--neutral-100: oklch(0.93 0.008 250);
--neutral-200: oklch(0.87 0.010 250);
--neutral-500: oklch(0.60 0.015 250);
--neutral-800: oklch(0.30 0.020 250);
--neutral-950: oklch(0.15 0.015 250);  /* Almost black, hint of blue */
```

This creates visual cohesion. The difference is subtle but the result feels intentional.

## The 60-30-10 rule

Distribute color by visual weight:

- **60% dominant** — background, large surfaces. Usually your lightest neutral.
- **30% secondary** — cards, sections, supporting elements. Your mid-tone or secondary color.
- **10% accent** — buttons, links, highlights, calls to action. Your primary or accent color.

This ratio prevents visual chaos. Breaking it intentionally (a bold hero section, an accent-heavy dashboard) is fine — but know the baseline you are breaking from.

## Semantic color roles

Define colors by role, not by value:

```css
--color-surface:     /* Page background */
--color-surface-alt: /* Card/section background */
--color-border:      /* Dividers, outlines */
--color-text:        /* Primary body text */
--color-text-muted:  /* Secondary text, captions */
--color-primary:     /* Primary actions, links */
--color-success:     /* Positive states */
--color-warning:     /* Caution states */
--color-error:       /* Error states, destructive actions */
```

## Dark mode strategy

Do not invert. Redesign:

- **Reduce chroma** — saturated colors on dark backgrounds vibrate and strain eyes. Drop chroma by 20-30%.
- **Reduce contrast** — pure white on pure black is harsh. Use off-white (~95% lightness) on dark gray (~15% lightness).
- **Elevate with lightness** — in dark mode, "higher" elements (cards, modals) are lighter, not darker. This replaces shadows.
- **Test your entire palette** — each semantic color needs a dark mode variant. Generate them systematically, do not eyeball.

```css
/* Light mode */
--color-surface: oklch(0.98 0.005 250);
--color-text: oklch(0.15 0.015 250);

/* Dark mode */
--color-surface: oklch(0.15 0.010 250);
--color-text: oklch(0.93 0.008 250);
```

## Contrast requirements

| Element | Minimum ratio (WCAG AA) |
|---|---|
| Normal text (<18px) | 4.5:1 |
| Large text (≥18px bold or ≥24px) | 3:1 |
| UI components and graphics | 3:1 |
| Decorative elements | No requirement |

Check with browser DevTools (Inspect → color picker → contrast ratio) or a tool like Polypane.
