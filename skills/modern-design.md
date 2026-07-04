---
id: modern-design
displayName: Modern Design
version: 1.0.0
triggers:
  - /design
  - /modern-design
description: Visual design principles, motion guidelines, and Tailwind CSS patterns for modern interactive web
---

# Modern Design Skill

## When to Use
Use this skill when designing or implementing the visual and motion language of a modern web product — layout, typography, colour, spacing, and animation principles.

## Layout Principles

### Grid
```css
/* 12-column fluid grid */
.grid { display: grid; grid-template-columns: repeat(12, 1fr); gap: clamp(1rem, 2vw, 1.5rem); }

/* Centered content with max-width */
.container { max-width: 1280px; margin-inline: auto; padding-inline: clamp(1rem, 5vw, 4rem); }
```

### Fluid typography (clamp)
```css
h1 { font-size: clamp(2rem, 5vw + 1rem, 5rem); line-height: 1.1; }
p  { font-size: clamp(1rem, 1.5vw + 0.5rem, 1.25rem); line-height: 1.6; }
```

### Tailwind equivalents
```html
<!-- Hero layout -->
<section class="min-h-screen grid place-items-center px-4 md:px-16">
  <div class="max-w-5xl w-full">
    <h1 class="text-4xl md:text-7xl font-bold tracking-tight leading-none">
      Headline
    </h1>
  </div>
</section>
```

## Colour

### CSS custom properties + dark mode
```css
:root {
  --color-bg:      #ffffff;
  --color-text:    #0f0f0f;
  --color-accent:  #6c63ff;
  --color-muted:   #6b7280;
}
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg:   #0f0f0f;
    --color-text: #f5f5f5;
  }
}
```

### Glassmorphism
```css
.glass {
  background: rgba(255,255,255,0.08);
  backdrop-filter: blur(16px) saturate(180%);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 1rem;
}
```

## Motion Guidelines

| Use case | Duration | Easing |
|----------|----------|--------|
| Hover/focus | 150–200 ms | ease-out |
| Entrance animation | 300–500 ms | ease-out-cubic |
| Complex layout shift | 500–700 ms | spring |
| Ambient/looping | 2000+ ms | linear / sine |

```css
/* Good easing presets */
:root {
  --ease-out-expo:   cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out-quad: cubic-bezier(0.45, 0, 0.55, 1);
  --ease-spring:     cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

## Scroll-driven Animation (CSS native)
```css
@keyframes fade-up {
  from { opacity: 0; translate: 0 2rem; }
  to   { opacity: 1; translate: 0 0; }
}

.reveal {
  animation: fade-up linear both;
  animation-timeline: view();
  animation-range: entry 0% entry 40%;
}
```

## Micro-interaction Patterns
```css
/* Magnetic button feel */
.btn {
  transition: transform 200ms var(--ease-out-expo),
              box-shadow 200ms ease;
}
.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 32px rgba(0,0,0,0.15);
}
.btn:active { transform: translateY(0); }
```

## Best Practices
- Respect `prefers-reduced-motion`: wrap all animations in `@media (prefers-reduced-motion: no-preference)`
- Use `will-change: transform` only on elements actively animating — remove after animation ends
- Follow the 60fps rule: animate `transform` and `opacity` only; avoid `width`, `height`, `top`, `left`
- Keep z-index values in a named scale (1=base, 10=sticky, 50=modal, 100=tooltip)
