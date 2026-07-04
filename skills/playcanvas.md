---
id: playcanvas
displayName: PlayCanvas
version: 1.0.0
triggers:
  - /playcanvas
description: Entity-component game engine for interactive 3D experiences and AR/VR with PlayCanvas
---

# PlayCanvas Skill

## When to Use
Use this skill for game-style 3D experiences, product configurators, or interactive scenes needing a full entity-component system, physics, and audio.

## Setup
```bash
npm install playcanvas
```

## Core Patterns

### Application bootstrap
```js
import * as pc from 'playcanvas';

const canvas = document.getElementById('canvas');
const app = new pc.Application(canvas, {
  mouse: new pc.Mouse(canvas),
  touch: new pc.TouchDevice(canvas),
});
app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
app.setCanvasResolution(pc.RESOLUTION_AUTO);
app.start();
```

### Create entity with model
```js
const box = new pc.Entity('box');
box.addComponent('model', { type: 'box' });
box.addComponent('rigidbody', { type: pc.BODYTYPE_DYNAMIC });
box.addComponent('collision', { type: 'box' });
box.setPosition(0, 5, 0);
app.root.addChild(box);
```

### Camera and light
```js
const camera = new pc.Entity('camera');
camera.addComponent('camera', { clearColor: new pc.Color(0.1, 0.1, 0.15) });
camera.setPosition(0, 5, 10);
app.root.addChild(camera);

const light = new pc.Entity('light');
light.addComponent('light');
light.setEulerAngles(45, 30, 0);
app.root.addChild(light);
```

### Script component
```js
const Rotate = pc.createScript('rotate');
Rotate.attributes.add('speed', { type: 'number', default: 10 });
Rotate.prototype.update = function (dt) {
  this.entity.rotate(0, this.speed * dt, 0);
};
```

### Load GLTF asset
```js
const asset = new pc.Asset('model', 'container', { url: '/model.glb' });
app.assets.add(asset);
app.assets.load(asset);
asset.ready(() => {
  const entity = asset.resource.instantiateRenderEntity();
  app.root.addChild(entity);
});
```

## Best Practices
- Use `pc.Application#destroy()` to free all resources
- Prefer the PlayCanvas Editor for complex scenes; use the engine directly for embeds
- Enable `app.graphicsDevice.maxPixelRatio = 2` for retina
- Use LOD groups and occlusion culling for large scenes
