---
id: spline
displayName: Spline
version: 1.0.0
triggers:
  - /spline
description: Embed interactive Spline 3D scenes in web projects with the Spline viewer or React component
---

# Spline Skill

## When to Use
Use this skill to embed Spline-authored 3D scenes in React or vanilla HTML projects, and to control scene state, events, and variables programmatically.

## Setup
```bash
# React
npm install @splinetool/react-spline @splinetool/runtime

# Vanilla
npm install @splinetool/runtime
```

## Core Patterns

### React embed
```tsx
import Spline from '@splinetool/react-spline';

export default function Hero() {
  return (
    <Spline
      scene="https://prod.spline.design/YOUR_SCENE_ID/scene.splinecode"
      style={{ width: '100%', height: '100vh' }}
    />
  );
}
```

### Access Spline application instance
```tsx
import { useRef } from 'react';
import Spline from '@splinetool/react-spline';
import type { Application } from '@splinetool/runtime';

export default function Scene() {
  const splineRef = useRef<Application | null>(null);

  function onLoad(app: Application) {
    splineRef.current = app;
  }

  function handleClick() {
    splineRef.current?.emitEvent('mouseDown', 'Cube');
  }

  return <Spline scene="..." onLoad={onLoad} />;
}
```

### Spline events
```tsx
<Spline
  scene="..."
  onSplineMouseDown={(e) => console.log('clicked object:', e.target.name)}
  onSplineMouseHover={(e) => console.log('hovering:', e.target.name)}
/>
```

### Set variable
```ts
splineRef.current?.setVariable('color', '#ff0000');
```

### Vanilla JS
```js
import { Application } from '@splinetool/runtime';

const canvas = document.getElementById('canvas');
const app = new Application(canvas);
await app.load('https://prod.spline.design/YOUR_SCENE_ID/scene.splinecode');
app.emitEvent('mouseDown', 'Button');
```

## Best Practices
- Use the "Export → Web" option in Spline to get the `.splinecode` URL
- Keep scene polygon counts reasonable for mobile (< 100k tris)
- Wrap `<Spline>` in a `<Suspense>` boundary for loading states
- Use `onSplineMouseDown` / `onSplineMouseHover` for interactive hotspots
- Disable Spline's watermark in the editor export settings (paid plan)
