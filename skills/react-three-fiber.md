---
id: react-three-fiber
displayName: React Three Fiber
version: 1.0.0
triggers:
  - /r3f
  - /react-three
description: Write Three.js scenes declaratively inside React with R3F and Drei helpers
---

# React Three Fiber Skill

## When to Use
Use this skill for Three.js inside React apps — interactive 3D UIs, product viewers, or immersive experiences where React state drives the scene.

## Setup
```bash
npm install @react-three/fiber @react-three/drei three
npm install -D @types/three
```

## Core Patterns

### Canvas bootstrap
```tsx
import { Canvas } from '@react-three/fiber';
import { OrbitControls, Environment } from '@react-three/drei';

export default function Scene() {
  return (
    <Canvas camera={{ position: [0, 0, 5], fov: 60 }} shadows>
      <ambientLight intensity={0.4} />
      <directionalLight position={[5, 5, 5]} castShadow />
      <Environment preset="city" />
      <OrbitControls enableDamping />
      <mesh castShadow>
        <boxGeometry args={[1, 1, 1]} />
        <meshStandardMaterial color="royalblue" />
      </mesh>
    </Canvas>
  );
}
```

### useFrame animation
```tsx
import { useRef } from 'react';
import { useFrame } from '@react-three/fiber';
import type { Mesh } from 'three';

function Spinner() {
  const ref = useRef<Mesh>(null);
  useFrame((_, delta) => {
    if (ref.current) ref.current.rotation.y += delta;
  });
  return (
    <mesh ref={ref}>
      <torusKnotGeometry args={[1, 0.3, 128, 16]} />
      <meshNormalMaterial />
    </mesh>
  );
}
```

### GLTF model with Drei
```tsx
import { useGLTF } from '@react-three/drei';

function Model({ url }: { url: string }) {
  const { scene } = useGLTF(url);
  return <primitive object={scene} />;
}
Model.preload = (url: string) => useGLTF.preload(url);
```

### Shader material with uniforms
```tsx
import { useRef } from 'react';
import { useFrame } from '@react-three/fiber';
import { shaderMaterial } from '@react-three/drei';
import { extend } from '@react-three/fiber';

const WaveMaterial = shaderMaterial(
  { uTime: 0 },
  `varying vec2 vUv; uniform float uTime;
   void main() { vUv = uv; gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0); }`,
  `varying vec2 vUv; uniform float uTime;
   void main() { gl_FragColor = vec4(vUv, sin(uTime) * 0.5 + 0.5, 1.0); }`
);
extend({ WaveMaterial });

function WaveMesh() {
  const ref = useRef<any>(null);
  useFrame(({ clock }) => { if (ref.current) ref.current.uTime = clock.getElapsedTime(); });
  return (
    <mesh>
      <planeGeometry args={[2, 2, 32, 32]} />
      {/* @ts-expect-error custom material */}
      <waveMaterial ref={ref} />
    </mesh>
  );
}
```

## Best Practices
- Wrap `<Canvas>` in a sized container; Canvas fills its parent
- Use `<Suspense fallback={<Loader />}>` for async assets
- Prefer Drei helpers (`useGLTF`, `useTexture`, `Html`) over raw Three.js loaders
- Avoid creating objects in `useFrame`; mutate refs instead
- Use `dpr={[1, 2]}` on `<Canvas>` for responsive pixel ratio
