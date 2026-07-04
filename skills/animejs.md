---
id: animejs
displayName: Anime.js
version: 1.0.0
triggers:
  - /anime
  - /animejs
description: Keyframe and timeline tweening for CSS, SVG, DOM, and JS objects with Anime.js
---

# Anime.js Skill

## When to Use
Use this skill for precise keyframe animations on DOM elements, SVG paths, canvas, or plain JS objects — especially staggered sequences and SVG drawing effects.

## Setup
```bash
npm install animejs
```

## Core Patterns

### Basic tween
```js
import anime from 'animejs';

anime({
  targets: '.box',
  translateX: 250,
  rotate: '1turn',
  duration: 800,
  easing: 'easeInOutQuad',
});
```

### Keyframes
```js
anime({
  targets: '.el',
  keyframes: [
    { translateY: -40 },
    { translateX: 250 },
    { translateY: 0 },
    { translateX: 0 },
  ],
  duration: 3000,
  easing: 'easeOutElastic(1, .8)',
});
```

### Stagger
```js
anime({
  targets: '.card',
  opacity: [0, 1],
  translateY: [30, 0],
  delay: anime.stagger(100, { start: 200 }),
});
```

### Timeline
```js
const tl = anime.timeline({ easing: 'easeOutExpo', duration: 600 });
tl
  .add({ targets: '.title',    opacity: [0, 1], translateY: [20, 0] })
  .add({ targets: '.subtitle', opacity: [0, 1], translateY: [20, 0] }, '-=400')
  .add({ targets: '.cta',      opacity: [0, 1], scale: [0.8, 1] },    '-=300');
```

### SVG path drawing
```js
const path = anime.path('.motion-path');
anime({
  targets: '.moving-el',
  translateX: path('x'),
  translateY: path('y'),
  rotate:     path('angle'),
  easing:     'linear',
  duration:   2000,
  loop:       true,
});

// SVG stroke draw-on
anime({ targets: 'path', strokeDashoffset: [anime.setDashoffset, 0], duration: 1500 });
```

### Scroll trigger (manual)
```js
const observer = new IntersectionObserver(([entry]) => {
  if (entry.isIntersecting) anime({ targets: '.el', opacity: [0, 1], translateY: [20, 0] });
}, { threshold: 0.2 });
observer.observe(document.querySelector('.el'));
```

## Best Practices
- Use `anime.timeline` for sequenced, dependent animations
- Prefer `transform` properties over `top`/`left` for GPU compositing
- Call `anim.pause()` / `anim.restart()` rather than recreating instances
- Use `loop: true` + `direction: 'alternate'` for ping-pong effects
