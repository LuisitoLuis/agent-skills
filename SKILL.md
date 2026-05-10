---
name: animejs-skill
description: "Trigger: animejs animation, anime.js, stagger, timeline, scroll animation. Anime.js reference for animations, timelines, stagger, scroll sync, SVG, and text effects."
license: MIT
metadata:
  author: juliangarnier
  version: "0.0.1"
---

# Anime.js — Skill Reference

> Lightweight, modular, high-performance JavaScript animation engine.
> Current version: **4.0.0** | Official docs: https://animejs.com/documentation

---

## Activation Contract

Use this skill when:
- Building web animations (CSS properties, transforms, colors) in vanilla JS or any framework
- Creating animation sequences with timelines
- Implementing scroll-triggered animations
- Animating SVG elements (morphing, drawing, motion paths)
- Text animations (split, scramble effects)
- Interactive animations (draggable, animatable)

Works with: Vanilla JS, React, Vue, Svelte, Next.js, Nuxt, or any DOM-based project.

Do NOT use this skill for:
- Complex physics simulations (use Matter.js or similar)
- Canvas/WebGL animations (use Three.js or Pixi.js)
- Video/audio sync (use native Web APIs)

---

## Decision Gates

| Need | Use |
|------|-----|
| Simple one-shot animation | `animate()` — Section 1 |
| Timers and time control | `createTimer()` — Section 2 |
| Orchestrate multiple animations | `createTimeline()` — Section 3 |
| Real-time updates (mouse, scroll) | `createAnimatable()` — Section 4 |
| Drag-and-drop with physics | `createDraggable()` — Section 5 |
| Layout changes (FLIP technique) | `createLayout()` — Section 6 |
| Responsive animations | `createScope()` — Section 7 |
| Scroll-triggered animations | `onScroll()` — Section 8 |
| SVG morphing | `morphTo` — Section 9 |
| SVG line drawing | `createDrawable` — Section 9 |
| SVG path following | `createMotionPath` — Section 9 |
| Text character/word animation | `splitText()` — Section 10 |
| Text scramble effect | `scrambleText()` — Section 10 |
| Staggered animations | `stagger()` — Section 11 |
| Physics springs | `createSpring()` — Section 12 |
| High-performance transforms | `waapi` — Section 14 |
| Global engine configuration | `engine` — Section 15 |

---

## Hard Rules

1. **Import only what you need** — Use modular imports to keep bundle size small (~24KB total)
2. **Use transforms over positioning** — Transform properties (x, y, scale, rotate) are GPU-accelerated
3. **Prefer timelines over nested callbacks** — `createTimeline()` is more readable than callback chains
4. **Use WAAPI for transforms/opacity only** — Use JS engine for colors, scroll sync, and callbacks
5. **Clean up after yourself** — Call `revert()` or `cancel()` on animations when components unmount
6. **Avoid animating layout properties** — Animate `transform` and `opacity`, not `width`/`height` directly

---

## Output Contract

When this skill is invoked, return:
- Relevant code snippets for the requested animation pattern
- Module imports needed for the feature
- Performance considerations if applicable
- Cleanup recommendations

---

## Installation

```bash
npm install animejs
```

```js
// ES Modules (bundler: Vite, esbuild, etc.)
import { animate, createTimeline, stagger } from 'animejs';

// CommonJS
const { animate } = require('animejs');

// CDN — ES Module
import { animate } from 'https://esm.sh/animejs';
// or JsDelivr
import { animate } from 'https://cdn.jsdelivr.net/npm/animejs/+esm';

// CDN — UMD (script tag)
// <script src="https://cdn.jsdelivr.net/npm/animejs/dist/bundles/anime.umd.min.js"></script>
// const { animate } = anime;
```

### Available distribution files

| File | Type |
|---|---|
| `dist/modules/index.js` | ES modules entry point |
| `dist/modules/index.cjs` | CommonJS entry point |
| `dist/bundles/anime.esm.min.js` | Minified ES bundle |
| `dist/bundles/anime.umd.min.js` | Minified UMD bundle |

### Bundle size (modular)

