---
id: substance-3d
displayName: Substance 3D
version: 1.0.0
triggers:
  - /substance
  - /substance-3d
description: Adobe Substance 3D texture baking, PBR material workflow, and export for Three.js / Babylon.js
---

# Substance 3D Skill

## When to Use
Use this skill for creating PBR texture sets in Substance 3D Painter/Designer and integrating them into Three.js, Babylon.js, or R3F projects.

## PBR Texture Set

A standard PBR texture set exported from Substance 3D Painter:

| Map | Purpose |
|-----|---------|
| `albedo` / `baseColor` | Surface colour (no lighting) |
| `normal` | Surface detail without extra geometry |
| `metallic` | Which parts are metal (0–1) |
| `roughness` | Surface microsurface roughness (0–1) |
| `ambientOcclusion` | Precomputed shadow in crevices |
| `emissive` | Self-illuminated areas |

## Export Settings (Substance 3D Painter)
1. File → Export Textures
2. Config: **glTF PBR Metal Roughness**
3. Format: **PNG** (lossless) or **JPEG** (photos, no alpha)
4. Size: 2048×2048 for hero assets, 1024×1024 for secondary

## Load in Three.js
```js
import * as THREE from 'three';
const loader = new THREE.TextureLoader();

const [albedo, normal, orm] = await Promise.all([
  loader.loadAsync('/textures/mat_albedo.png'),
  loader.loadAsync('/textures/mat_normal.png'),
  loader.loadAsync('/textures/mat_orm.png'), // R=AO, G=roughness, B=metallic
]);

// sRGB for colour textures
albedo.colorSpace = THREE.SRGBColorSpace;

const mat = new THREE.MeshStandardMaterial({
  map:              albedo,
  normalMap:        normal,
  aoMap:            orm,
  roughnessMap:     orm,
  metalnessMap:     orm,
  aoMapIntensity:   1.0,
});
```

## Load in Babylon.js
```ts
import { PBRMaterial, Texture } from '@babylonjs/core';
const mat = new PBRMaterial('substance', scene);
mat.albedoTexture       = new Texture('/textures/mat_albedo.png', scene);
mat.bumpTexture         = new Texture('/textures/mat_normal.png', scene);
mat.metallicTexture     = new Texture('/textures/mat_orm.png', scene);
mat.useRoughnessFromMetallicTextureGreen = true;
mat.useMetallnessFromMetallicTextureBlue = true;
```

## KTX2 Compression
```bash
# Convert to GPU-compressed KTX2 (much smaller, faster GPU upload)
npm install -g @gltf-transform/cli
gltf-transform etc1s model.glb model-compressed.glb  # UASTC for normals
gltf-transform uastc model.glb model-compressed.glb --level 4
```

## Best Practices
- Always set `colorSpace = THREE.SRGBColorSpace` on albedo/emissive textures; leave normal/orm as linear
- Pack AO + roughness + metallic into one ORM texture to save texture samplers
- Use KTX2 / Basis textures in production for ~5–10x GPU memory savings
- Match UV scale between Painter and the final mesh — check in Painter's 3D view
