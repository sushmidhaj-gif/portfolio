# Case study page pattern guide

Reference for building new work case study pages so they stay aligned with the home portfolio (`portfolio (6).html`) and shared tokens in `style.css`. Implementation lives in `case-study.css`; each page is an HTML file that loads **`style.css` first**, then **`case-study.css`**.

---

## 1. Page shell (must match)

| Decision | Detail |
|----------|--------|
| **Root classes** | `class="case-study"` on **both** `<html>` and `<body>`. |
| **Why** | Turns off home scroll-snap (`scroll-snap-type: none` on `html`) and restores default cursor (`cursor: auto` on `body`). Home uses `cursor: none` and mandatory y-snap. |
| **Stylesheet order** | `../style.css` → `../case-study.css` (paths adjust if the file is not under `work/`). |
| **Fonts** | Same Google Fonts link as home: **DM Sans** + **Cormorant Garamond** (weights used in the reference page). Typography must use only `var(--sans)` and `var(--serif)` — no extra families. |
| **Body type** | Case study body: 16px, weight 300, line-height 1.75 (readable long-form default). |

---

## 2. Style choices aligned with the home page

- **Design tokens** — Always use CSS variables from `:root` in `style.css`: `--navy`, `--teal`, `--mauve`, `--brown`, `--blush`, `--ink-muted`, `--line`, `--serif`, `--sans`, `--page-pad-x`. Do not introduce one-off palette hexes for structural UI unless mirroring the documented hero overrides (see §4).
- **Pill controls** — Uppercase, ~12px sans, letter-spacing ~0.06em, `border-radius: 100px`, 1.5px borders, `translateY(-2px)` on hover — same language as `.btn-navy` / `.ws-link` on the home page.
- **Eyebrow / label pattern** — 11px sans, uppercase, `letter-spacing: 0.12em` — matches work slide `.ws-num` / `.ws-label` rhythm.
- **Section labels on blush** — `.cs-section-label` mirrors the hero eyebrow idea: line + navy rule (32px wide, 30% opacity), paired with muted ink for the label text.
- **Nav** — Reuse the same `<nav id="main-nav">` markup and classes as the case study reference (`nav.light` when over dark hero/footer). Home uses `nav.light` over dark sections; case studies use a small script to toggle `light` when the scroll position overlaps `.cs-hero-project` or `footer`.

---

## 3. Layout width and horizontal rhythm

| Element | Rule |
|---------|------|
| **Content max-width** | **1100px** centered (`max-width: 1100px; margin: 0 auto`) for `.cs-main`, `.cs-hero-inner`, `.cs-cover`, `.cs-section-block`, `.cs-confidential-split`. Keeps line length and alignment consistent with the portfolio’s work area. |
| **Horizontal padding** | **`var(--page-pad-x)`** (7vw in `:root`) — same gutter as the home hero and work slides. Use it on hero, body shell, and any full-bleed-to-pad region. |
| **Grids** | Hero: 2 columns (`1fr 1fr`), gap `clamp(32px, 5vw, 64px)`. Body columns (`.cs-two-col`, challenge/framework grids): two or three columns with responsive collapse to one column at **768px**. |

---

## 4. Project hero colors (map to home work slides)

Pick **one** modifier on `<header class="cs-hero-project">` so the case study hero matches the corresponding home `#work-n` slide:

| Class | Home slide | Background | Notes |
|-------|------------|------------|--------|
| *(none)* | `#work-1` | `--navy` | Default. Muted label `#a8c4d0`, desc `#c8dfea`, title/tags on `--blush`. |
| `.cs-hero-project--teal` | `#work-2` | `--teal` | Muted `#d4eef3`, desc `#eaf6f9`. |
| `.cs-hero-project--mauve` | `#work-3` | `--mauve` | Dark text on light tint: title `--navy`, `.cs-back` gets inverted pill treatment. |
| `.cs-hero-project--brown` | `#work-4` | `--brown` | Muted `#ead9ce`, desc `#f0e4db`. |

**Hero copy classes** — Reuse the **same class names** as the work slides: `.ws-num`, `.ws-label`, `.ws-title`, `.ws-desc`, `.ws-tags`, `.ws-tag`. `case-study.css` re-specifies them inside `.cs-hero-project` so metrics match `#work-1`; colored slides use the `--teal` / `--mauve` / `--brown` blocks for label/body colors.

---

## 5. Padding and spacing (reference values)

Values use **`clamp()`** for fluid spacing; reuse the same classes rather than inventing new margins.

