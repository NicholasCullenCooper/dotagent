# Interaction Design Reference

## Interactive states

Every interactive element must define all applicable states:

| State | Visual signal | Required for |
|---|---|---|
| Default | Base appearance | All interactive elements |
| Hover | Subtle change (background, underline, color shift) | Pointer devices |
| Focus | Visible ring or outline | All (keyboard navigation) |
| Active/pressed | Slight scale-down or darken | Buttons, links, controls |
| Disabled | Reduced opacity + no pointer events | Conditionally interactive elements |
| Loading | Spinner, skeleton, or pulse | Async actions |
| Selected | Distinct from hover/focus (background, border, icon) | Multi-select, tabs, toggles |
| Error | Red border/outline + error message | Form inputs |

Missing states make UI feel unfinished. Focus and disabled are the most commonly forgotten.

## Focus management

```css
/* Visible, intentional focus ring */
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}

/* Remove outline for mouse clicks (but keep for keyboard) */
:focus:not(:focus-visible) {
  outline: none;
}
```

- Focus rings must be visible against both light and dark backgrounds.
- Use `outline`, not `box-shadow`, for focus indicators. `box-shadow` is clipped by `overflow: hidden`.
- When opening modals/drawers, move focus to the first interactive element inside.
- When closing them, return focus to the trigger element.

## Keyboard patterns

| Component | Expected keys |
|---|---|
| Button | Enter, Space |
| Link | Enter |
| Tab list | Arrow keys to switch, Enter/Space to activate |
| Menu | Arrow keys to navigate, Enter to select, Escape to close |
| Dialog/modal | Escape to close, Tab trapped inside |
| Dropdown/select | Arrow keys, Enter to select, Escape to close, type-ahead |
| Checkbox | Space to toggle |
| Radio group | Arrow keys to move selection |

Use native HTML elements where possible — they get keyboard behavior for free. Custom components must implement these patterns.

## Touch targets

- Minimum 44×44px touch target (WCAG 2.5.8).
- Add padding or `min-height`/`min-width` — do not make the visible element bigger than the design calls for.
- Space touch targets at least 8px apart to prevent accidental taps.

## Popover and anchor positioning

Prefer the Popover API for tooltips, dropdowns, and menus:

```html
<button popovertarget="menu">Options</button>
<div id="menu" popover>
  <!-- menu content -->
</div>
```

Benefits: light-dismiss (click outside to close), top-layer stacking (no z-index wars), keyboard accessible by default.

For positioning relative to a trigger, use CSS anchor positioning where supported, with a JavaScript fallback (Floating UI) for broader compat:

```css
.tooltip {
  position: absolute;
  position-anchor: --trigger;
  top: anchor(bottom);
  left: anchor(center);
}
```
