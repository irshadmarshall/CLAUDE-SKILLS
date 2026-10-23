---
id: react-spring
displayName: React Spring
version: 1.0.0
triggers:
  - /react-spring
  - /spring
description: Physics-based spring animations in React with @react-spring/web
---

# React Spring Skill

## When to Use
Use this skill for natural-feeling, physics-based animations in React — springy hover effects, list transitions, drag interactions, and number counters.

## Setup
```bash
npm install @react-spring/web
```

## Core Patterns

### useSpring
```tsx
import { useSpring, animated } from '@react-spring/web';

function FadeIn() {
  const styles = useSpring({ from: { opacity: 0 }, to: { opacity: 1 } });
  return <animated.div style={styles}>Hello</animated.div>;
}
```

### Toggle animation
```tsx
const [open, setOpen] = useState(false);
const styles = useSpring({
  height: open ? 200 : 0,
  opacity: open ? 1 : 0,
  config: { tension: 220, friction: 20 },
});
```

### useSprings (list)
```tsx
import { useSprings, animated } from '@react-spring/web';

const springs = useSprings(
  items.length,
  items.map((_, i) => ({ delay: i * 80, from: { opacity: 0, y: 40 }, to: { opacity: 1, y: 0 } }))
);

return springs.map((style, i) => <animated.div key={i} style={style}>{items[i]}</animated.div>);
```

### useTrail (stagger)
```tsx
import { useTrail, animated } from '@react-spring/web';

const trail = useTrail(items.length, { opacity: 1, from: { opacity: 0 } });
return trail.map((style, i) => <animated.div key={i} style={style}>{items[i]}</animated.div>);
```

### Drag gesture with @use-gesture
```tsx
import { useDrag } from '@use-gesture/react';
import { useSpring, animated } from '@react-spring/web';

function Draggable() {
  const [{ x, y }, api] = useSpring(() => ({ x: 0, y: 0 }));
  const bind = useDrag(({ offset: [ox, oy] }) => api.start({ x: ox, y: oy }));
  return <animated.div {...bind()} style={{ x, y, touchAction: 'none' }}>Drag me</animated.div>;
}
```

## Best Practices
- Prefer `immediate: true` for instant resets (e.g., snapping back)
- Use `config: config.gentle` / `config.wobbly` from `@react-spring/web` presets
- Avoid animating layout-triggering properties (width/height) — use `scaleX`/`scaleY` instead
- For enter/leave transitions use `useTransition`
