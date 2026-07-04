---
id: motion
displayName: Framer Motion
version: 1.0.0
triggers:
  - /motion
  - /framer
description: Layout animations, gestures, variants, and page transitions with Framer Motion
---

# Framer Motion Skill

## When to Use
Use this skill for React UI animations — layout transitions, hover/tap effects, scroll-based reveals, shared-layout animations, and route transitions.

## Setup
```bash
npm install motion
```

## Core Patterns

### Basic animate
```tsx
import { motion } from 'motion/react';

<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  exit={{ opacity: 0, y: -20 }}
  transition={{ duration: 0.4, ease: 'easeOut' }}
/>
```

### Variants (stagger children)
```tsx
const container = {
  hidden: { opacity: 0 },
  show: { opacity: 1, transition: { staggerChildren: 0.1 } },
};
const item = { hidden: { y: 20, opacity: 0 }, show: { y: 0, opacity: 1 } };

<motion.ul variants={container} initial="hidden" animate="show">
  {items.map((i) => <motion.li key={i} variants={item}>{i}</motion.li>)}
</motion.ul>
```

### Layout animation
```tsx
<motion.div layout layoutId="card" className="card" />
```

### Scroll-driven (useScroll)
```tsx
import { useScroll, useTransform, motion } from 'motion/react';

function Parallax() {
  const { scrollYProgress } = useScroll();
  const y = useTransform(scrollYProgress, [0, 1], ['0%', '50%']);
  return <motion.div style={{ y }}>...</motion.div>;
}
```

### Gesture
```tsx
<motion.button
  whileHover={{ scale: 1.05 }}
  whileTap={{ scale: 0.97 }}
  transition={{ type: 'spring', stiffness: 400, damping: 20 }}
/>
```

### AnimatePresence (exit animations)
```tsx
import { AnimatePresence, motion } from 'motion/react';

<AnimatePresence mode="wait">
  {show && (
    <motion.div key="modal" initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }}>
      Modal
    </motion.div>
  )}
</AnimatePresence>
```

## Best Practices
- Use `layoutId` for shared-element transitions across routes
- Prefer spring transitions for interactive gestures; ease for entrance/exit
- `mode="wait"` in `<AnimatePresence>` prevents overlapping exit/enter
- Keep variants at the component level and pass them down rather than inlining large objects
