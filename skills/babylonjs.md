---
id: babylonjs
displayName: Babylon.js
version: 1.0.0
triggers:
  - /babylon
  - /babylonjs
description: Physics-enabled 3D scenes, PBR materials, and game-ready experiences with Babylon.js
---

# Babylon.js Skill

## When to Use
Use this skill for full-featured 3D scenes requiring built-in physics, advanced PBR materials, GUI overlays, or Babylon's Inspector debugging tools.

## Setup
```bash
npm install @babylonjs/core @babylonjs/loaders @babylonjs/materials
```

## Core Patterns

### Engine and scene setup
```ts
import { Engine, Scene, ArcRotateCamera, HemisphericLight, Vector3, MeshBuilder } from '@babylonjs/core';

const canvas  = document.getElementById('canvas') as HTMLCanvasElement;
const engine  = new Engine(canvas, true);
const scene   = new Scene(engine);

const camera = new ArcRotateCamera('cam', -Math.PI / 2, Math.PI / 3, 10, Vector3.Zero(), scene);
camera.attachControl(canvas, true);

new HemisphericLight('light', new Vector3(0, 1, 0), scene);

const box = MeshBuilder.CreateBox('box', { size: 1 }, scene);

engine.runRenderLoop(() => scene.render());
window.addEventListener('resize', () => engine.resize());
```

### PBR material
```ts
import { PBRMaterial, Texture } from '@babylonjs/core';
const mat = new PBRMaterial('mat', scene);
mat.albedoTexture  = new Texture('/albedo.png', scene);
mat.metallicTexture = new Texture('/metallic.png', scene);
mat.roughness = 0.4;
box.material = mat;
```

### Load GLTF
```ts
import '@babylonjs/loaders/glTF';
import { SceneLoader } from '@babylonjs/core';

SceneLoader.ImportMeshAsync('', '/models/', 'model.glb', scene).then(({ meshes }) => {
  meshes[0].position.y = 0;
});
```

### Havok physics
```ts
import HavokPhysics from '@babylonjs/havok';
import { HavokPlugin, PhysicsAggregate, PhysicsShapeType } from '@babylonjs/core';

const havok = await HavokPhysics();
scene.enablePhysics(new Vector3(0, -9.81, 0), new HavokPlugin(true, havok));

new PhysicsAggregate(box, PhysicsShapeType.BOX, { mass: 1 }, scene);
```

## Best Practices
- Use `scene.debugLayer.show()` for the built-in Inspector during development
- Prefer `MeshBuilder` factories over direct `new Mesh()` for built-in primitives
- Batch draw calls with `Mesh.MergeMeshes` or thin instances for performance
- Dispose assets with `scene.dispose()` or `mesh.dispose()` to avoid memory leaks
