---
id: barba
displayName: Barba.js
version: 1.0.0
triggers:
  - /barba
  - /page-transitions
description: Smooth AJAX page transitions with hooks and custom animations using Barba.js
---

# Barba.js Skill

## When to Use
Use this skill for multi-page websites (not SPAs) that need seamless between-page transitions without full page reloads.

## Setup
```bash
npm install @barba/core
# Optional: GSAP plugin
npm install @barba/prefetch
```

## Core Patterns

### Basic init
```js
import barba from '@barba/core';

barba.init({
  transitions: [
    {
      name: 'fade',
      leave({ current }) {
        return gsap.to(current.container, { opacity: 0, duration: 0.4 });
      },
      enter({ next }) {
        return gsap.from(next.container, { opacity: 0, duration: 0.4 });
      },
    },
  ],
});
```

```html
<body data-barba="wrapper">
  <main data-barba="container" data-barba-namespace="home">
    <!-- page content -->
  </main>
</body>
```

### Namespace-specific transition
```js
barba.init({
  transitions: [
    {
      name: 'to-about',
      from: { namespace: ['home'] },
      to:   { namespace: ['about'] },
      leave: ({ current }) => gsap.to(current.container, { x: '-100%', duration: 0.5 }),
      enter: ({ next })    => gsap.from(next.container,  { x:  '100%', duration: 0.5 }),
    },
  ],
});
```

### Hooks (reinitialise scripts per page)
```js
barba.hooks.after(() => {
  // Re-run any scripts that need fresh DOM
  initAnimations();
  ScrollTrigger.refresh();
});
```

### Prefetch links
```js
import prefetch from '@barba/prefetch';
barba.use(prefetch);
```

## Best Practices
- Return a Promise from `leave`/`enter` (or use GSAP which is thenable)
- Destroy and reinit ScrollTrigger/Locomotive inside `barba.hooks.after`
- Use `preventRunning: true` to block clicks during a transition
- Test with `barba.force()` during development to simulate transitions