| Module | Size |
|---|---|
| Timer | 5.60 KB |
| Animation | +5.20 KB |
| Timeline | +0.55 KB |
| Animatable | +0.40 KB |
| Draggable | +6.41 KB |
| Scroll | +4.30 KB |
| Scope | +0.22 KB |
| SVG | 0.35 KB |
| Stagger | +0.48 KB |
| Spring | 0.52 KB |
| WAAPI | 3.50 KB |
| **Total** | **~24.50 KB** |

---

## Module imports

Only import what you need to keep the bundle small:

```js
import {
  animate,           // Main animation function
  createTimer,       // Timer without animated properties
  createTimeline,    // Animation sequencer
  createAnimatable,  // Real-time animatable properties
  createDraggable,   // Draggable elements
  createScope,       // Responsive scope
  createLayout,      // Automatic layout animations
  onScroll,          // Scroll Observer
  stagger,           // Staggering utility
  createSpring,      // Physics spring
  waapi,             // Enhanced Web Animation API
  utils,             // Math and DOM utilities

  // SVG
  morphTo,
  createDrawable,
  createMotionPath,

  // Text
  splitText,
  scrambleText,

  // Engine
  engine,
} from 'animejs';
```

---

## 1. animate() — Main animation function

```js
animate(targets, parameters);
```

### Targets

```js
// CSS Selector
animate('.box', { x: 100 });

// DOM Element
animate(document.querySelector('.box'), { x: 100 });

// NodeList / Array of elements
animate(document.querySelectorAll('.box'), { x: 100 });

// JavaScript Object
const obj = { value: 0 };
animate(obj, { value: 100, onUpdate: () => console.log(obj.value) });

// Mixed array
animate(['.box', myElement, myObject], { opacity: 0 });
```

### Animatable properties

```js
// CSS Properties
animate('.el', {
  width: '200px',
  backgroundColor: '#ff0000',
  opacity: 0.5,
  borderRadius: '50%',
});

// CSS Transforms (individual, no conflicts)
animate('.el', {
  x: 100,          // translateX
  y: 50,           // translateY
  z: 0,            // translateZ
  rotate: 90,      // rotateZ (degrees by default)
  rotateX: 45,
  rotateY: 45,
  scale: 1.5,
  scaleX: 2,
  scaleY: 0.5,
  skew: 15,
  skewX: 10,
  skewY: 10,
});

// CSS Variables
animate('.el', { '--my-color': '#ff0000' });

// HTML Attributes
animate('input[type=range]', { value: 50 });

// SVG Attributes
animate('circle', { r: 50, cx: 100, cy: 100 });

// JS Object properties
const data = { count: 0 };
animate(data, { count: 100 });
```

### Tween value types

```js
// Numerical
animate('.el', { x: 100 });

// With unit (automatic conversion)
animate('.el', { width: '50%' });  // converts from px
animate('.el', { x: '10rem' });

// Relative (JS only)
animate('.el', { x: '+=50' });   // add 50
animate('.el', { x: '-=50' });   // subtract 50
animate('.el', { x: '*=2' });    // multiply by 2

// Color
animate('.el', { backgroundColor: 'rgb(255, 0, 0)' });
animate('.el', { backgroundColor: '#ff0000' });
animate('.el', { backgroundColor: 'hsl(0, 100%, 50%)' });

// Color function (WAAPI)
animate('.el', { color: 'oklch(70% 0.2 120)' });

// CSS variable as value
animate('.el', { x: 'var(--offset)' });

// Function-based (per element)
animate('.el', {
  x: (el, index, total) => index * 50,
  delay: (el, index) => index * 100,
});
```

### Tween parameters (per property)

```js
animate('.el', {
  x: {
    to: 200,
    from: 0,          // forced initial value
    delay: 200,
    duration: 800,
    ease: 'inOutExpo',
    composition: 'add',  // 'replace' | 'add' | 'blend'
    modifier: v => Math.round(v),
  },
});
```

### Keyframes

```js
// Tween values keyframes (array of values)
animate('.el', {
  x: [0, 50, 100, 50, 0],
});

// Tween parameters keyframes
animate('.el', {
  x: [
    { to: 100, duration: 500, ease: 'outExpo' },
    { to: 0,   duration: 500, ease: 'inExpo'  },
  ],
});

// Duration-based keyframes (JS only)
animate('.el', {
  keyframes: [
    { x: 100, duration: 400 },
    { y: 50,  duration: 300 },
    { rotate: 90, duration: 500 },
  ],
});

// Percentage-based keyframes (JS only)
animate('.el', {
  keyframes: {
    '0%':   { x: 0,   opacity: 1 },
    '50%':  { x: 100, opacity: 0.5 },
    '100%': { x: 200, opacity: 1 },
  },
});
```

