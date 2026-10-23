---
id: aos
displayName: AOS (Animate On Scroll)
version: 1.0.0
triggers:
  - /aos
  - /animate-on-scroll
description: Attribute-driven CSS entrance animations triggered by scroll with AOS
---

# AOS Skill

## When to Use
Use this skill for simple scroll-triggered entrance animations via HTML `data-aos` attributes — no JavaScript animation code required.

## Setup
```bash
npm install aos
```
```js
import AOS from 'aos';
import 'aos/dist/aos.css';

AOS.init({
  duration: 800,
  easing: 'ease-out-cubic',
  once: true,
  offset: 80,
});
```

## Core Patterns

### Basic attribute
```html
<div data-aos="fade-up">Fades up on scroll</div>
<div data-aos="zoom-in" data-aos-delay="200">Zooms in with delay</div>
<div data-aos="slide-left" data-aos-duration="1200">Slides from right</div>
```

### Available animations
```
Fade:    fade  fade-up  fade-down  fade-left  fade-right
Zoom:    zoom-in  zoom-out  zoom-in-up  zoom-in-down
Flip:    flip-left  flip-right  flip-up  flip-down
Slide:   slide-up  slide-down  slide-left  slide-right
```

### Per-element options
```html
<div
  data-aos="fade-up"
  data-aos-duration="1000"
  data-aos-delay="100"
  data-aos-easing="ease-in-out"
  data-aos-anchor=".parent"
  data-aos-anchor-placement="top-center"
  data-aos-once="true"
>
```

### Refresh after dynamic content
```js
AOS.refresh();  // recalculate offsets
AOS.refreshHard(); // reinitialise from scratch
```

### React usage
```tsx
useEffect(() => { AOS.init({ once: true }); }, []);
// In JSX:
<div data-aos="fade-up">Content</div>
```

## Best Practices
- Set `once: true` for most use cases to prevent re-triggering on scroll-up
- Use `data-aos-anchor` to trigger animation based on a different element entering view
- Call `AOS.refresh()` after lazy-loaded images settle to fix offset calculations
- Avoid AOS on above-the-fold elements — they'll flash invisible before init
