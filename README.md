# Agent Skills

A curated collection of specialized skills for AI coding assistants. Each skill provides domain-specific instructions, patterns, and best practices to enhance the assistant's ability to handle particular technologies and workflows.

## What are Skills?

Skills are instruction sets that activate contextually when the assistant recognizes relevant patterns in your request. They're designed to:

- Provide accurate, up-to-date documentation for specific libraries and frameworks
- Encode proven patterns and best practices
- Reduce hallucinations by anchoring responses to verified references
- Accelerate development by offering copy-paste-ready code snippets

## Available Skills

### [animejs](/skills/animejs/)

**Trigger**: Anime.js animations, timelines, stagger effects, scroll sync, SVG animations, text effects.

A comprehensive reference covering Anime.js v4.0 — including `animate()`, timelines, scroll observers, SVG utilities, text splitting, spring physics, and WAAPI integration.

```js
import { createTimeline, stagger } from 'animejs';

createTimeline()
  .add('.logo',  { opacity: [0, 1], y: [-20, 0], duration: 600 })
  .add('.title', { opacity: [0, 1], x: [-30, 0], delay: stagger(50) })
  .add('.cta',   { scale: [0.8, 1], opacity: [0, 1] }, '-=200');
```

### [theme-toggle-effect](/skills/theme-toggle-effect/)

**Trigger**: Light/dark mode toggle with smooth transition animations, View Transitions API.

A collection of polished theme toggle effects using CSS masks and the View Transitions API. Includes circle reveals, polygon transitions, blur effects, and gradient animations.

```css
::view-transition-new(root) {
  mask: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 40 40"><circle cx="20" cy="20" r="20" fill="white"/></svg>') center / 0 no-repeat;
  animation: scale 1s;
  animation-fill-mode: both;
}
```

## Adding New Skills

To create a new skill, add a directory under `skills/` with a `SKILL.md` file. Each skill should include:

- **Frontmatter**: `name`, `description`, `version`, `author`
- **Activation triggers**: Clear conditions for when to invoke the skill
- **Decision gates**: Quick-reference table mapping needs to solutions
- **Hard rules**: Non-negotiable patterns and anti-patterns
- **Code examples**: Production-ready snippets for common use cases
- **Output contract**: What the skill should return when invoked

## License

MIT