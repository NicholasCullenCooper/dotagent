# Spatial Design Reference

## Spacing scale

Use a 4px base unit. Common scale:

| Token | Value | Use |
|---|---|---|
| space-1 | 4px | Tight gaps (icon-to-text) |
| space-2 | 8px | Related element spacing |
| space-3 | 12px | Compact padding |
| space-4 | 16px | Standard padding, gap |
| space-6 | 24px | Section padding |
| space-8 | 32px | Card padding, larger gaps |
| space-12 | 48px | Section margins |
| space-16 | 64px | Page-level spacing |
| space-24 | 96px | Hero spacing |

Do not invent values outside the scale. If 24px is not enough and 32px is too much, the problem is elsewhere.

## The squint test

Blur your vision (or squint at the screen). You should still be able to identify:

- Where sections begin and end.
- What is a heading vs. body text.
- Where the primary action is.

If everything looks like an even gray blur, the spacing and hierarchy need work.

## Container queries

Prefer container queries over media queries for component-level layout:

```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .card { flex-direction: row; }
}
```

Components should respond to their container, not the viewport. This makes them reusable across contexts.

## Z-index scale

Use a named scale, not arbitrary numbers:

```css
--z-base:     0;
--z-dropdown: 100;
--z-sticky:   200;
--z-overlay:  300;
--z-modal:    400;
--z-popover:  500;
--z-toast:    600;
```

Never use z-index values outside the scale. If you need a new layer, add it to the scale.

## Grid usage

- Use CSS Grid for page layout, Flexbox for component layout.
- A 12-column grid handles most layouts. 4-column for mobile.
- Break the grid intentionally — full-bleed images, asymmetric hero layouts — but return to it for content sections.
- `gap` is your friend. Do not use margins between grid children.

## Safe areas

Account for device safe areas on mobile:

```css
padding-bottom: env(safe-area-inset-bottom);
padding-left: env(safe-area-inset-left);
padding-right: env(safe-area-inset-right);
```

Especially important for bottom navigation bars and fixed CTAs.