### Playback settings

```js
animate('.el', {
  x: 100,
  delay: 500,             // delay before starting (ms)
  duration: 1000,         // duration (ms)
  loop: true,             // true = infinite, number = repetitions
  loopDelay: 200,         // pause between loops (JS only)
  alternate: true,        // reverses direction on each loop
  reversed: false,        // plays in reverse
  autoplay: true,         // starts automatically
  frameRate: 60,          // max FPS (JS only)
  playbackRate: 1,        // speed (0.5 = half speed)
  playbackEase: 'linear', // global easing for the animation (JS only)
  persist: false,         // keeps styles after completion (WAAPI only)
});
```

### Callbacks

```js
animate('.el', {
  x: 100,
  onBegin:        (anim) => console.log('started'),       // JS only
  onComplete:     (anim) => console.log('complete'),
  onBeforeUpdate: (anim) => {},                           // JS only
  onUpdate:       (anim) => console.log(anim.progress),  // JS only
  onRender:       (anim) => {},                           // JS only
  onLoop:         (anim) => {},                           // JS only
  onPause:        (anim) => {},                           // JS only
}).then((anim) => console.log('promise resolved'));
```

### Animation methods

```js
const anim = animate('.el', { x: 100, autoplay: false });

anim.play();           // play
anim.pause();          // pause
anim.resume();         // resume
anim.reverse();        // reverse direction
anim.restart();        // restart from the beginning
anim.alternate();      // alternate direction
anim.complete();       // jump to end
anim.cancel();         // cancel without reverting
anim.revert();         // cancel and restore original values
anim.reset();          // reset to initial state (JS only)
anim.seek(500);        // jump to time in ms
anim.stretch(2000);    // stretch total duration (JS only)
anim.refresh();        // recompute values (JS only)
```

### Animation properties

```js
anim.duration    // total duration (ms)
anim.currentTime // current time (ms)
anim.progress    // progress 0-1
anim.paused      // boolean
anim.began       // boolean
anim.completed   // boolean
anim.reversed    // boolean
anim.targets     // array of targets
```

---

## 2. createTimer() — Timer

Pure timer without animated properties, useful for orchestrating timing logic.

```js
import { createTimer } from 'animejs';

const timer = createTimer({
  duration: 2000,
  loop: true,
  onUpdate: (t) => console.log(t.currentTime),
  onComplete: (t) => console.log('done'),
});
```

Supports the same **playback settings**, **callbacks**, and **methods** as `animate()`.

---

## 3. createTimeline() — Timeline

Orchestrates animation sequences with precise time control.

```js
import { createTimeline } from 'animejs';

const tl = createTimeline({
  loop: true,
  defaults: { duration: 500, ease: 'outExpo' }, // defaults for all animations
});

// Add animations (chained in sequence by default)
tl.add('.box',    { x: 100 })
  .add('.circle', { y: 100 })
  .add('.text',   { opacity: 0 });
```

### Time positions

```js
tl.add('.el', { x: 100 })              // after the previous
  .add('.el', { y: 50 }, 500)          // absolute: at 500ms from start
  .add('.el', { scale: 2 }, '+=200')   // relative: 200ms AFTER the previous ends
  .add('.el', { rotate: 90 }, '-=100') // relative: 100ms BEFORE the previous ends
  .add('.el', { opacity: 0 }, '<')     // at the same time as the previous
  .add('.el', { opacity: 1 }, '<100')  // 100ms after the start of the previous
  .label('myLabel')                    // label at current time
  .add('.el', { x: 0 }, 'myLabel');    // position by label
```

### Timeline methods

```js
tl.add(targets, params, position)  // add animation
  .set(targets, params, position)  // set values instantly
  .sync(animation, position)       // sync external animation
  .call(fn, position)              // call function at a specific time
  .label('name', position)         // add label
  .remove(targets)                 // remove animations for targets
  .init()                          // initialize without playing

// Playback (same as animate)
tl.play() .pause() .resume() .reverse()
  .restart() .alternate() .complete()
  .cancel() .revert() .reset()
  .seek(ms) .stretch(ms) .refresh()
```

