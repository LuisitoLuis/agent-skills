---
name: codrops-hover-styles
description: >
  Use this skill whenever the user wants to implement, reproduce, adapt, or get inspired by
  button hover animations or link underline hover effects from Codrops' ButtonHoverStyles
  or LineHoverStyles collections. Triggers include: "codrops button animation", "button hover
  effect like pan/hyperion/mimas/atlas/calypso/bestia/etc", "link hover underline animation",
  "CSS hover style for links", "slide-in underline", "marquee button", "clip-path button",
  "progress stroke button", "wavy underline SVG link", "scribble underline effect".
  Also trigger for requests like "CSS button hover animation", "subtle button effect",
  "link underline animation CSS", or "codrops hover" even without a specific name.
---

# Codrops Hover Styles Skill

This skill covers **21 CSS button hover styles** (ButtonHoverStyles) and **15 link underline
hover effects** (LineHoverStyles) from Codrops. All are CSS-only unless noted.

Sources:
- Buttons: https://github.com/codrops/ButtonHoverStyles
- Links: https://github.com/codrops/LineHoverStyles

---

## Workflow

1. **Identify** which style(s) the user wants — by name, number, or description.
2. **Read** the relevant reference file(s) for exact CSS.
3. **Adapt** to the user's colors/tokens/framework.
4. **Deliver** clean, ready-to-use HTML + CSS.

---

## Quick Reference

### Button Hover Styles (ButtonHoverStyles)

| # | Name | Effect summary | Key technique |
|---|------|---------------|---------------|
| 01 | **Pan** | Pill, fill slides up on hover | `translate3d` on `::before` |
| 02 | **Hyperion** | Bg wipe + text flies up & returns | `scale3d` wipe + `MoveUpInitial/End` animation |
| 03 | **Mimas** | Skewed fill slides out right | `skew` + `translate3d` on `::before` |
| 04 | **Atlas** | Marquee text replaces label | `marquee` keyframe, `animation-play-state` |
| 05 | **Kari** | Circular button, marquee rotated | Same as Atlas + `border-radius: 50%` |
| 06 | **Pandora** | Offset shadow lifts further | `translate3d` on inner `<span>` |
| 07 | **Janus** | Organic blob morphs + floats | `clip-path: path(...)` transition |
| 08 | **Anthe** | Arrow/chevron clip-path fill | `clip-path: polygon(...)` + text slides left |
| 09 | **Pallene** | Rounded rect fills to circle | `inset box-shadow` + `border-radius` |
| 10 | **Telesto** | Text flies right + pointed fill enters | Dual `::before/after` + `MoveRightInitial/End` |
| 11 | **Calypso** | Radial bubble expands from top | Circular `::before` + `scale3d(0→1)` |
| 12 | **Skoll** | Round button, fill drops down | `translate3d(0,100%)` on circle `::before` |
| 13 | **Greip** | Triangle clip wipes fill | `clip-path: polygon` collapses to triangle |
| 14 | **Dione** | Inner box shrinks, outer border expands | Dual `scale3d` on `::before` and `::after` |
| 15 | **Helene** | Slot-machine text spin + shadow lift | `slotMachine` keyframe + blur shadow |
| 16 | **Rhea** | Rect → star morphing blob | `clip-path: polygon` complex morph |
| 17 | **Narvi** | Speech bubble shape floats up | `clip-path` tail, text flicker |
| 18 | **Hati** | Circular, rotating texture reveals | Rotating tiled `background-image` |
| 19 | **Bestia** | Card scales + radial fill | Scale outer + inner `scale3d(0→1)` |
| 20 | **Surtur** | Circular SVG rotating text + eye | SVG `textPath` + eye icon |
| 21 | **Fenrir** | SVG circular progress stroke | `stroke-dashoffset` 1→0 |

### Link/Line Hover Styles (LineHoverStyles)

