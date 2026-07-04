---
id: gsap-scrolltrigger
displayName: GSAP ScrollTrigger
version: 1.0.0
triggers:
  - /gsap
  - /scrolltrigger
description: Drive animations with scroll position using GSAP timelines and ScrollTrigger
---

# GSAP ScrollTrigger Skill

## When to Use
Use this skill when building scroll-driven animations, pinned sections, parallax effects, or GSAP tweens and timelines.

## Setup
```bash
npm install gsap
```

## Core Patterns

### Register plugin
```js
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);
```

### Basic scroll animation
```js
gsap.to('.box', {
  x: 500,
  rotation: 360,
  scrollTrigger: {
    trigger: '.box',
    start: 'top 80%',
    end: 'top 20%',
    scrub: true,
  },
});
```

### Pinned section
```js
ScrollTrigger.create({
  trigger: '.pin-section',
  start: 'top top',
  end: '+=200%',
  pin: true,
  scrub: 1,
});
```

### Staggered entrance timeline
```js
const tl = gsap.timeline({
  scrollTrigger: {
    trigger: '.cards',
    start: 'top 70%',
    toggleActions: 'play none none reverse',
  },
});
tl.from('.card', { opacity: 0, y: 60, stagger: 0.12, ease: 'power3.out' });
```

### Horizontal scroll section
```js
const panels = gsap.utils.toArray('.panel');
gsap.to(panels, {
  xPercent: -100 * (panels.length - 1),
  ease: 'none',
  scrollTrigger: {
    trigger: '.horizontal-scroll',
    pin: true,
    scrub: 1,
    end: () => `+=${panels.length * innerWidth}`,
  },
});
```

### Refresh after dynamic content
```js
ScrollTrigger.refresh();
```

## Best Practices
- Always `ScrollTrigger.kill()` or component `.kill()` on unmount in SPAs
- Use `markers: true` during development to visualize trigger points
- `scrub: 1` (number) adds smoothing; `scrub: true` is instant
- Prefer `will-change: transform` on animated elements
- Call `ScrollTrigger.refresh()` after layout shifts (e.g., image loads)