---

## 4. createAnimatable() — Animatable

Imperatively animate properties in real time (ideal for mouse interactions, smooth scroll, etc.).

```js
import { createAnimatable } from 'animejs';

const box = createAnimatable('.box', {
  x: { duration: 500, ease: 'outSpring' },
  y: { duration: 500, ease: 'outSpring' },
  scale: { duration: 300 },
  // unit: 'px',       // default unit
  // modifier: v => v, // global modifier
});

// Setter: animates to the new value
box.x(200);
box.y(100);
box.scale(1.5);

// Getter: returns current value
console.log(box.x()); // null if not yet set

// Revert
box.revert();
```

---

## 5. createDraggable() — Draggable

Makes elements draggable with spring physics and snapping.

```js
import { createDraggable, createSpring } from 'animejs';

const draggable = createDraggable('.card', {
  // Axis constraints
  x: true,        // allow drag on X
  y: false,       // lock Y axis
  // x: { mapTo: anotherElement }, // map position to another element

  // Container and bounds
  container: '.wrapper',    // selector, element, 'window', or 'parent'
  containerPadding: 20,     // inner padding of the container
  containerFriction: 0.8,   // friction when dragged outside the container

  // Snap
  snap: 50,                 // number, array, or function
  // snap: [0, 100, 200, 300],
  // snap: (val) => Math.round(val / 50) * 50,

  // Release physics
  releaseEase: createSpring({ stiffness: 200, damping: 15 }),
  releaseMass: 1,
  releaseStiffness: 200,
  releaseDamping: 15,
  releaseContainerFriction: 0.85,

  // Velocity
  velocityMultiplier: 1,
  minVelocity: 0,
  maxVelocity: Infinity,
  dragSpeed: 1,
  dragThreshold: 0,   // min pixels to start dragging

  // Auto-scroll
  scrollThreshold: 20,
  scrollSpeed: 10,

  // Cursor
  cursor: 'grab',         // CSS cursor on hover
  trigger: '.handle',     // element that triggers the drag

  // Callbacks
  onGrab:        (d) => {},
  onDrag:        (d) => {},
  onUpdate:      (d) => {},
  onRelease:     (d) => {},
  onSnap:        (d) => {},
  onSettle:      (d) => {},
  onResize:      (d) => {},
  onAfterResize: (d) => {},
});

// Methods
draggable.enable();
draggable.disable();
draggable.setX(100);
draggable.setY(50);
draggable.animateInView();
draggable.scrollInView();
draggable.stop();
draggable.reset();
draggable.revert();
draggable.refresh();
```

---

## 6. createLayout() — Layout Animations

Automatically animates layout changes using the FLIP technique (First, Last, Invert, Play).

```js
import { createLayout } from 'animejs';

const layout = createLayout('.container', {
  children: true,    // animate container children
  duration: 600,
  ease: 'outExpo',
  properties: ['width', 'height', 'transform', 'opacity'],

  // Enter/exit states
  enterFrom: { opacity: 0, scale: 0.5 },
  leaveTo:   { opacity: 0, scale: 0.5 },
  swapAt:    0.5,  // swap point (0-1)
});

// Typical usage
layout.record();         // capture current positions
// ... make DOM changes ...
layout.animate();        // animate from previous position to new one

// Or combined:
layout.update(() => {
  // DOM changes here
});

layout.revert();         // revert animation
```

### Using data-layout-id

```html
<!-- Elements with the same layout-id are tracked across containers -->
<div data-layout-id="card-1" class="container-a">Card</div>
<!-- After moving to the other container: -->
<div data-layout-id="card-1" class="container-b">Card</div>
```

### Layout use cases

```js
// CSS display property animation
// DOM reorder animation
// Enter / Exit animations
// Modal dialog animations
// Swap parent animations (element moves between parent containers)
```

---

## 7. createScope() — Scope

Groups animations with shared defaults and media query support for responsive animations.