| Region | Pattern |
|--------|---------|
| **`.cs-hero-project`** | `clamp(72px, 12vw, 120px)` top, `var(--page-pad-x)` sides, `clamp(48px, 8vw, 72px)` bottom — aligns with “body below hero” shell. |
| **`.cs-body-shell`** | Same vertical/side padding as hero top/sides/bottom so the fold from hero to blush feels continuous. |
| **`.cs-main`** | (If used) `clamp(48px, 8vw, 88px)` top, `clamp(64px, 10vw, 100px)` bottom, horizontal `--page-pad-x`. |
| **`.cs-cover`** | Bottom padding only: `clamp(48px, 6vw, 72px)` under the frame. |
| **`.cs-section-block`** | Vertical `clamp(56px, 7vw, 80px)`; `border-bottom: 1px solid var(--line)`; first block inside `.cs-body-shell` has `padding-top: 0`. |
| **`.cs-section`** (stacked sections) | Bottom margin `clamp(40px, 6vw, 56px)`. |
| **`.cs-meta`** | Column gap 22px; left border + `padding-left: clamp(0px, 3vw, 32px)`; on mobile, top border and padding instead. |
| **`.cs-callout`** | Inner padding `clamp(24px, 4vw, 32px)` × `clamp(20px, 4vw, 32px)`. |
| **`.cs-confidential-split`** | Top padding `clamp(56px, 7vw, 80px)` inside `.cs-confidential-wrap` (which only adds top border). |

---

## 6. Typography and text formatting

### Roles

- **Serif (`var(--serif)`)** — Display titles: hero `h1.ws-title`, section titles `.cs-section-title`, block titles `.cs-block-title`, pull quote body `.cs-pull-quote-text`, stat numbers `.cs-stat-num`, confidential heading, framework/challenge titles. Weights are mostly 300–600 depending on hierarchy.
- **Sans (`var(--sans)`)** — Everything else: body copy, labels, meta, buttons, lists.

### Repeating specs

| Use case | Spec (typical) |
|----------|----------------|
| Uppercase labels | 11px, weight 300 or 500, `letter-spacing: 0.1em–0.12em` |
| Hero title | `clamp(40px, 5vw, 72px)`, weight 300, line-height ~1.05, letter-spacing ~-0.025em |
| Block section title | `clamp(24px, 2.8vw, 32px)` serif, weight 600 |
| Block number (italic) | `clamp(22px, 2.4vw, 30px)` serif italic, **color `var(--teal)`** |
| Body paragraphs | 16px, weight 300, line-height 1.75, color `var(--ink-muted)` |
| **Strong in body** | Weight 500, color `var(--navy)` |
| **Emphasis in body** | Italic sans, weight 500, color `var(--teal)` (`.cs-body-para em`) |
| Intro lead line | `.cs-intro-line`: 16px, weight 500, `var(--navy)` |
| Links in prose | `var(--navy)`, underline, `text-underline-offset: 3px` |

### Prose width

- **`.cs-prose`** / **`.cs-after-framework`**: cap long lines with `max-width: 42em` where specified — improves readability on blush.

---

## 7. Color usage on the “blush” body

- **Page background** — `body` / `--blush` (white in current tokens).
- **Primary text** — Headings and strong: `--navy`. Body: `--ink-muted`.
- **Accent** — Teal for italic numerals, framework labels, light stat card numbers, confidential heading strong, list bullets (`→` in teal).
- **Borders / dividers** — `var(--line)`; section blocks use bottom border only.
- **Dark panels** — `.cs-pull-quote` and `.cs-stat-card` (default): `--navy` background, `--blush` text; muted white rgba for overlines and secondary lines.
- **Cards on white** — Light stat variant, challenge cards, framework cards, preview card: `--blush` fill + `var(--line)` border; optional subtle shadow on callout (`rgba(8, 54, 84, 0.04)`).

---

## 8. Reusable layout and content components

Use these class names from `case-study.css` instead of duplicating structure.

