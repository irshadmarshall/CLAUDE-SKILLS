---
id: pixijs
displayName: PixiJS
version: 1.0.0
triggers:
  - /pixi
  - /pixijs
description: Fast 2D sprites, filters, tilemaps, and particle effects with PixiJS WebGL renderer
---

# PixiJS Skill

## When to Use
Use this skill for 2D WebGL rendering — sprites, spritesheets, particle effects, UI overlays, interactive data visualisations, and 2D games.

## Setup
```bash
npm install pixi.js
```

## Core Patterns

### Application
```ts
import { Application, Sprite, Assets } from 'pixi.js';

const app = new Application();
await app.init({ resizeTo: window, backgroundAlpha: 0 });
document.body.appendChild(app.canvas);
```

### Sprite from texture
```ts
const texture = await Assets.load('/bunny.png');
const sprite  = new Sprite(texture);
sprite.anchor.set(0.5);
sprite.x = app.screen.width  / 2;
sprite.y = app.screen.height / 2;
app.stage.addChild(sprite);

app.ticker.add(() => { sprite.rotation += 0.01; });
```

### Spritesheet animation
```ts
import { AnimatedSprite, Assets } from 'pixi.js';

const sheet = await Assets.load('/hero.json');
const frames = Object.keys(sheet.textures).map(k => sheet.textures[k]);
const anim = new AnimatedSprite(frames);
anim.animationSpeed = 0.15;
anim.play();
app.stage.addChild(anim);
```

### Graphics (vector shapes)
```ts
import { Graphics } from 'pixi.js';

const g = new Graphics();
g.beginFill(0xff6600).drawRoundedRect(0, 0, 200, 100, 12).endFill();
g.x = 50; g.y = 50;
app.stage.addChild(g);
```

### Filter (blur)
```ts
import { BlurFilter } from 'pixi.js';
sprite.filters = [new BlurFilter(4)];
```

### Container culling
```ts
import { CullingMixin, Container } from 'pixi.js';
const world = new Container();
world.cullable = true;
```

## Best Practices
- Use texture atlases (spritesheets) to minimise draw calls
- Enable `app.renderer.plugins.prepare` to preload GPU uploads
- Pool and reuse particle objects instead of creating/destroying per frame
- Use `container.interactiveChildren = false` on non-interactive containers
- Destroy assets on unmount: `app.destroy(true, { children: true, texture: true })`