```js
import { createScope } from 'animejs';

const scope = createScope({
  root: '.my-component',          // root element (selector context)
  defaults: { duration: 600, ease: 'outExpo' },
  mediaQueries: {
    mobile:   '(max-width: 768px)',
    portrait: '(orientation: portrait)',
    dark:     '(prefers-color-scheme: dark)',
  },
});

// add() re-runs whenever a media query changes
scope.add(({ matches, root }) => {
  const isMobile = matches.mobile;

  createTimeline()
    .add('.box', {
      x: isMobile ? 0 : 200,
      y: isMobile ? 100 : 0,
    });

  // Optionally return a cleanup function
  return () => {};
});

// addOnce() runs only once (does not re-run on media query change)
scope.addOnce(() => {
  animate('.logo', { opacity: 1, delay: 500 });
});

scope.revert();   // cleans up all animations in the scope
scope.refresh();  // re-runs all constructors
scope.keepTime(); // preserves time when refreshing
```

---

## 8. onScroll() — Scroll Observer

Synchronizes and triggers animations based on scroll position.

```js
import { animate, onScroll } from 'animejs';

// As the autoplay value of an animation
animate('.el', {
  x: 200,
  autoplay: onScroll(),
});

// Full configuration
animate('.section', {
  opacity: [0, 1],
  autoplay: onScroll({
    container: window,        // scroll container
    target: '.section',       // observed element (defaults to animation target)
    axis: 'y',                // 'x' | 'y'
    debug: false,             // shows visual markers

    // Thresholds: when the element enters/leaves
    // Shorthand: 'top bottom' = when top of element hits bottom of viewport
    enter: 'bottom top',      // enters when scrolling down
    leave: 'top bottom',      // leaves when scrolling

    // Numeric values (0-1 relative to viewport)
    enter: 0.5,               // at the viewport midpoint
    // Relative values
    enter: '50% 100%',        // 50% of the element at 100% of the container

    repeat: true,             // repeats the animation each time

    // Synchronisation modes
    sync: true,               // syncs progress with scroll
    sync: 'play',             // calls play() on enter
    sync: 'restart',          // calls restart() on enter
    sync: 'resume',           // calls resume() on enter

    // Callbacks
    onEnter:         (obs) => {},
    onEnterForward:  (obs) => {},
    onEnterBackward: (obs) => {},
    onLeave:         (obs) => {},
    onLeaveForward:  (obs) => {},
    onLeaveBackward: (obs) => {},
    onUpdate:        (obs) => {},
    onSyncComplete:  (obs) => {},
    onResize:        (obs) => {},
  }),
});
```

### ScrollObserver methods

```js
const obs = onScroll({ target: '.el' });
obs.link(anim);    // link an animation
obs.refresh();     // recompute thresholds
obs.revert();      // destroy the observer
```

---

## 9. SVG — Utilities

```js
import { animate, morphTo, createDrawable, createMotionPath } from 'animejs';

// morphTo — SVG shape morphing
animate('#shape-a', {
  d: morphTo('#shape-b'),         // morph to another element's path
  duration: 1000,
  ease: 'inOutQuad',
});

// createDrawable — SVG line drawing animation
const drawable = createDrawable('path');
animate(drawable, {
  draw: '0 1',       // from start to end of stroke
  // draw: ['0 0', '0 1', '1 1'],  // keyframes
  duration: 1500,
  ease: 'inOutSine',
});
// draw: [start, end] where start and end are 0-1

// createMotionPath — Follow an SVG path
animate('.car', {
  ...createMotionPath('.road'),   // spreads x, y, rotate properties
  duration: 3000,
  ease: 'linear',
});
```

---

## 10. Text — Text utilities

### splitText()

Splits text into lines, words, and/or characters to animate them individually.

```js
import { splitText, animate, stagger } from 'animejs';

const splitter = splitText('.heading', {
  lines: true,
  words: true,
  chars: true,
  includeSpaces: false,
  debug: false,
  accessible: true, // aria-hidden on spans, aria-label on parent
});

// Animate characters
animate(splitter.chars, {
  opacity: [0, 1],
  y: [20, 0],
  delay: stagger(30),
  duration: 600,
  ease: 'outExpo',
});

// Animate words
animate(splitter.words, {
  scale: [0.8, 1],
  delay: stagger(50),
});

// Available properties
splitter.lines   // array of line elements
splitter.words   // array of word elements
splitter.chars   // array of character elements

// Methods
splitter.addEffect((el) => {
  // custom effect logic
});
splitter.refresh();  // recompute after resize
splitter.revert();   // restore original HTML
```

