# Typography Reference

## Type scale

Use a modular scale. Common ratios:

| Ratio | Name | Feel |
|---|---|---|
| 1.125 | Major second | Tight, compact UI |
| 1.200 | Minor third | General purpose |
| 1.250 | Major third | Slightly editorial |
| 1.333 | Perfect fourth | Strong hierarchy |
| 1.414 | Augmented fourth | Magazine, editorial |
| 1.618 | Golden ratio | Dramatic headlines |

Pick one ratio. Derive all sizes from it. Do not invent sizes.

## Fluid type

Use `clamp()` for responsive sizing instead of breakpoint jumps:

```css
/* Base: 16px at 375px → 18px at 1440px */
font-size: clamp(1rem, 0.915rem + 0.42vw, 1.125rem);

/* Heading: 28px at 375px → 48px at 1440px */
font-size: clamp(1.75rem, 1.1rem + 2.6vw, 3rem);
```

## Font pairing

Rules of thumb:

- **One font is often enough.** Weight and size variation create hierarchy without a second face.
- **If two fonts, contrast them.** Serif headline + sans body, or geometric sans + humanist sans. Not two similar sans-serifs.
- **Match x-height.** Paired fonts should have similar x-heights so they feel balanced at the same size.
- **Test at body size.** A display font that looks great at 48px may be unreadable at 14px.

## Web font loading

```css
/* Prevent layout shift from font loading */
@font-face {
  font-family: 'YourFont';
  font-display: swap; /* or optional for non-critical text */
  src: url('...') format('woff2');
}
```

Subset fonts to the characters you use. A full Google Font can be 200KB; subsetting to Latin cuts it to 15-20KB.

## OpenType features

Enable features the font supports:

```css
/* Tabular numbers for aligned columns */
font-variant-numeric: tabular-nums;

/* Ligatures for body text */
font-variant-ligatures: common-ligatures;

/* Small caps for labels */
font-variant-caps: small-caps;

/* Old-style figures for running text */
font-variant-numeric: oldstyle-nums;
```

## Line height and measure

- **Body text**: line-height 1.5–1.7, measure 45–75 characters.
- **Headings**: line-height 1.1–1.3 (tighter than body).
- **UI labels**: line-height 1.2–1.4.
- Longer lines need more line-height. Shorter lines need less.

## Weight usage

Do not use more than 3 weights of the same font. A typical system:

- **Regular (400)** — body text.
- **Medium (500)** or **Semibold (600)** — subheadings, labels, emphasis.
- **Bold (700)** — headings, primary actions.

Avoid light weights (300) for body text — they are hard to read on low-DPI screens.
