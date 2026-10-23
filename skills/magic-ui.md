---
id: magic-ui
displayName: Magic UI
version: 1.0.0
triggers:
  - /magic-ui
  - /magicui
description: Copy-paste animated UI components built on Framer Motion and Tailwind CSS
---

# Magic UI Skill

## When to Use
Use this skill when building landing pages or product UIs that need polished, animated components — shimmer text, marquees, animated borders, particles, etc.

## Setup
```bash
# Using the CLI
npx magicui-cli add <component-name>

# Manual: copy component source from magicui.design/docs/<component>
# Requires: Tailwind CSS + Framer Motion
npm install framer-motion clsx tailwind-merge
```

## Popular Components

### Shimmer Button
```tsx
import ShimmerButton from '@/components/ui/shimmer-button';

<ShimmerButton>Get Started</ShimmerButton>
```

### Animated Gradient Text
```tsx
import AnimatedGradientText from '@/components/ui/animated-gradient-text';

<AnimatedGradientText>✨ Introducing Magic UI</AnimatedGradientText>
```

### Marquee (infinite scroll)
```tsx
import Marquee from '@/components/ui/marquee';

<Marquee pauseOnHover className="[--duration:20s]">
  {items.map((item) => <Card key={item.id} {...item} />)}
</Marquee>
```

### Number Ticker
```tsx
import NumberTicker from '@/components/ui/number-ticker';

<NumberTicker value={1000} />
```

### Particles background
```tsx
import Particles from '@/components/ui/particles';

<div className="relative">
  <Particles className="absolute inset-0" quantity={80} />
  <h1 className="relative z-10">Hero</h1>
</div>
```

### Border Beam
```tsx
import { BorderBeam } from '@/components/ui/border-beam';

<div className="relative rounded-xl">
  <BorderBeam size={250} duration={12} />
  Card content
</div>
```

## Best Practices
- Use the CLI (`npx magicui-cli add`) to keep component source in your repo
- All components are unstyled beyond Tailwind — customise via `className`
- Combine `Particles` or `Meteors` backgrounds with `z-index` stacking
- Reduce `quantity` and `duration` for mobile performance
