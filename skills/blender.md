---
id: blender
displayName: Blender
version: 1.0.0
triggers:
  - /blender
description: Blender-to-web pipeline: optimise and export 3D models as GLTF/GLB for Three.js or R3F
---

# Blender Skill

## When to Use
Use this skill when exporting Blender models for use in Three.js, React Three Fiber, Babylon.js, or A-Frame web projects.

## Export Pipeline

### GLTF/GLB export settings (Blender 4.x)
1. File → Export → glTF 2.0 (.glb/.gltf)
2. Recommended settings:
   - Format: **GLB** (single binary file)
   - Include: **Selected Objects** (export only what you need)
   - Transform: Apply all transforms before export
   - Geometry: **Apply Modifiers** ✓
   - Compression: **Draco** (for smaller files; requires Three.js DRACOLoader)
   - Textures: **JPEG** (photos) / **PNG** (alpha/normal maps)

### Draco compression CLI
```bash
# Install gltf-transform
npm install -g @gltf-transform/cli

# Compress with Draco
gltf-transform draco input.glb output.glb

# Resize textures
gltf-transform resize input.glb output.glb --width 1024 --height 1024

# Full optimise
gltf-transform optimize input.glb output.glb --compress draco
```

### Load in Three.js
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js';

const draco = new DRACOLoader().setDecoderPath('/draco/');
const loader = new GLTFLoader().setDRACOLoader(draco);

loader.load('/model.glb', ({ scene, animations }) => {
  myScene.add(scene);
  if (animations.length) {
    const mixer = new THREE.AnimationMixer(scene);
    animations.forEach(clip => mixer.clipAction(clip).play());
  }
});
```

### Load in R3F (with gltfjsx)
```bash
# Generate a typed React component from a GLB
npx gltfjsx model.glb --types --transform
```

## Texture Best Practices
- Bake all procedural textures before export
- Use power-of-two texture sizes (512, 1024, 2048)
- Pack Metallic-Roughness into the same texture (R=ambient occlusion, G=roughness, B=metallic) — GLTF standard
- Convert diffuse textures to KTX2 (Basis) for GPU-compressed loading:
  ```bash
  gltf-transform etc1s input.glb output.glb
  ```

## Blender Python (batch export)
```python
import bpy, os

bpy.ops.export_scene.gltf(
    filepath=os.path.join('/out', 'model.glb'),
    export_format='GLB',
    export_draco_mesh_compression_enable=True,
)
```
