# Codrops Button Hover Styles — CSS Reference

Source: https://github.com/codrops/ButtonHoverStyles

## Base button reset

```css
.button {
  pointer-events: auto;
  cursor: pointer;
  background: #e7e7e7;
  border: none;
  padding: 1.5rem 3rem;
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  position: relative;
  display: inline-block;
}
.button::before,
.button::after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

---

## 01 · Pan — Pill fill slides up

**HTML:** `<button class="button button--pan"><span>Label</span></button>`

```css
.button--pan {
  font-weight: 700;
  border: 2px solid #000;
  border-radius: 3rem;
  overflow: hidden;
  color: #fff;
}
.button--pan span {
  position: relative;
  mix-blend-mode: difference;
}
.button--pan::before {
  content: '';
  background: #000;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--pan:hover::before {
  transform: translate3d(0, -100%, 0);
}
```

---

## 02 · Hyperion — Background wipe + text flicker

**HTML:** `<button class="button button--hyperion"><span><span>Label</span></span></button>`

```css
.button--hyperion {
  font-weight: 500;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  overflow: hidden;
  color: #fff;
}
.button--hyperion span { display: block; position: relative; }
.button--hyperion > span { overflow: hidden; }
.button--hyperion > span > span { overflow: hidden; mix-blend-mode: difference; }
.button--hyperion:hover > span > span {
  animation: MoveUpInitial 0.2s forwards, MoveUpEnd 0.2s forwards 0.2s;
}
@keyframes MoveUpInitial { to { transform: translate3d(0,-105%,0); } }
@keyframes MoveUpEnd {
  from { transform: translate3d(0,100%,0); }
  to   { transform: translate3d(0,0,0); }
}
.button--hyperion::before {
  content: '';
  background: #000;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
  transform-origin: 100% 50%;
}
.button--hyperion:hover::before {
  transform: scale3d(0, 1, 1);
  transform-origin: 0% 50%;
}
```

---

## 03 · Mimas — Skewed fill slides out

**HTML:** `<button class="button button--mimas"><span>Label</span></button>`

```css
.button--mimas {
  text-transform: uppercase;
  letter-spacing: 0.05rem;
  font-weight: 700;
  font-size: 0.85rem;
  border-radius: 0.5rem;
  overflow: hidden;
  color: #fff;
  background: #e7e7e7;
}
.button--mimas span { position: relative; mix-blend-mode: difference; }
.button--mimas::before {
  content: '';
  background: #000;
  width: 120%;
  left: -10%;
  transform: skew(30deg);
  transition: transform 0.4s cubic-bezier(0.3, 1, 0.8, 1);
}
.button--mimas:hover::before { transform: translate3d(100%, 0, 0); }
```

---

## 04 · Atlas — Marquee text on hover

**HTML:**
```html
<button class="button button--atlas">
  <span>Label</span>
  <div class="marquee" aria-hidden="true">
    <div class="marquee__inner">
      <span>Label</span><span>Label</span><span>Label</span><span>Label</span>
    </div>
  </div>