#### Split parameters

```js
splitText('.el', {
  lines: { class: 'my-line', wrap: '.wrapper', clone: false },
  words: { class: 'my-word' },
  chars: { class: 'my-char' },
});
```

### scrambleText() (NEW)

Scramble effect that randomly shuffles characters while revealing the target text.

```js
import { animate, scrambleText } from 'animejs';

animate('.heading', {
  ...scrambleText({
    text: 'New text',                    // destination text
    chars: 'abcdefghijklmnopqrstuvwxyz', // scramble character set
    override: false,                     // overwrite current text
    ease: 'linear',
    cursor: true,                        // show cursor at the end
    revealRate: 0.5,
    revealDelay: 0,
    settleRate: 0.5,
    settleDuration: 1000,
    delay: 0,
    duration: 1000,
    perturbation: 1,
    from: 'start',                       // 'start' | 'end' | 'center' | number
    reversed: false,
    seed: 0,
    onChange: (val, target) => {},
  }),
});
```

---

## 11. stagger() — Staggering

Creates staggered delays or values across multiple elements.

```js
import { animate, stagger } from 'animejs';

// Time staggering (delay per index)
animate('.dots', {
  y: -20,
  delay: stagger(100),                     // 0, 100, 200, 300...
  delay: stagger(100, { start: 200 }),     // 200, 300, 400...
  delay: stagger(100, { from: 'center' }), // from the center outward
  delay: stagger(100, { from: 2 }),        // from index 2
  delay: stagger(100, { reversed: true }), // reversed
  delay: stagger(100, { ease: 'inOutQuad' }), // with easing
});

// Value staggering (range between first and last element)
animate('.dots', {
  scale: stagger([0.5, 1.5]),       // from 0.5 to 1.5
  x: stagger(['-100px', '100px']),
});

// 2D Grid staggering
animate('.grid-item', {
  scale: stagger(0.1, {
    grid: [10, 10],       // columns x rows
    from: 'center',       // origin point
    axis: 'x',            // 'x' | 'y' | undefined (diagonal)
  }),
});

// Timeline staggering (time positions)
createTimeline()
  .add('.el', { y: -10 }, stagger(50));  // each element offset by +50ms

// Full parameters
stagger(value, {
  start: 0,         // start value or time
  from: 'first',    // 'first'|'center'|'last'|'edges'|index|[col,row]
  reversed: false,
  ease: 'linear',
  grid: [cols, rows],
  axis: 'x',        // 'x'|'y'
  modifier: (v) => v,
  use: 'delay',     // property to stagger
  total: undefined, // forced total element count
});
```

---

## 12. Easings — Easing functions

### Built-in eases

```js
// Syntax: 'type(exponent)'
'linear'
'ease'          // CSS alias

// In / Out / InOut — 3 forms:
'in(n)'         // inSine ~ in(1.675)
'out(n)'
'inOut(n)'

// Predefined aliases (shortcuts)
'inSine'    'outSine'    'inOutSine'
'inQuad'    'outQuad'    'inOutQuad'
'inCubic'   'outCubic'   'inOutCubic'
'inQuart'   'outQuart'   'inOutQuart'
'inQuint'   'outQuint'   'inOutQuint'
'inExpo'    'outExpo'    'inOutExpo'
'inCirc'    'outCirc'    'inOutCirc'
'inBack'    'outBack'    'inOutBack'
'inBounce'  'outBounce'  'inOutBounce'
'inElastic' 'outElastic' 'inOutElastic'
```

### Cubic Bezier

```js
// cubicBezier(x1, y1, x2, y2)
ease: 'cubicBezier(0.25, 0.1, 0.25, 1.0)'
// or using createCubicBezier:
import { createCubicBezier } from 'animejs';
ease: createCubicBezier(0.25, 0.1, 0.25, 1.0)
```

### Linear (multi-point)

```js
// linear([p1, p2, p3, ...]) — values between 0 and 1
ease: 'linear(0, 0.5, 1)'
ease: 'linear(0, 0.2 25%, 0.8 75%, 1)'
```

