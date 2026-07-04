---
id: rive
displayName: Rive
version: 1.0.0
triggers:
  - /rive
description: Embed and control Rive interactive state-machine animations in web and React apps
---

# Rive Skill

## When to Use
Use this skill to integrate Rive `.riv` animations with state machines driven by user interaction, app state, or scroll position.

## Setup
```bash
# React
npm install @rive-app/react-canvas

# Vanilla
npm install @rive-app/canvas
```

## Core Patterns

### React (useRive hook)
```tsx
import { useRive } from '@rive-app/react-canvas';

export function RiveButton() {
  const { rive, RiveComponent } = useRive({
    src: '/animations/button.riv',
    stateMachines: 'State Machine 1',
    autoplay: true,
  });

  return (
    <RiveComponent
      onMouseEnter={() => rive?.stateMachineInputs('State Machine 1')
        ?.find(i => i.name === 'Hover')?.fire()}
      style={{ width: 200, height: 60 }}
    />
  );
}
```

### State machine inputs
```tsx
import { useRive, useStateMachineInput } from '@rive-app/react-canvas';

function Interactive() {
  const { rive, RiveComponent } = useRive({
    src: '/hero.riv',
    stateMachines: 'Main',
    autoplay: true,
  });

  const hoverInput  = useStateMachineInput(rive, 'Main', 'Hover');
  const clickInput  = useStateMachineInput(rive, 'Main', 'Click');
  const levelInput  = useStateMachineInput(rive, 'Main', 'Level');

  return (
    <div
      onMouseEnter={() => hoverInput && (hoverInput.value = true)}
      onMouseLeave={() => hoverInput && (hoverInput.value = false)}
      onClick={() => clickInput?.fire()}
    >
      <RiveComponent />
      <input type="range" onChange={e => levelInput && (levelInput.value = +e.target.value)} />
    </div>
  );
}
```

### Vanilla JS
```js
import { Rive, StateMachineInput } from '@rive-app/canvas';

const r = new Rive({
  canvas: document.getElementById('canvas'),
  src: '/hero.riv',
  stateMachines: 'Main',
  autoplay: true,
  onLoad() {
    const inputs = r.stateMachineInputs('Main');
    const hover = inputs.find(i => i.name === 'Hover');
    canvas.addEventListener('mouseenter', () => (hover.value = true));
    canvas.addEventListener('mouseleave', () => (hover.value = false));
  },
});
```

## Best Practices
- Export `.riv` from the Rive editor (File → Export → For Web)
- Name state machine inputs consistently — boolean triggers use `.fire()`, booleans set `.value`
- Use `@rive-app/react-canvas` (not WebGL) for most UI animations
- Handle the `onLoadError` callback to surface missing-file issues
