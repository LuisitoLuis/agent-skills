# Codrops Line Hover Styles for Links — CSS Reference

Source: https://github.com/codrops/LineHoverStyles

## Base link reset

```css
.link {
  cursor: pointer;
  text-decoration: none;
  white-space: nowrap;
  color: inherit;
}
```

---

## 01 · Metis — Simple slide-in underline

**HTML:** `<a href="#" class="link link--metis">Label</a>`

```css
.link--metis {
  background-image: linear-gradient(#000, #000);
  background-size: 0% 1px;
  background-position: 100% 100%;
  background-repeat: no-repeat;
  transition: background-size 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--metis:hover {
  background-size: 100% 1px;
  background-position: 0% 100%;
}
```

---

## 02 · Io — Underline wipes right to left

**HTML:** `<a href="#" class="link link--io">Label</a>`

```css
.link--io {
  background-image: linear-gradient(#000, #000);
  background-size: 100% 1px;
  background-position: 0% 100%;
  background-repeat: no-repeat;
  transition: background-size 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--io:hover {
  background-size: 0% 1px;
  background-position: 100% 100%;
}
```

---

## 03 · Thebe — Center-outward underline expand

**HTML:** `<a href="#" class="link link--thebe">Label</a>`

```css
.link--thebe {
  background-image: linear-gradient(#000, #000);
  background-size: 0% 1px;
  background-position: 50% 100%;
  background-repeat: no-repeat;
  transition: background-size 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--thebe:hover {
  background-size: 100% 1px;
}
```

---

## 04 · Leda — Duplicate text, offset reveal

**HTML:**
```html
<a href="#" class="link link--leda" data-text="Your Text">
  <span>Your Text</span>
</a>
```

```css
.link--leda { position: relative; overflow: hidden; padding-bottom: 2px; }
.link--leda span {
  display: block;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--leda::after {
  content: attr(data-text);
  position: absolute;
  bottom: 0; left: 0;
  height: 100%;
  transform: translate3d(0, 100%, 0);
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
  text-decoration: underline;
}
.link--leda:hover span { transform: translate3d(0, -100%, 0); }
.link--leda:hover::after { transform: translate3d(0, 0, 0); }
```

---

## 05 · Ersa — Strikethrough on hover

**HTML:** `<a href="#" class="link link--ersa"><span>Label</span></a>`

```css
.link--ersa { position: relative; }
.link--ersa::before {
  content: '';
  position: absolute;
  top: 50%; left: 0;
  width: 100%; height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: 100% 50%;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--ersa:hover::before {
  transform: scaleX(1);
  transform-origin: 0% 50%;
}
```

---

## 06 · Elara — Thick highlight fills behind text

**HTML:** `<a href="#" class="link link--elara"><span>Label</span></a>`

```css
.link--elara { position: relative; color: #000; }
.link--elara::before {
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 100%; height: 100%;
  background: currentColor;
  opacity: 0.1;
  transform: scaleY(0.1);
  transform-origin: 0% 100%;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--elara:hover::before { transform: scaleY(1); }
```

---

## 07 · Dia — Underline from left, overline from right

**HTML:** `<a href="#" class="link link--dia">Label</a>`

```css
.link--dia {
  background-image:
    linear-gradient(#000, #000),
    linear-gradient(#000, #000);
  background-size: 0% 1px, 0% 1px;
  background-position: 0% 100%, 100% 0%;
  background-repeat: no-repeat;
  transition: background-size 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--dia:hover {
  background-size: 100% 1px, 100% 1px;
}
```

---

## 08 · Kale — Bold bracket underline

**HTML:** `<a href="#" class="link link--kale">Label</a>`

```css
.link--kale {
  position: relative;
  padding-bottom: 4px;
}
.link--kale::before, .link--kale::after {
  content: '';
  position: absolute;
  bottom: 0;
  height: 2px;
  background: currentColor;
  width: 0;
  transition: width 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--kale::before { left: 0; }
.link--kale::after { right: 0; transition-delay: 0.1s; }
.link--kale:hover::before, .link--kale:hover::after { width: 50%; }
```

---

## 09 · Carpo — Underline that flips color

**HTML:** `<a href="#" class="link link--carpo">Label</a>`

```css
.link--carpo {
  position: relative;
  overflow: hidden;
  padding-bottom: 2px;
}
.link--carpo::before {
  content: '';
  position: absolute;
  bottom: 0; left: -100%;
  width: 100%; height: 1px;
  background: currentColor;
  transition: left 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--carpo:hover::before { left: 0; }
```

