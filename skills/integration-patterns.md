---
id: integration-patterns
displayName: Integration Patterns
version: 1.0.0
triggers:
  - /integration
  - /patterns
description: Patterns for composing Three.js, GSAP, R3F, Locomotive Scroll, and other animation libraries together
---

# Integration Patterns Skill

## When to Use
Use this skill when combining multiple 3D/animation libraries in the same project to avoid conflicts and maximise performance.

## Common Combinations

### Three.js + GSAP (non-React)
```js
import * as THREE from 'three';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';
gsap.registerPlugin(ScrollTrigger);

// Let Three.js own the render loop; GSAP drives values
const uniforms = { uProgress: { value: 0 } };

gsap.to(uniforms.uProgress, {
  value: 1,
  scrollTrigger: { trigger: '#scene', scrub: true },
});

function animate() {
  requestAnimationFrame(animate);
  // uniforms.uProgress.value is updated by GSAP
  renderer.render(scene, camera);
}
animate();
```

### R3F + Framer Motion (React)
```tsx
// Framer Motion handles DOM/CSS; R3F handles canvas
import { motion } from 'motion/react';
import { Canvas } from '@react-three/fiber';

export function HeroSection() {
  return (
    <section>
      {/* CSS layer */}
      <motion.h1 initial={{ opacity: 0 }} animate={{ opacity: 1 }}>
        Hello
      </motion.h1>

      {/* WebGL layer, absolutely positioned behind */}
      <Canvas style={{ position: 'absolute', inset: 0, zIndex: -1 }}>
        <mesh><boxGeometry /><meshNormalMaterial /></mesh>
      </Canvas>
    </section>
  );
}
```

### Locomotive Scroll + GSAP ScrollTrigger proxy
```js
// Single source of scroll truth: Locomotive
// GSAP ScrollTrigger reads from Locomotive's scroll position
scroll.on('scroll', ScrollTrigger.update);
ScrollTrigger.scrollerProxy('[data-scroll-container]', {
  scrollTop(val) {
    return arguments.length
      ? scroll.scrollTo(val, { duration: 0, disableLerp: true })
      : scroll.scroll.instance.scroll.y;
  },
  getBoundingClientRect: () => ({ top: 0, left: 0, width: innerWidth, height: innerHeight }),
});
ScrollTrigger.addEventListener('refresh', () => scroll.update());
ScrollTrigger.refresh();
```

### Barba.js + GSAP + ScrollTrigger (multi-page)
```js
barba.hooks.before(() => {
  ScrollTrigger.getAll().forEach(t => t.kill());
});
barba.hooks.after(() => {
  ScrollTrigger.refresh();
  initPageAnimations();
});
```

### R3F + Lottie (mixed media hero)
```tsx
import { Canvas } from '@react-three/fiber';
import Lottie from 'lottie-react';

<div style={{ position: 'relative', height: '100vh' }}>
  {/* WebGL background */}
  <Canvas style={{ position: 'absolute', inset: 0 }}>
    <mesh><planeGeometry args={[10, 10]} /><meshBasicMaterial color="black" /></mesh>
  </Canvas>

  {/* Lottie overlay */}
  <Lottie
    animationData={data}
    style={{ position: 'absolute', bottom: 40, right: 40, width: 200 }}
  />
</div>
```

## Performance Rules
1. **One render loop** — let Three.js / R3F own `requestAnimationFrame`; GSAP/Framer Motion update values that the render loop reads
2. **Avoid layout thrash** — batch DOM reads before writes; use `will-change: transform` on animated elements
3. **Dispose on unmount** — Three.js geometries, materials, textures; GSAP timelines; Lottie instances; Locomotive Scroll
4. **Separate concerns** — WebGL on `<canvas>` (GPU compositor layer), CSS animations on DOM (CPU/GPU), avoid mixing the two unnecessarily
5. **One scroll driver** — choose Locomotive OR native scroll as the source of truth; proxy GSAP ScrollTrigger to it
