# Motion Design Reference

## Duration rules

| Category | Duration | Examples |
|---|---|---|
| Micro-interaction | 100–150ms | Button press, toggle, checkbox |
| Transition | 200–300ms | Panel open/close, tab switch, hover |
| Entrance/exit | 300–500ms | Modal, drawer, page transition |

Never exceed 500ms for UI motion. Longer durations feel sluggish.

## Easing

- **Entrances**: ease-out (fast start, gentle landing). Element arrives and settles.
- **Exits**: ease-in (gentle start, fast finish). Element accelerates away.
- **State changes**: ease-in-out (gentle start and end). Element morphs in place.
- **Never**: linear (except progress bars and looping animations). Linear feels mechanical.

```css
--ease-out:    cubic-bezier(0.16, 1, 0.3, 1);     /* Snappy entrance */
--ease-in:     cubic-bezier(0.55, 0, 1, 0.45);     /* Quick exit */
--ease-in-out: cubic-bezier(0.65, 0, 0.35, 1);     /* Smooth morph */
--spring:      linear(0, 0.006, ..., 1);            /* Spring physics */
```

## Reduced motion

Always respect the user's preference:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

Do not just slow animations down — remove them. Users who set this preference need it.

## Perceived performance

Motion can make loading feel faster:

- **Skeleton screens** > spinners. Show the shape of what is loading.
- **Optimistic updates** — reflect the action immediately, reconcile with server async.
- **Progressive reveal** — stagger entrance animations (50–100ms offset) so content flows in rather than popping.
- **Instant feedback** — button state changes should happen in <50ms, even if the action takes longer.

## What to animate

| Animate | Do not animate |
|---|---|
| State changes (open/close, show/hide) | Colors (unless interactive state) |
| Entrances and exits | Layout shifts (causes reflow) |
| Focus and hover states | Text content changes |
| Loading/progress indicators | Scroll position (let the browser handle it) |
| Micro-feedback (check, toggle) | Background patterns or textures |

## Scroll-driven animation

Use CSS scroll-driven animations for parallax and reveal effects:

```css
@keyframes fade-in {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.reveal {
  animation: fade-in linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 50%;
}
```

Prefer CSS-native scroll animations over JavaScript `IntersectionObserver` + class-toggle patterns when browser support allows.
