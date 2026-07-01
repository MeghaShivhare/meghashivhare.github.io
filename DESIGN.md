# Design System — meghashivhare.github.io

## Concept: "Ops Dashboard"

The aesthetic is borrowed from the tools a DevOps engineer lives in daily:
dark monitoring dashboards (Grafana), terminals, and status pages.
Clean, dark, data-forward — the design serves the metrics.

Deliberately different from blueprint/drafting aesthetics (light ground, graphite lines).
This site is the **dark counterpart**: deep navy, terminal green, amber metrics.

---

## Color Tokens

```css
--bg:        #080D1A;   /* deep navy — not pure black, feels like dark-mode dashboard */
--surface:   #0F1729;   /* card / panel background */
--surface2:  #162035;   /* hover state surface, nested panels */
--border:    #1E2D4A;   /* hairline dividers */
--border2:   #263654;   /* stronger borders on hover */

--text:      #D4E5FF;   /* cool-white body text */
--muted:     #6B8CB8;   /* secondary text, labels */
--dim:       #3A5070;   /* tertiary — timestamps, decorative elements */

--green:     #00D97E;   /* PRIMARY accent — "operational" green, like Grafana uptime */
--green-dim: rgba(0, 217, 126, 0.12);   /* green tint for backgrounds */
--amber:     #F5A623;   /* metrics highlight — the big numbers */
--blue:      #4C9EFF;   /* links, tech tags */
--blue-dim:  rgba(76, 158, 255, 0.10);  /* tag backgrounds */
```

**Color discipline:**
- `--green` is the signature color. Use it for: status indicators, CTAs, section labels, accents.
- `--amber` is for numbers/metrics only. Never use it for UI chrome.
- `--blue` is for links and technology tags only.
- ~90% of the palette is monochrome navy/slate. Restraint is the point.

---

## Typography

**Inter** (body + headings): Clean grotesque, excellent screen rendering at all weights.
- Hero title: 700, `clamp(2rem, 5vw, 3.2rem)`, letter-spacing `-0.02em`
- Section titles: 600, `1.2rem`
- Body: 400–500, `15px`, line-height `1.7`

**JetBrains Mono** (annotations + code):
- All labels, tags, section numbers, status indicators, contact values, config-style skill rows
- Always uppercase with `letter-spacing: 0.08–0.15em` when used as labels
- Never used for body prose

**Scale rules:**
- Use `clamp()` for anything that appears in the hero
- Body line-length: 65–75ch max (enforced by `max-width` on `.wrap`)
- `text-wrap: balance` on headings

---

## Layout

- `max-width: 860px` centered with fluid gutters via padding
- Single-column throughout (no sidebar on portfolio pages)
- Sections separated by `1px solid var(--border)` hairlines
- Section header pattern: mono number tag + title + `flex: 1` line rule

---

## Components

### Stat Cards (hero metrics)
3-column grid. Amber number, small muted label. Subtle green glow on hover.
Numbers should always be the most important thing on the page.

### Timeline (experience)
Two-column grid: `140px` date column (right-aligned, mono) + content column.
Vertical hairline connector between items. Amber bold for key metrics in bullets.

### Skills Grid (config aesthetic)
Dark surface, mono font throughout. Groups styled as code comments (`# category`).
Keys in green, values in text color. Looks like a YAML/config file.

### Blog Cards
Dark surface cards with dashed-border placeholder for unpublished posts.
Tag → title → description → meta row hierarchy.

### Contact Items
Icon + label/value pairs in dark surface cards. Grid layout.

---

## Motion

- **Cursor blink** on hero title: `step-end` animation, 1.1s period
- **Status dot pulse** in nav: opacity oscillation, 2s ease-in-out
- **Hover transitions**: `0.15–0.2s` for `border-color`, `background`, `color`
- **No transform animations** except nav arrow on blog post items (`translateX(3px)`)
- **`prefers-reduced-motion`**: All animations should resolve to end-state instantly

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Voice & Content Principles

- Metrics first: every experience bullet with a number gets the number upfront
- Amber bold for quantified impact (`<strong>50%</strong>`, `<strong>40%</strong>`)
- Skills are formatted as config, not a tag cloud — reflects how DevOps thinks
- Blog posts are referenced as "notes" or "writing", not articles

---

## Using impeccable

After major content changes, run a polish pass:

```bash
npx impeccable polish the portfolio homepage
npx impeccable audit the blog listing page
```

Reference this file as DESIGN.md context when initializing:
```bash
npx impeccable init   # will pick up DESIGN.md automatically
```