| Component | Classes | Purpose |
|-----------|---------|---------|
| **Hero** | `.cs-hero-project` (+ optional `--teal` / `--mauve` / `--brown`), `.cs-hero-inner`, `.cs-hero-copy` | Two-column hero + `.ws-*` copy. |
| **Meta column** | `.cs-meta`, `.cs-meta-item`, `label` + `p` | Role, timeline, team, scope. |
| **Back link** | `a.cs-back` | Pill “← All work”; adapts for mauve hero. |
| **Body wrapper** | `.cs-body-shell` | Wraps everything below hero (cover + sections + confidential). |
| **Cover image** | `.cs-cover`, `.cs-cover-frame`, `.cs-cover-caption` | Bordered frame (default aspect 946×672), caption row (left navy, right muted). |
| **Numbered section** | `.cs-section-block`, `.cs-block-header`, `.cs-block-num`, `.cs-block-title` | Flow sections with teal italic index. |
| **Two columns** | `.cs-two-col` + `.cs-body-para` | Equal columns; stacks ≤768px. |
| **Intro line** | `.cs-intro-line` | Short navy lead-in before a grid. |
| **Challenges** | `.cs-challenge-grid`, `.cs-challenge-card`, `.cs-challenge-num`, `.cs-challenge-title`, `.cs-challenge-text` | Pair of bordered cards. |
| **Pull quote** | `.cs-pull-quote`, `.cs-pull-quote-label`, `.cs-pull-quote-text` | Navy block, serif italic quote. |
| **Framework pillars** | `.cs-framework-grid`, `.cs-framework-card`, `.cs-framework-label`, `.cs-framework-title`, `.cs-framework-text` | Top navy bar + card. |
| **Post-framework copy** | `.cs-after-framework` | Narrow paragraph after grid. |
| **Stats** | `.cs-stat-grid`, `.cs-stat-card`, `.cs-stat-card--light`, `.cs-stat-overline`, `.cs-stat-num`, `.cs-stat-heading`, `.cs-stat-body`, `.cs-stat-wide`, `.cs-stat-wide-figure`, `.cs-stat-wide-text`, `.cs-stat-wide-unit` | 3-up grid + optional full-width row. |
| **Confidential closer** | `.cs-confidential-wrap`, `.cs-confidential-split`, `.cs-confidential-heading`, `.cs-confidential-lede`, `.cs-cta` | Split layout + email CTA (same pill idea as `.btn-navy`). |
| **Preview / list** | `.cs-preview-card`, `.cs-preview-label`, `.cs-preview-list` | Bulleted list with `→` pseudo-elements. |
| **Callout** | `.cs-callout`, `.cs-callout-icon`, `.cs-callout-title`, `.cs-callout-body` | Optional bordered callout (e.g. confidentiality note). |
| **Generic section** | `.cs-section`, `.cs-section-label`, `.cs-section-title`, `.cs-prose` | If you need a labeled section outside the bordered block pattern. |

---

## 9. Borders, radii, and imagery

- **Cards / quotes / stats** — `border-radius: 8px` is the default; callout and preview card use **12px**.
- **Cover frame** — `8px` radius, `1px solid var(--line)`, `background: var(--blush)`; image `object-fit: contain` so mockups don’t crop unexpectedly.
- **Pills** — Tags and buttons: **100px** radius.

---

## 10. Footer and behavior

- Reuse the same **`<footer>`** structure and classes as the home page / reference case study (`footer-copy`, etc. in `style.css`).
- **Nav theme script** — Keep scroll/resize listeners that toggle `nav.light` when the fixed nav overlaps the dark hero or footer so logo and links stay readable.

---

## 11. Accessibility patterns to preserve

- **`aria-labelledby`** on `<section>` pointing at the visible `h2` id.
- **`aria-label`** on meta `<aside>` (e.g. “Project details”).
- **`aria-hidden="true"`** on decorative numbering where it duplicates the heading.
- Meaningful **`alt`** on cover images; width/height on images when known to reduce layout shift.

---

## 12. Breakpoints (already in CSS)

- **768px** — Hero single column; meta border moves to top; `.cs-two-col`, `.cs-challenge-grid`, `.cs-framework-grid`, `.cs-stat-grid`, `.cs-stat-wide`, `.cs-confidential-split` → one column.
- **600px** — `.cs-callout` stacks vertically.

---

## 13. Checklist for a new case study file

1. `html.case-study` + `body.case-study`, correct relative paths to CSS and home anchors (`portfolio (6).html#work-n`, `#hero`, `#about`, `#contact`).
2. Nav + footer markup consistent with reference; nav script for `light` toggle.
3. Hero modifier matches the project’s home slide color.
4. Copy uses `.ws-*` in hero; body uses `.cs-body-shell` → `.cs-cover` (if needed) → `.cs-section-block` sections → optional `.cs-confidential-wrap`.
5. No new font families; use tokens for color and `--page-pad-x` for horizontal inset.
6. Images: prefer assets under `images/` with paths relative to the HTML file.

---

*Derived from `work/highspot-agent-center.html`, `case-study.css`, and `style.css` (home / work slides).*
