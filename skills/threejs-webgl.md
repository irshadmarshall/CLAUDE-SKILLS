---
id: threejs-webgl
displayName: Three.js WebGL
version: 1.0.0
triggers:
  - /threejs
  - /three
description: Build Three.js scenes with geometries, materials, lights, cameras, and custom shaders
---

# Three.js WebGL Skill

## When to Use
Use this skill when asked to build 3D scenes, WebGL visualisations, particle systems, custom shaders, or anything powered by Three.js.

## Setup
```bash
npm install three
# TypeScript types
npm install -D @types/three
```

## Core Patterns

### Minimal scene bootstrap
```js
import * as THREE from 'three';

const scene    = new THREE.Scene();
const camera   = new THREE.PerspectiveCamera(75, innerWidth / innerHeight, 0.1, 1000);
const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
renderer.setPixelRatio(devicePixelRatio);
renderer.setSize(innerWidth, innerHeight);
document.body.appendChild(renderer.domElement);

camera.position.z = 5;

function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();

window.addEventListener('resize', () => {
  camera.aspect = innerWidth / innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(innerWidth, innerHeight);
});
```

### PBR material
```js
const material = new THREE.MeshStandardMaterial({
  color: 0x88ccff,
  metalness: 0.4,
  roughness: 0.3,
  envMapIntensity: 1.0,
});
```

### Custom GLSL shader
```js
const mat = new THREE.ShaderMaterial({
  uniforms: { uTime: { value: 0 } },
  vertexShader: /* glsl */`
    uniform float uTime;
    varying vec2 vUv;
    void main() {
      vUv = uv;
      vec3 pos = position;
      pos.y += sin(pos.x * 3.0 + uTime) * 0.2;
      gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
    }
  `,
  fragmentShader: /* glsl */`
    varying vec2 vUv;
    void main() {
      gl_FragColor = vec4(vUv, 1.0, 1.0);
    }
  `,
});

// Update in animation loop
mat.uniforms.uTime.value = clock.getElapsedTime();
```

### GLTF loader
```js
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { DRACOLoader } from 'three/addons/loaders/DRACOLoader.js';

const draco = new DRACOLoader();
draco.setDecoderPath('/draco/');

const loader = new GLTFLoader();
loader.setDRACOLoader(draco);
loader.load('/model.glb', ({ scene: model }) => {
  scene.add(model);
});
```

### Orbit controls
```js
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
const controls = new OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;
// call controls.update() inside animate()
```

## Best Practices
- Dispose geometries and materials when removing objects: `geo.dispose(); mat.dispose();`
- Use `renderer.shadowMap.enabled = true` and `castShadow`/`receiveShadow` for shadows
- Prefer `BufferGeometry` and instancing (`InstancedMesh`) for large numbers of objects
- Use `renderer.setPixelRatio(Math.min(devicePixelRatio, 2))` to cap on retina screens
- Prefer compressed textures (KTX2 / Basis) via `KTX2Loader` for large assets