---

## 10 · Helike — Overline drops in from top

**HTML:** `<a href="#" class="link link--helike"><span>Label</span></a>`

```css
.link--helike { position: relative; }
.link--helike::before {
  content: '';
  position: absolute;
  top: -2px; left: 0;
  width: 100%; height: 1px;
  background: currentColor;
  transform: scaleX(0);
  transform-origin: 100% 0%;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--helike:hover::before {
  transform: scaleX(1);
  transform-origin: 0% 0%;
}
```

---

## 11 · Mneme — Thick gradient underline slide

**HTML:** `<a href="#" class="link link--mneme">Label</a>`

```css
.link--mneme {
  background-image: linear-gradient(to right, #000 0%, #000 100%);
  background-size: 0% 3px;
  background-position: 0% 100%;
  background-repeat: no-repeat;
  transition: background-size 0.4s cubic-bezier(0.7, 0, 0.2, 1);
  padding-bottom: 4px;
}
.link--mneme:hover { background-size: 100% 3px; }
```

---

## 12 · Iocaste — SVG wavy underline slides in

**HTML:**
```html
<a href="#" class="link link--iocaste">
  <span>Label</span>
  <svg class="link__graphic link__graphic--slide" width="300%" height="100%" viewBox="0 0 1200 60" preserveAspectRatio="none">
    <path d="M0,56.5c0,0,298.666,0,399.333,0C448.336,56.5,513.994,46,597,46c77.327,0,135,10.5,200.999,10.5c95.996,0,402.001,0,402.001,0"></path>
  </svg>
</a>
```

```css
.link--iocaste { position: relative; overflow: hidden; }
.link--iocaste span { display: block; }
.link__graphic { position: absolute; bottom: -5%; left: 0; pointer-events: none; fill: none; stroke: currentColor; stroke-width: 2; }
.link__graphic--slide {
  top: 0; left: -100%; width: 300%;
  transform: translate3d(0, 0, 0);
  transition: transform 0.4s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--iocaste:hover .link__graphic--slide { transform: translate3d(calc(100% / 3), 0, 0); }
```

---

## 13 · Herse — SVG arc underline draws in

**HTML:**
```html
<a href="#" class="link link--herse">
  <span>Label</span>
  <svg class="link__graphic link__graphic--stroke link__graphic--arc" width="100%" height="18" viewBox="0 0 59 18">
    <path d="M.945.149C12.3 16.142 43.573 22.572 58.785 10.842" pathLength="1"/>
  </svg>
</a>
```

```css
.link--herse { position: relative; padding-bottom: 6px; }
.link__graphic--stroke path {
  stroke: currentColor;
  stroke-width: 2;
  fill: none;
  stroke-dasharray: 1;
  stroke-dashoffset: 1;
  transition: stroke-dashoffset 0.4s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--herse:hover path { stroke-dashoffset: 0; }
.link__graphic--arc { position: absolute; bottom: 0; left: 0; }
```

---

## 14 · Carme — SVG scribble underline draws in

**HTML:**
```html
<a href="#" class="link link--carme">
  <span>Label</span>
  <svg class="link__graphic link__graphic--stroke link__graphic--scribble" width="100%" height="9" viewBox="0 0 101 9">
    <path d="M.426 1.973C4.144 1.567 17.77-.514 21.443 1.48 24.296 3.026 24.844 4.627 27.5 7c3.075 2.748 6.642-4.141 10.066-4.688 7.517-1.2 13.237 5.425 17.59 2.745C58.5 3 60.464-1.786 66 2c1.996 1.365 3.174 3.737 5.286 4.41 5.423 1.727 25.34-7.981 29.14-1.294" pathLength="1"/>
  </svg>
</a>
```

```css
/* Same technique as Herse — uses stroke-dashoffset animation */
.link--carme { position: relative; padding-bottom: 4px; }
.link__graphic--scribble { position: absolute; bottom: -4px; left: 0; }
.link--carme:hover path { stroke-dashoffset: 0; }
```

---

## 15 · Eirene — Highlight fill slides in

**HTML:** `<a href="#" class="link link--eirene"><span>Label</span></a>`

```css
.link--eirene { position: relative; }
.link--eirene::before {
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: currentColor;
  opacity: 0.15;
  transform: scaleX(0);
  transform-origin: 100% 50%;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
}
.link--eirene:hover::before {
  transform: scaleX(1);
  transform-origin: 0% 50%;
}
```