### Steps

```js
// steps(n, direction)
ease: 'steps(5)'
ease: 'steps(5, start)'  // 'start'|'end'|'both'|'none'
```

### Irregular (Custom)

```js
import { createIrregular } from 'animejs';
ease: createIrregular(/* seed, amplitude, frequency */);
```

### Spring

```js
import { createSpring } from 'animejs';

ease: createSpring({
  mass:      1,      // object mass
  stiffness: 100,    // spring stiffness
  damping:   10,     // damping coefficient
  velocity:  0,      // initial velocity
});

// or shorthand string
ease: 'spring(mass, stiffness, damping, velocity)'
ease: 'spring(1, 100, 10, 0)'

// outSpring (damped, comes to rest)
ease: 'outSpring'
ease: 'outSpring(stiffness, damping)'
```

---

## 13. Utilities

```js
import {
  $, get, set, cleanInlineStyles, remove, sync, keepTime,
  random, createSeededRandom, randomPick, shuffle,
  round, clamp, snap, wrap, mapRange, lerp, damp,
  roundPad, padStart, padEnd, degToRad, radToDeg,
  utils,
} from 'animejs';

// DOM
$('.selector')                // querySelectorAll -> array
get(target, 'x')              // get the current value of a property
set(target, { x: 100 })       // set value instantly
cleanInlineStyles(target)     // remove inline styles left by animations
remove(target)                // remove target from all active animations
sync(fn)                      // run fn on the next engine frame
keepTime(timer)               // preserve timer time on revert

// Numbers
random(0, 100)                // random number between min and max
random(0, 100, 2)             // with decimal places
createSeededRandom(seed)      // reproducible random generator -> fn()
randomPick([a, b, c])         // pick a random element from an array
shuffle([1, 2, 3, 4])         // shuffle array in place (mutates)

round(3.1415, 2)              // -> 3.14
clamp(value, min, max)        // clamp value to range
snap(value, increment)        // round to nearest increment
snap(value, [0,50,100])       // round to nearest value in array
wrap(value, min, max)         // wrap value within range (modulo)
mapRange(value, inMin, inMax, outMin, outMax)  // remap a value between ranges
lerp(a, b, t)                 // linear interpolation
damp(current, target, lambda, dt)  // smooth damp (frame-rate independent)

roundPad(value, decimals)     // round with trailing zeros: 1.5 -> "1.50"
padStart(str, length, char)   // pad left
padEnd(str, length, char)     // pad right

degToRad(180)                 // -> Math.PI
radToDeg(Math.PI)             // -> 180

// Chain-able utilities
utils(value)
  .round(2)
  .clamp(0, 100)
  .mapRange(0, 100, 0, 1)
  .get()  // get final value
```

---

## 14. WAAPI — Enhanced Web Animation API

Uses browser hardware acceleration for transforms and opacity.

```js
import { waapi } from 'animejs';

// waapi.animate() — same API as animate() but uses WAAPI internally
waapi.animate('.box', {
  x: 200,
  opacity: 0,
  duration: 1000,
  ease: 'outExpo',
});

// Improvements over native WAAPI:
// - Sensible defaults
// - Multi-target support
// - Automatic units (no explicit 'px' needed)
// - Function-based values
// - Individual CSS transforms (x, y, rotate, scale...)
// - Per-property parameters
// - Spring and custom easings

// API differences vs native WAAPI:
// loop        -> iterations
// alternate   -> direction: 'alternate'
// ease        -> easing
// .then()     -> .finished

// Convert anime.js easing to WAAPI format
const easing = waapi.convertEase('outElastic(1, .5)');
// -> CustomEffect function for use in native WAAPI
```

### When to use WAAPI vs JS engine

| Use WAAPI when... | Use JS engine when... |
|---|---|
| Only transforms and opacity | Color animations |
| Maximum performance matters | JS objects / custom properties |
| You don't need JS callbacks | You need precise onUpdate |
| GPU-accelerated properties | Layout / scroll sync |

---

## 15. Engine — Global engine