| # | Name | Effect summary | Key technique |
|---|------|---------------|---------------|
| 01 | **Metis** | Underline slides in left→right | `background-size` 0%→100% |
| 02 | **Io** | Underline wipes out right→left | `background-size` 100%→0% |
| 03 | **Thebe** | Underline expands from center | `background-position: 50%` |
| 04 | **Leda** | Underlined copy slides up from below | `translate3d` + `::after` w/ underline |
| 05 | **Ersa** | Strikethrough appears center | `scaleX` on `::before` at `top: 50%` |
| 06 | **Elara** | Background highlight fills from bottom | `scaleY` on `::before` |
| 07 | **Dia** | Underline + overline from opposite ends | Dual `background-image` gradients |
| 08 | **Kale** | Underline fills from both ends | Dual `::before/after` width 0→50% |
| 09 | **Carpo** | Underline slides in from left | `left: -100%` → `left: 0` on `::before` |
| 10 | **Helike** | Overline drops in from top | `scaleX` on top `::before` |
| 11 | **Mneme** | Thick gradient underline slides in | `background-size` with 3px line |
| 12 | **Iocaste** | SVG wavy path slides in | SVG `translate3d` 1/3 of 300% width |
| 13 | **Herse** | SVG arc draws on hover | `stroke-dashoffset: 1→0` |
| 14 | **Carme** | SVG scribble draws on hover | `stroke-dashoffset: 1→0` |
| 15 | **Eirene** | Background highlight slides in | `scaleX` fill from left |

---

## Reference Files

For full CSS of every style:

- **`references/button-styles.md`** — All 21 button styles with HTML markup + CSS
- **`references/line-styles.md`** — All 15 link underline styles with HTML markup + CSS

Always read the relevant reference before generating output — it contains exact keyframe
names, clip-path coordinates, and structural details that are critical to reproduce correctly.

---

## Usage Patterns

### Adapting colors to a design system

Replace `#000` / `#e7e7e7` / `#fff` with CSS custom properties:

```css
/* Example: adapt Hyperion to a brand system */
.button--hyperion { color: var(--color-text-inverse); }
.button--hyperion::before { background: var(--color-brand); }
```

### Adapting to Tailwind (arbitrary values)

Most effects rely on `::before`/`::after` pseudo-elements — Tailwind can't do this inline.
Write the animation CSS in a `<style>` block or a `.css` file, then apply the class.

### Using in React/Next.js

Import the CSS file globally or in a component:
```tsx
// global.css or component.module.css
import './button-hover-styles.css'

// Component
<button className="button button--calypso"><span>Click me</span></button>
```

### Combining with `mix-blend-mode: difference`

Several buttons (Pan, Hyperion, Mimas, Anthe, Skoll, Greip, Bestia) use
`mix-blend-mode: difference` on the text so it inverts against the fill.
This requires the parent to have a dark fill — it won't work on transparent backgrounds.

### SVG line styles (Iocaste, Herse, Carme)

These require inline SVG inside the `<a>`. The SVG uses `pathLength="1"` so
`stroke-dashoffset` can be used with normalized values (0→1) regardless of path length.

---

## Common Keyframe Animations (shared across buttons)

Define these once if using multiple button styles:

```css
@keyframes MoveUpInitial {
  to { transform: translate3d(0, -105%, 0); }
}
@keyframes MoveUpEnd {
  from { transform: translate3d(0, 100%, 0); }
  to   { transform: translate3d(0, 0, 0); }
}
@keyframes MoveRightInitial {
  to { transform: translate3d(105%, 0, 0); }
}
@keyframes MoveRightEnd {
  from { transform: translate3d(-100%, 0, 0); }
  to   { transform: translate3d(0, 0, 0); }
}
@keyframes MoveScaleUpInitial {
  to { transform: translate3d(0, -105%, 0) scale3d(1, 2, 1); opacity: 0; }
}
@keyframes MoveScaleUpEnd {
  from { transform: translate3d(0, 100%, 0) scale3d(1, 2, 1); opacity: 0; }
  to   { transform: translate3d(0, 0, 0); opacity: 1; }
}
@keyframes marquee {
  0%   { transform: translate3d(var(--move-initial), 0, 0); }
  100% { transform: translate3d(var(--move-final), 0, 0); }
}
```
