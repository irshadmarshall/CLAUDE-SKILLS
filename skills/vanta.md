---
id: vanta
displayName: Vanta.js
version: 1.0.0
triggers:
  - /vanta
description: Add animated canvas backgrounds (waves, birds, net, fog, etc.) with Vanta.js
---

# Vanta.js Skill

## When to Use
Use this skill to add atmospheric, animated WebGL backgrounds to hero sections, landing pages, or full-screen overlays.

## Setup
```html
<!-- Vanta requires Three.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vanta@latest/dist/vanta.waves.min.js"></script>
```
or with npm (use a CDN build or the vanta npm package + Three.js):
```bash
npm install vanta three
```

## Core Patterns

### Vanilla JS
```js
import * as THREE from 'three';
import WAVES from 'vanta/dist/vanta.waves.min';

const effect = WAVES({
  el: '#hero',
  THREE,
  mouseControls: true,
  touchControls: true,
  color: 0x1a1a2e,
  waveHeight: 20,
  shininess: 50,
  waveSpeed: 0.75,
  zoom: 0.65,
});

// Cleanup
effect.destroy();
```

### React hook
```tsx
import { useEffect, useRef } from 'react';
import * as THREE from 'three';
import NET from 'vanta/dist/vanta.net.min';

export function VantaBackground() {
  const ref   = useRef<HTMLDivElement>(null);
  const vanta = useRef<any>(null);

  useEffect(() => {
    if (!vanta.current && ref.current) {
      vanta.current = NET({ el: ref.current, THREE, color: 0xff6600, backgroundColor: 0x111111 });
    }
    return () => vanta.current?.destroy();
  }, []);

  return <div ref={ref} style={{ width: '100%', height: '100vh' }} />;
}
```

## Available Effects
`WAVES` · `NET` · `BIRDS` · `FOG` · `RINGS` · `GLOBE` · `HALO` · `CLOUDS` · `CELLS` · `TOPOLOGY`

## Best Practices
- Always call `effect.destroy()` on unmount to free GPU resources
- Use `mouseControls: false` on mobile-only sections
- Lower `waveSpeed` / `quantity` for better performance on lower-end devices
- Place content over the Vanta container using `position: relative; z-index: 1`
