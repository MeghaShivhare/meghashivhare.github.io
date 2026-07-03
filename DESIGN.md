# Design System — meghashivhare.github.io

## Concept: "Editorial Maximalist"

Warm paper background, oversized black type, one loud accent color reserved
strictly for numbers and key facts. The aesthetic reads like a design studio's
self-promo site, not a résumé — the goal is a page recruiters remember after
they close the tab, while every metric that matters is still impossible to miss.

No profile photo. The hero leads with kinetic typography and a scrolling
tech-stack ticker instead — bigger impact, zero cropping/sizing problems.

---

## Color Tokens

```css
--bg:        #ede8e2;  /* warm paper background */
--ink:       #111;     /* primary text / headline black */
--muted:     #555;     /* body copy */
--dim:       #888;     /* labels, meta, timestamps */
--border:    #c8c4be;  /* hairline dividers on beige */
--accent:    #f97316;  /* THE signature color — every metric/number, nothing else */
```

**Color discipline:**
- `--accent` (orange) is reserved for numbers and quantified facts: hero stats,
  manifesto dollar figures, blog stat callouts. If it's not a metric, it's not orange.
- Dark cards (experience, thoughts, footer) use near-black gradients with their
  own differentiated number colors (green/blue) — fine to vary there since
  each card tells a distinct story, but the *first-impression* numbers in the
  hero must always be `--accent`.
- The sparkle emoji accents use a small rainbow gradient purely as a decorative
  flourish — don't pull from that gradient anywhere else.

---

## Typography

**System sans** (body + headings), **Courier New** (labels, meta, mono accents).
- Hero title: 900 weight, `clamp(3.5rem, 10vw, 9rem)`, one line rendered as
  hollow/outline text (`-webkit-text-stroke`) for contrast drama against the
  solid-fill line beneath it.
- Section titles: 800, `clamp(2.5rem, 5.5vw, 5rem)`.
- Body: 400–500, 15–16px, line-height 1.7–1.8.
- Mono labels: uppercase, `letter-spacing: 0.06–0.18em`.

---

## Layout

- No fixed `max-width` wrapper on the homepage — sections use `vw`-based
  padding so type can go edge-to-edge and feel large.
- Single accent color threaded through every page (home + blog) so the two
  don't feel like different sites.
- Sections separated by `1px solid var(--border)` hairlines.

---

## Components

### Hero
Full-width, no split panel, no photo. Structure: meta row (role/location +
copyright) → outline+solid two-line headline → one-sentence thesis statement
→ stat row (accent-colored numbers) → infinite-scroll tech marquee.

### Stat Row (hero + blog)
Numbers always `--accent`, bold, larger than surrounding text. Labels small,
muted, uppercase mono.

### Manifesto
Scroll-driven grey→black text reveal (`clip-path`). Dollar figures/key facts
bolded in `--accent` inside the reveal text.

### Experience Cards
Dark gradient cards, differentiated number colors per role (green/blue) — kept
distinct since they're deep-dives, not first-impression numbers.

### Marquee Ticker
CSS-only infinite horizontal scroll of the tech stack, sits at the bottom of
the hero. Duplicate the content list once so `translateX(-50%)` loops seamlessly.

### Blog ("Notes")
Same beige/black/accent system as the homepage — nav is a black bar/pill,
category and stat colors use `--accent`, not a different theme. The listing
page keeps the "drawing list" spreadsheet metaphor; individual posts can keep
self-contained content chrome (e.g. dark code blocks) since those read as
"embedded terminal" rather than page theme.

---

## Motion

- **Marquee scroll**: `26s linear infinite`, pauses visually fine under
  `prefers-reduced-motion` via the global animation-duration override below.
- **Manifesto reveal**: scroll-position-driven `clip-path`, no JS animation library.
- **Fade-up on scroll**: `IntersectionObserver`, `0.7s` opacity/transform.
- **Hover transitions**: `0.15–0.25s` for color/background/transform.
- **`prefers-reduced-motion`**: all animations resolve to end-state instantly.

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

- Metrics first, always `--accent`-colored, always bold.
- One punchy thesis sentence in the hero — this is the "memorable" line, not
  a job title restatement.
- Skills read as a spreadsheet/config list, not a tag cloud.
- Blog posts are "Notes", not "articles".
- No filler sections — an empty/half-built Projects section is worse than no
  section at all. Add one only when there's a real project to show.