</button>
```

```css
.button--atlas > span { display: inline-block; }
.button--atlas:hover > span { opacity: 0; }
.marquee { position: absolute; top: 0; left: 0; width: 100%; overflow: hidden; pointer-events: none; }
.marquee__inner {
  width: fit-content;
  display: flex;
  position: relative;
  --offset: 1rem;
  --move-initial: calc(-25% + var(--offset));
  --move-final: calc(-50% + var(--offset));
  transform: translate3d(var(--move-initial), 0, 0);
  animation: marquee 1s linear infinite;
  animation-play-state: paused;
  opacity: 0;
}
.button--atlas:hover .marquee__inner {
  animation-play-state: running;
  opacity: 1;
  transition-duration: 0.4s;
}
.marquee span { text-align: center; white-space: nowrap; font-style: italic; padding: 1.5rem 0.5rem; }
@keyframes marquee {
  0%   { transform: translate3d(var(--move-initial), 0, 0); }
  100% { transform: translate3d(var(--move-final), 0, 0); }
}
```

---

## 05 · Kari — Circular button with marquee

Same marquee markup as Atlas. Add `class="button--kari"`.

```css
.button--kari {
  font-weight: 900;
  font-size: 1.25rem;
  border-radius: 50%;
  border: 2px solid #000;
}
.button--kari > span { display: inline-block; transition: opacity 0.1s; }
.button--kari:hover > span { opacity: 0; }
.button--kari .marquee { transform: rotate(-2.75deg); }
.button--kari:hover .marquee__inner { animation-play-state: running; opacity: 1; transition-duration: 0.6s; }
```

---

## 06 · Pandora — Offset shadow lift

**HTML:** `<button class="button button--pandora"><span>Label</span></button>`

```css
.button--pandora {
  background: #000;
  font-weight: 700;
  padding: 0;
  border-radius: 5px;
}
.button--pandora span {
  display: block;
  background: #a7a7a7;
  padding: 1.5rem 2rem;
  border: 1px solid #000;
  border-radius: 5px;
  transform: translate3d(-4px, -4px, 0);
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--pandora:hover span { transform: translate3d(-8px, -8px, 0); }
```

---

## 07 · Janus — Organic blob shape morph

**HTML:** `<button class="button button--janus"><span>Label</span></button>`

```css
.button--janus {
  font-weight: 900;
  width: 175px;
  height: 120px;
  color: #fff;
  background: none;
}
.button--janus::before {
  content: '';
  background: #e6e6e6;
  clip-path: path("M154.5,88.5 C131,113.5 62.5,110 30,89.5 C-2.5,69 -3.5,42 4.5,25.5 C12.5,9 33.5,-6 85,3.5 C136.5,13 178,63.5 154.5,88.5 Z");
  transition: clip-path 0.5s cubic-bezier(0.585, 2.5, 0.645, 0.55), background 0.5s ease;
}
.button--janus:hover::before {
  background: #000;
  clip-path: path("M143,77 C117,96 74,100.5 45.5,91.5 C17,82.5 -10.5,57 5.5,31.5 C21.5,6 79,-5.5 130.5,4 C182,13.5 169,58 143,77 Z");
}
.button--janus::after {
  content: '';
  height: 86%;
  width: 97%;
  top: 5%;
  border-radius: 58% 42% 55% 45% / 56% 45% 55% 44%;
  border: 1px solid #000;
  transform: rotate(-20deg);
  z-index: -1;
  transition: transform 0.5s cubic-bezier(0.585, 2.5, 0.645, 0.55);
}
.button--janus:hover::after { transform: translate3d(0, -5px, 0); }
.button--janus span { display: block; transition: transform 0.3s ease; mix-blend-mode: difference; }
.button--janus:hover span { transform: translate3d(0, -10px, 0); }
```

---

## 08 · Anthe — Arrow/chevron clip-path reveal

**HTML:** `<button class="button button--anthe"><span>Label</span></button>`

```css
.button--anthe { color: #fff; background: none; }
.button--anthe::before {
  content: '';
  background: #000;
  clip-path: polygon(0% 0%, 100% 0, 100% 50%, 100% 100%, 0% 100%);
  transition: clip-path 0.4s cubic-bezier(0.2, 1, 0.8, 1);
}
.button--anthe:hover::before {
  clip-path: polygon(0% 0%, 75% 0%, 100% 50%, 75% 100%, 0% 100%);
}
.button--anthe span {
  display: block;
  mix-blend-mode: difference;
  transition: transform 0.4s cubic-bezier(0.2, 1, 0.8, 1);
}
.button--anthe:hover span { transform: translate3d(-10px, 0, 0); }
```

---

## 09 · Pallene — Border to filled circle

**HTML:** `<button class="button button--pallene">Label</button>`

```css
.button--pallene {
  font-weight: 700;
  border-radius: 0.5rem;
  border: 2px solid #000;
  box-shadow: inset 0 0 0 0px #000;
  transition: border-radius 0.3s, box-shadow 0.3s, color 0.3s;
  transition-timing-function: cubic-bezier(0.7, 0, 0.2, 1);
}
.button--pallene:hover {
  color: #e7e7e7;
  border-radius: 50%;
  box-shadow: inset 0 0 0 40px #000;
  transition-delay: 0s, 0s, 0.2s;
}
```

---

## 10 · Telesto — Text flies right + pointed fill

**HTML:** `<button class="button button--telesto"><span><span>Label</span></span></button>`

```css
.button--telesto { overflow: hidden; font-weight: 800; font-style: italic; color: #fff; }
.button--telesto span { display: block; position: relative; z-index: 1; }
.button--telesto > span { overflow: hidden; mix-blend-mode: difference; }
.button--telesto:hover > span > span {
  animation: MoveRightInitial 0.1s forwards, MoveRightEnd 0.3s forwards 0.2s;
}
@keyframes MoveRightInitial { to { transform: translate3d(105%, 0, 0); } }
@keyframes MoveRightEnd {
  from { transform: translate3d(-100%, 0, 0); }
  to   { transform: translate3d(0, 0, 0); }
}
.button--telesto::before, .button--telesto::after { content: ''; background: #000; }
.button--telesto::before {
  width: 135%;
  clip-path: polygon(75% 0%, 100% 50%, 75% 100%, 0% 100%, 0% 0%);
  transform: translate3d(-100%, 0, 0);
}
.button--telesto:hover::before {
  transform: translate3d(0, 0, 0);
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--telesto::after {
  width: 105%;
  transform: translate3d(100%, 0, 0);
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--telesto:hover::after {
  transform: translate3d(0, 0, 0);
  transition: transform 0.01s 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
```

---

## 11 · Calypso — Circular fill expands from center

**HTML:** `<button class="button button--calypso"><span>Label</span></button>`

```css
.button--calypso { overflow: hidden; font-size: 1.15rem; border-radius: 0.85rem; color: #fff; }
.button--calypso span { display: block; position: relative; mix-blend-mode: difference; z-index: 10; }
.button--calypso:hover span {
  animation: MoveScaleUpInitial 0.3s forwards, MoveScaleUpEnd 0.3s forwards 0.3s;
}
@keyframes MoveScaleUpInitial {
  to { transform: translate3d(0,-105%,0) scale3d(1,2,1); opacity: 0; }
}
@keyframes MoveScaleUpEnd {
  from { transform: translate3d(0,100%,0) scale3d(1,2,1); opacity: 0; }
  to   { transform: translate3d(0,0,0); opacity: 1; }
}
.button--calypso::before {
  content: '';
  background: #000;
  width: 120%;
  height: 0;
  padding-bottom: 120%;
  top: -110%;
  left: -10%;
  border-radius: 50%;
  transform: translate3d(0,68%,0) scale3d(0,0,0);
}
.button--calypso:hover::before {
  transform: translate3d(0,0,0) scale3d(1,1,1);
  transition: transform 0.4s cubic-bezier(0.1, 0, 0.3, 1);
}
.button--calypso::after {
  content: '';
  background: #000;
  transform: translate3d(0,-100%,0);
  transition: transform 0.4s cubic-bezier(0.1, 0, 0.3, 1);
}
.button--calypso:hover::after {
  transform: translate3d(0,0,0);
  transition-duration: 0.05s;
  transition-delay: 0.4s;
  transition-timing-function: linear;
}
```

---

## 12 · Skoll — Round button, fill drops down

**HTML:** `<button class="button button--skoll"><span><span>Label</span></span></button>`

```css
.button--skoll {
  overflow: hidden; border-radius: 50%;
  color: #fff; width: 100px; height: 100px; padding: 0;
}
.button--skoll span { display: block; position: relative; }
.button--skoll > span { overflow: hidden; mix-blend-mode: difference; }
.button--skoll:hover > span > span {
  animation: MoveUpInitial 0.2s forwards, MoveUpEnd 0.2s forwards 0.2s;
}
.button--skoll::before {
  content: '';
  background: #000;
  width: 100%; height: 0; padding-bottom: 100%;
  border-radius: 50%;
  transform: translate3d(0,0,0);
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--skoll:hover::before { transform: translate3d(0,100%,0); }
```

---

## 13 · Greip — Triangle clip-path wipe

**HTML:** `<button class="button button--greip"><span><span>Label</span></span></button>`

```css
.button--greip { overflow: hidden; color: #fff; padding: 1rem 2rem; }
.button--greip span { display: block; position: relative; }
.button--greip > span { overflow: hidden; mix-blend-mode: difference; }
.button--greip:hover > span > span {
  animation: MoveUpInitial 0.2s forwards, MoveUpEnd 0.2s forwards 0.2s;
}
.button--greip::before {
  content: '';
  background: #000;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
  transition: clip-path 0.2s cubic-bezier(0.7, 0, 0.2, 1);
}
.button--greip:hover::before {
  transition-duration: 0.3s;
  clip-path: polygon(0 0, 100% 0, 0 0, 0% 100%);
}
```

---

## 14 · Dione — Double border reveal

**HTML:** `<button class="button button--dione"><span>Label</span></button>`

```css
.button--dione { background: none; font-style: italic; padding: 1.5rem 3rem; }
.button--dione span { display: inline-block; position: relative; color: #fff; }
.button--dione::before {
  content: '';
  background: #000;
  transition: transform 0.3s cubic-bezier(0.2,1,0.7,1);
}
.button--dione:hover::before { transform: scale3d(0.9, 0.8, 1); }
.button--dione::after {
  content: '';
  border: 1px solid #000;
  transition: transform 0.3s cubic-bezier(0.2,1,0.7,1);
  transform: scale3d(0.85, 0.65, 1);
}
.button--dione:hover::after { transform: scale3d(1,1,1); }
```

---

## 15 · Helene — Slot machine text + shadow lift

**HTML:** `<button class="button button--helene"><span><span>Label</span></span></button>`

```css
.button--helene {
  border-radius: 7px; border: 1px solid #000;
  font-weight: 900; text-transform: uppercase; font-size: 0.85rem;
  padding: 0 3rem; height: 4rem;
}
.button--helene::before {
  content: '';
  top: 10px; left: 10px;
  width: calc(100% - 20px); height: calc(100% - 20px);
  background: rgba(0,0,0,0.5);
  filter: blur(7px); border-radius: 7px; z-index: -1;
  transform: translate3d(0,15px,0);
  transition: transform 0.45s;
}
.button--helene:hover::before { transform: translate3d(0,0,0); }
.button--helene span { display: block; }
.button--helene > span { height: 100%; overflow: hidden; line-height: 4rem; }
.button--helene:hover > span > span { animation: slotMachine 0.15s ease-out forwards 3; }
@keyframes slotMachine {
  50%  { transform: translate3d(0,100%,0); opacity: 0; }
  51%  { transform: translate3d(0,-100%,0); opacity: 0; }
  100% { transform: translate3d(0,0,0); opacity: 1; }
}
```

---

## 16 · Rhea — Star/asterisk clip-path morph

**HTML:** `<button class="button button--rhea"><span>Label</span></button>`

```css
.button--rhea { font-weight: 900; width: 180px; height: 180px; color: #000; background: none; }
.button--rhea::before {
  content: ''; z-index: -1;
  background: #e7e7e7;
  clip-path: polygon(20% 30%, 0 30%, 0 50%, 0 70%, 20% 70%, 50% 70%, 80% 70%, 100% 70%, 100% 50%, 100% 30%, 80% 30%, 50% 30%);
  transition: clip-path 0.4s cubic-bezier(0.3, 1, 0.2, 1), transform 0.4s cubic-bezier(0.3, 1, 0.2, 1), background 0.4s ease;
}
.button--rhea:hover::before {
  background: #000;
  transform: scale3d(0.7, 0.7, 1);
  clip-path: polygon(30% 10%, 10% 30%, 30% 50%, 10% 70%, 30% 90%, 50% 70%, 70% 90%, 90% 70%, 70% 50%, 90% 30%, 70% 10%, 50% 30%);
}
.button--rhea span {
  display: block;
  transition: transform 0.4s cubic-bezier(0.3, 1, 0.2, 1), opacity 0.05s;
}
.button--rhea:hover span {
  transform: scale3d(0.1, 0.1, 1); opacity: 0;
  transition-delay: 0s, 0.35s;
}
```

---

## 17 · Narvi — Speech bubble shape

**HTML:** `<button class="button button--narvi"><span><span>Label</span></span></button>`

```css
.button--narvi { font-weight: bold; background: none; }
.button--narvi::before {
  content: ''; z-index: -1; background: #e7e7e7;
  clip-path: polygon(0% 0%, 100% 0%, 100% 70%, 85% 70%, 80% 70%, 75% 70%, 0 70%);
  transition: clip-path 0.3s cubic-bezier(0.7, 0, 0.2, 1), transform 0.3s ease;
}
.button--narvi:hover::before {
  transform: translate3d(0, -10px, 0);
  clip-path: polygon(0% 0%, 100% 0%, 100% 70%, 85% 70%, 86% 100%, 75% 70%, 0 70%);
}
.button--narvi > span {
  display: block; z-index: 1; overflow: hidden;
  transition: transform 0.3s;
  transform: translate3d(0, -0.556rem, 0);
}
.button--narvi:hover > span { transform: translate3d(0, -1.111rem, 0); }
.button--narvi:hover > span > span {
  animation: MoveUpInitial 0.15s forwards, MoveUpEnd 0.15s forwards 0.15s;
}
```

---

## 18 · Hati — Rotating texture pattern

**HTML:** `<button class="button button--hati"><span>Label</span></button>`

```css
.button--hati {
  border-radius: 50%; overflow: hidden; border: 2px solid;
  background: none; font-weight: 900; font-style: italic;
}
.button--hati::before {
  animation: rotateIt 10s linear infinite;
  background-image: url(/* small tile texture */);
  content: '';
  width: 300%; height: 300%; top: -100%; left: -100%;
  z-index: -1; opacity: 0; transform-origin: 50% 50%;
  transition: opacity 0.3s;
}
@keyframes rotateIt { to { transform: rotate(-360deg); } }
.button--hati:hover::before { opacity: 0.7; }
.button--hati span { display: block; position: relative; z-index: 1; }
```

---

## 19 · Bestia — Scale + radial fill

**HTML:** `<button class="button button--bestia"><div class="button__bg"></div><span>Label</span></button>`

```css
.button--bestia { font-size: 1.15rem; color: #fff; background: none; padding: 0; }
.button--bestia .button__bg {
  top: 0; left: 0; position: absolute;
  width: 100%; height: 100%;
  background: #e7e7e7; border-radius: 0.85rem; overflow: hidden;
  transition: transform 0.4s cubic-bezier(0.1, 0, 0.3, 1);
}
.button--bestia:hover .button__bg { transform: scale3d(1.2, 1.2, 1); }
.button--bestia .button__bg::before,
.button--bestia .button__bg::after { content: ''; position: absolute; background: #000; }
.button--bestia .button__bg::before {
  width: 110%; height: 0; padding-bottom: 110%;
  top: 50%; left: 50%; border-radius: 50%;
  transform: translate3d(-50%,-50%,0) scale3d(0,0,1);
}
.button--bestia:hover .button__bg::before {
  transition: transform 0.4s cubic-bezier(0.1, 0, 0.3, 1);
  transform: translate3d(-50%,-50%,0) scale3d(1,1,1);
}
.button--bestia .button__bg::after {
  top: 0; left: 0; width: 100%; height: 100%;
  opacity: 0; transition: opacity 0.1s 0.3s;
}
.button--bestia:hover .button__bg::after { opacity: 1; }
.button--bestia span { display: block; position: relative; mix-blend-mode: difference; z-index: 1; padding: 1.5rem 3rem; }
```

---

## 20 · Surtur — SVG circular text + eye icon

**HTML:** (complex SVG markup — see index.html)

Needs circular `<textPath>` SVG + an eye icon SVG.

```css
.button--surtur { border-radius: 50%; overflow: hidden; width: 170px; height: 170px; padding: 0; background: none; }
.textcircle { position: absolute; top: 0; left: 0; width: 100%; height: 100%; fill: none; }
.textcircle text { fill: #000; font-size: 0.65rem; letter-spacing: 0.3em; }
.eye { display: block; transition: transform 0.3s; }
.button--surtur:hover .eye { transform: scale(0.8); }
```

---

## 21 · Fenrir — Circular progress stroke on hover

**HTML:**
```html
<button class="button button--fenrir">
  <svg class="progress" width="70" height="70" viewbox="0 0 70 70">
    <path class="progress__circle" d="m35,2.5c17.96,0 32.5,14.54 32.5,32.5c0,17.96 -14.54,32.5 -32.5,32.5c-17.96,0 -32.5,-14.54 -32.5,-32.5c0,-17.96 14.54,-32.5 32.5,-32.5z"/>
    <path class="progress__path" d="m35,2.5c17.96,0 32.5,14.54 32.5,32.5c0,17.96 -14.54,32.5 -32.5,32.5c-17.96,0 -32.5,-14.54 -32.5,-32.5c0,-17.96 14.54,-32.5 32.5,-32.5z" pathLength="1"/>
  </svg>
  <span>Go</span>
</button>
```

```css
.button--fenrir { background: none; border-radius: 50%; width: 70px; height: 70px; padding: 0; }
.progress { position: absolute; top: 0; left: 0; }
.progress__circle { fill: none; stroke: #e7e7e7; stroke-width: 2; }
.progress__path {
  fill: none; stroke: #000; stroke-width: 2;
  stroke-dasharray: 1; stroke-dashoffset: 1;
  transition: stroke-dashoffset 0.5s cubic-bezier(0.7, 0, 0.3, 1);
}
.button--fenrir:hover .progress__path { stroke-dashoffset: 0; }
.button--fenrir span { display: block; position: relative; z-index: 1; }
```
