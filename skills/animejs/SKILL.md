---
name: animejs
description: >
  Anime.js 4.0 animation engine reference. Lightweight, modular, high-performance.
  Trigger: When building web animations, timelines, stagger effects, scroll animations, SVG morphing, text effects, or drag interactions with animejs.
metadata:
  author: juliangarnier
  version: "0.0.1"
---

## When to Use

Use this skill when:
- CSS property animations (transforms, colors, opacity)
- Sequenced animations with timelines
- Scroll-triggered or scroll-synced animations
- SVG morphing, line drawing, motion paths
- Text animations (split, scramble)
- Drag-and-drop with spring physics
- Responsive animations with media queries

Do NOT use for: physics simulations (Matter.js), Canvas/WebGL (Three.js), video/audio sync.

---

## Quick Decision

| Need | Function |
|------|----------|
| One-shot animation | `animate()` |
| Sequence orchestration | `createTimeline()` |
| Real-time updates (mouse/scroll) | `createAnimatable()` |
| Drag with physics | `createDraggable()` |
| Layout changes (FLIP) | `createLayout()` |
| Responsive/media queries | `createScope()` |
| Scroll-triggered | `onScroll()` |
| SVG morphing / drawing | `morphTo` / `createDrawable` |
| Text split/animate | `splitText()` |
| Staggered delays | `stagger()` |
| Spring physics | `createSpring()` |

---

## Installation

```bash
npm install animejs
```
```js
import { animate, createTimeline, stagger } from 'animejs';
// CDN: https://cdn.jsdelivr.net/npm/animejs/+esm
```

---

## animate() — Core

```js
animate(targets, params);
// Targets: CSS selector, DOM element, NodeList, JS object
animate('.box', { x: 100, duration: 800, ease: 'outExpo' });
```

### Properties & Values

```js
animate('.el', {
  // Transforms (GPU-accelerated)
  x: 100, y: 50, rotate: 90, scale: 1.5, skew: 15,
  // CSS
  opacity: 0.5, backgroundColor: '#ff0000',
  // Relative
  x: '+=50', x: '*=2',
  // Function-based
  delay: (el, i) => i * 100,
});
```

### Playback

```js
animate('.el', {
  x: 100, duration: 1000, delay: 500, ease: 'outExpo',
  loop: true, alternate: true, autoplay: true,
  onComplete: (anim) => {},
});
```

### Control

```js
const anim = animate('.el', { x: 100, autoplay: false });
anim.play(); anim.pause(); anim.reverse(); anim.restart();
anim.seek(500); anim.cancel(); anim.revert();
anim.progress; anim.duration; // properties
```

---

## createTimeline()

```js
const tl = createTimeline({ defaults: { duration: 500, ease: 'outExpo' } });
tl.add('.box', { x: 100 })
  .add('.circle', { y: 100 }, '-=200')  // overlap
  .add('.text', { opacity: 0 }, '<');     // same time
```

Positions: `500` (absolute), `'+=200'` (after), `'-=100'` (before), `'<'` (simultaneous), `'label'`

---

## onScroll() — Scroll

```js
import { animate, onScroll } from 'animejs';
animate('.el', {
  x: 200,
  autoplay: onScroll({ target: '.section', sync: true, repeat: true }),
});
```

---

## stagger()

```js
animate('.dots', { y: -20, delay: stagger(100) });
animate('.dots', { y: -20, delay: stagger(100, { from: 'center' }) });
animate('.dots', { scale: stagger([0.5, 1.5]) });  // value range
animate('.cell', { scale: [0,1], delay: stagger(50, { grid: [10,10], from: 'center' }) });
```

---

## SVG

```js
import { animate, morphTo, createDrawable, createMotionPath } from 'animejs';
animate('#a', { d: morphTo('#b'), duration: 1000 });           // morph
animate(createDrawable('path'), { draw: ['0 0','0 1'] });      // line draw
animate('.car', { ...createMotionPath('.road') });              // motion path
```

---

## Text

```js
import { splitText, animate, stagger, scrambleText } from 'animejs';
const { chars } = splitText('.heading', { chars: true });
animate(chars, { opacity: [0,1], y: [20,0], delay: stagger(30) });
animate('.el', { ...scrambleText({ text: 'New text', duration: 1000 }) });
```

---

## createDraggable()

```js
import { createDraggable, createSpring } from 'animejs';
createDraggable('.card', {
  container: '.board', snap: 100,
  releaseEase: createSpring({ stiffness: 200, damping: 20 }),
});
```

---

## createAnimatable() — Real-time

```js
import { createAnimatable } from 'animejs';
const box = createAnimatable('.box', { x: { duration: 500, ease: 'outSpring' } });
box.x(200);  // animate to
box.x();     // get current
```

---

## createScope() — Responsive

```js
import { createScope, createTimeline } from 'animejs';
createScope({ mediaQueries: { mobile: '(max-width: 768px)' } })
  .add(({ matches }) => {
    createTimeline().add('.nav', { x: matches.mobile ? ['-100%',0] : [0,0] });
  });
```

---

## Easings

```
'linear' 'ease'
'inSine' 'outSine' 'inOutSine'  'inQuad' 'outQuad' 'inOutQuad'
'inCubic' 'outCubic' 'inOutCubic'  'inExpo' 'outExpo' 'inOutExpo'
'inBack' 'outBack' 'inOutBack'  'inElastic' 'outElastic' 'inOutElastic'
'cubicBezier(.25,.1,.25,1)'  'steps(5)'  'spring(1,100,10,0)'  'outSpring'
```

---

## Common Patterns

```js
// Loop with alternate
animate('.box', { x: 250, duration: 800, ease: 'inOutExpo', loop: true, alternate: true });

// Timeline stagger
createTimeline()
  .add('.logo', { opacity: [0,1], y: [-20,0] })
  .add('.title', { opacity: [0,1], delay: stagger(50) }, '-=200');

// Scroll parallax
animate('.parallax', { y: ['-20%','20%'], autoplay: onScroll({ sync: true }) });

// Mouse tracking
const b = createAnimatable('.blob', { x: { duration: 800 }, y: { duration: 800 } });
document.addEventListener('mousemove', (e) => { b.x(e.clientX); b.y(e.clientY); });
```

---

## Hard Rules

1. Import only what you need — modular imports (~24KB total)
2. Use transforms (x, y, scale, rotate) — GPU-accelerated
3. Prefer timelines over nested callbacks
4. Clean up on unmount — call `revert()` or `cancel()`
5. Avoid animating layout — use transform/opacity, not width/height

---

## References

| Resource | URL |
|----------|-----|
| Official docs | https://animejs.com/documentation |
| Easings editor | https://animejs.com/easing-editor |
| GitHub | https://github.com/juliangarnier/anime |
| npm | https://www.npmjs.com/package/animejs |
| CodePen examples | https://codepen.io/collection/Poerqa |
