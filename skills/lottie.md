---
id: lottie
displayName: Lottie
version: 1.0.0
triggers:
  - /lottie
description: Play, control, and synchronise Lottie JSON animations exported from Adobe After Effects
---

# Lottie Skill

## When to Use
Use this skill to embed After Effects animations as lightweight JSON, control playback programmatically, or sync animation frames to scroll or interaction events.

## Setup
```bash
# Web (full-featured)
npm install lottie-web

# React wrapper
npm install lottie-react

# Lightweight web player
npm install @lottiefiles/dotlottie-web
```

## Core Patterns

### lottie-web (vanilla)
```js
import lottie from 'lottie-web';

const anim = lottie.loadAnimation({
  container:     document.getElementById('lottie'),
  renderer:      'svg',
  loop:          true,
  autoplay:      true,
  path:          '/animations/confetti.json',
});

// Control
anim.pause();
anim.play();
anim.setSpeed(0.5);
anim.goToAndStop(30, true); // frame 30, stop
anim.destroy();
```

### React
```tsx
import Lottie from 'lottie-react';
import confetti from './confetti.json';

function ConfettiAnim() {
  return <Lottie animationData={confetti} loop={true} style={{ width: 300, height: 300 }} />;
}
```

### Scroll-synced playback
```js
const anim = lottie.loadAnimation({
  container: el, renderer: 'svg', loop: false, autoplay: false, path: '/data.json',
});

window.addEventListener('scroll', () => {
  const progress = window.scrollY / (document.body.scrollHeight - innerHeight);
  anim.goToAndStop(Math.floor(progress * anim.totalFrames), true);
});
```

### DotLottie (`.lottie` format)
```js
import { DotLottie } from '@lottiefiles/dotlottie-web';

const dotlottie = new DotLottie({
  canvas:   document.getElementById('canvas'),
  src:      '/animations/hero.lottie',
  loop:     true,
  autoplay: true,
});
```

## Best Practices
- Use `renderer: 'canvas'` for many simultaneous instances (better performance than SVG)
- Prefer `.lottie` (dotLottie) format — up to 10x smaller than JSON
- Call `anim.destroy()` on unmount to free memory
- Export with bodymovin plugin from After Effects; optimise with LottieFiles optimiser
