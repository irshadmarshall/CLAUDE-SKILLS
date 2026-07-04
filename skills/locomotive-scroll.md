---
id: locomotive-scroll
displayName: Locomotive Scroll
version: 1.0.0
triggers:
  - /locomotive
  - /smooth-scroll
description: Smooth scroll with parallax and scroll event callbacks using Locomotive Scroll
---

# Locomotive Scroll Skill

## When to Use
Use this skill for buttery smooth scrolling experiences with parallax elements, sticky sections, and scroll progress events.

## Setup
```bash
npm install locomotive-scroll
```
```css
@import 'locomotive-scroll/dist/locomotive-scroll.css';
```

## Core Patterns

### Basic setup (v4)
```js
import LocomotiveScroll from 'locomotive-scroll';

const scroll = new LocomotiveScroll({
  el: document.querySelector('[data-scroll-container]'),
  smooth: true,
  multiplier: 0.8,
});
```

```html
<div data-scroll-container>
  <section data-scroll-section>
    <h1 data-scroll data-scroll-speed="-2">Slow parallax</h1>
    <img data-scroll data-scroll-speed="4" src="hero.jpg" />
  </section>
</div>
```

### Scroll event
```js
scroll.on('scroll', ({ scroll, limit }) => {
  const progress = scroll.y / limit.y;
  // drive other animations with progress
});
```

### With GSAP ScrollTrigger (proxy)
```js
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

scroll.on('scroll', ScrollTrigger.update);
ScrollTrigger.scrollerProxy('[data-scroll-container]', {
  scrollTop(value) {
    return arguments.length
      ? scroll.scrollTo(value, { duration: 0, disableLerp: true })
      : scroll.scroll.instance.scroll.y;
  },
  getBoundingClientRect() {
    return { top: 0, left: 0, width: innerWidth, height: innerHeight };
  },
  pinType: document.querySelector('[data-scroll-container]').style.transform ? 'transform' : 'fixed',
});
ScrollTrigger.addEventListener('refresh', () => scroll.update());
ScrollTrigger.refresh();
```

### Destroy on unmount
```js
scroll.destroy();
```

## Best Practices
- Always call `scroll.update()` after DOM changes (images load, content added)
- Use `data-scroll-speed` sparingly — heavy parallax can cause layout thrashing
- In SPAs, destroy and reinitialise on route change
- Test scroll behaviour with `smooth: false` first to isolate issues