```js
import { engine } from 'animejs';

// Parameters (configure the global engine)
engine.timeUnit = 'ms';              // 'ms' | 's' — time unit (ms by default)
engine.speed = 1;                    // global speed multiplier
engine.fps = 60;                     // global max FPS
engine.precision = 4;                // decimal precision
engine.pauseOnDocumentHidden = true; // pause when the tab is hidden

// Methods
engine.update();   // manually advance the engine (manual mode)
engine.pause();    // pause all timers/animations
engine.resume();   // resume the engine

// Properties
engine.currentTime   // current engine time
engine.paused        // boolean

// Defaults — global default values
engine.defaults.duration = 400;
engine.defaults.ease = 'outQuad';
// ... any animation/playback parameter
```

---

## Common usage patterns

### Basic animation

```js
import { animate } from 'animejs';

animate('.box', {
  x: 250,
  duration: 800,
  ease: 'inOutExpo',
  loop: true,
  alternate: true,
});
```

### Timeline sequence

```js
import { createTimeline, stagger } from 'animejs';

createTimeline({ loop: true })
  .add('.logo',  { opacity: [0,1], y: [-20,0], duration: 600 })
  .add('.title', { opacity: [0,1], x: [-30,0], delay: stagger(50) })
  .add('.cta',   { scale: [0.8,1], opacity: [0,1] }, '-=200');
```

### Scroll-synced animation

```js
import { animate, onScroll } from 'animejs';

animate('.parallax', {
  y: ['-20%', '20%'],
  ease: 'linear',
  autoplay: onScroll({ sync: true }),
});
```

### Text animation

```js
import { splitText, animate, stagger } from 'animejs';

const { chars } = splitText('.hero-title', { chars: true });

animate(chars, {
  opacity: [0, 1],
  y: [30, 0],
  rotateX: [-90, 0],
  delay: stagger(40, { from: 'center' }),
  duration: 700,
  ease: 'outBack',
});
```

### SVG line drawing on scroll

```js
import { animate, createDrawable, onScroll, stagger } from 'animejs';

animate(createDrawable('path'), {
  draw: ['0 0', '0 1'],
  delay: stagger(40),
  ease: 'inOut(3)',
  autoplay: onScroll({ sync: true }),
});
```

### Draggable with spring

```js
import { createDraggable, createSpring } from 'animejs';

createDraggable('.card', {
  container: '.board',
  snap: 100,
  releaseEase: createSpring({ stiffness: 200, damping: 20 }),
});
```

### Responsive scope

```js
import { createScope, createTimeline, stagger } from 'animejs';

createScope({
  mediaQueries: { mobile: '(max-width: 768px)' },
}).add(({ matches }) => {
  createTimeline()
    .add('.nav-item', {
      x: matches.mobile ? ['-100%', 0] : [0, 0],
      y: matches.mobile ? 0 : [-20, 0],
      delay: stagger(60),
    });
});
```

### 2D grid stagger

```js
import { animate, stagger } from 'animejs';

animate('.cell', {
  scale: [0, 1],
  delay: stagger(50, {
    grid: [10, 10],
    from: 'center',
  }),
  duration: 600,
  ease: 'outBack',
});
```

### Animatable for mouse tracking

```js
import { createAnimatable } from 'animejs';

const blob = createAnimatable('.blob', {
  x: { duration: 800, ease: 'outExpo' },
  y: { duration: 800, ease: 'outExpo' },
});

document.addEventListener('mousemove', (e) => {
  blob.x(e.clientX - 50);
  blob.y(e.clientY - 50);
});
```

---

## Quick reference: tween composition

| Value | Behaviour |
|---|---|
| `'replace'` (default) | Replaces the current animation |
| `'add'` | Adds to the current value (accumulates) |
| `'blend'` | Smoothly blends with the current animation |

```js
// Blend composition for interactive transforms
animate('.el', {
  x: mouseX,
  composition: 'blend',
});
```

## See also

- **react-19** — React animations with Anime.js
- **frontend-design** — UI animations and micro-interactions
- **javascript** — Using Anime.js with vanilla JavaScript

---

## References

| Resource | URL |
|---|---|
| Official documentation | https://animejs.com/documentation |
| Easings editor | https://animejs.com/easing-editor |
| CodePen examples | https://codepen.io/collection/Poerqa |
| GitHub | https://github.com/juliangarnier/anime |
| npm | https://www.npmjs.com/package/animejs |

---