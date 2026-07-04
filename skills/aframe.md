---
id: aframe
displayName: A-Frame
version: 1.0.0
triggers:
  - /aframe
  - /webxr
description: Build WebXR and VR scenes declaratively with A-Frame HTML primitives
---

# A-Frame Skill

## When to Use
Use this skill for WebXR scenes, VR experiences, or simple 3D scenes written as HTML without a build step.

## Setup
```html
<script src="https://aframe.io/releases/1.6.0/aframe.min.js"></script>
```
or
```bash
npm install aframe
```

## Core Patterns

### Basic scene
```html
<a-scene>
  <a-sky color="#ECECEC"></a-sky>
  <a-box position="0 1 -3" rotation="0 45 0" color="#4CC3D9"></a-box>
  <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
  <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>
</a-scene>
```

### GLTF model
```html
<a-scene>
  <a-assets>
    <a-asset-item id="robot" src="/robot.glb"></a-asset-item>
  </a-assets>
  <a-gltf-model src="#robot" position="0 0 -3"></a-gltf-model>
</a-scene>
```

### Custom component
```js
AFRAME.registerComponent('spin', {
  schema: { speed: { type: 'number', default: 1 } },
  tick(time, delta) {
    this.el.object3D.rotation.y += (this.data.speed * delta) / 1000;
  },
});
```
```html
<a-box spin="speed: 2"></a-box>
```

### Cursor interaction
```html
<a-entity camera look-controls>
  <a-entity cursor="fuse: false" raycaster="objects: .clickable"></a-entity>
</a-entity>
<a-box class="clickable" event-set__click="color: red"></a-box>
```

## Best Practices
- Use `<a-assets>` to preload textures and models
- Compress GLTF with Draco or Meshopt
- Keep polygon counts low for mobile VR (< 50k per scene)
- Use `a-entity` with components for custom logic rather than extending primitives
