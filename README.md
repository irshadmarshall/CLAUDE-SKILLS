# Claude Design Skills — Marketplace

A curated collection of Claude Code skills for 3D rendering, animation, and modern web design.

## Quick Start

```bash
# Add this marketplace to Claude Code
/plugin marketplace add freshtechbro/claudedesignskills

# Install individual skills
/plugin install threejs-webgl
/plugin install gsap-scrolltrigger
/plugin install react-three-fiber

# Or install a bundle
/plugin install core-3d-animation
/plugin install extended-3d-scroll
/plugin install animation-components
/plugin install authoring-motion
/plugin install meta-skills
```

## Available Skills

### Individual Skills

| Skill | Description |
|-------|-------------|
| `threejs-webgl` | Three.js scenes, geometries, shaders, and WebGL rendering |
| `gsap-scrolltrigger` | GSAP timelines with ScrollTrigger for scroll-driven animations |
| `react-three-fiber` | Declarative Three.js scenes inside React |
| `motion` | Framer Motion layout animations and gesture handling |
| `babylonjs` | Babylon.js physics, PBR materials, and game-ready scenes |
| `aframe` | A-Frame WebXR/VR declarative scenes |
| `vanta` | Vanta.js animated canvas backgrounds |
| `playcanvas` | PlayCanvas entity-component game engine |
| `pixijs` | PixiJS 2D sprites, filters, and WebGL rendering |
| `locomotive-scroll` | Smooth scroll with parallax and scroll events |
| `barba` | Page transition hooks with Barba.js |
| `react-spring` | Physics-based spring animations in React |
| `magic-ui` | Magic UI animated component primitives |
| `aos` | Animate On Scroll attribute-driven entrance effects |
| `animejs` | Anime.js keyframe and timeline tweening |
| `lottie` | Lottie JSON animation playback and control |
| `blender` | Blender-to-web asset pipeline and GLTF export |
| `spline` | Spline 3D scenes embedded in web projects |
| `rive` | Rive interactive state-machine animations |
| `substance-3d` | Substance 3D texture baking and PBR material workflow |
| `integration-patterns` | Composing multiple 3D/animation libraries together |
| `modern-design` | Modern visual design principles for interactive web |

### Bundles

| Bundle | Skills Included |
|--------|----------------|
| `core-3d-animation` | Three.js · GSAP · R3F · Motion · Babylon.js |
| `extended-3d-scroll` | A-Frame · Vanta · PlayCanvas · PixiJS · Locomotive · Barba |
| `animation-components` | React Spring · Magic UI · AOS · Anime.js · Lottie |
| `authoring-motion` | Blender · Spline · Rive · Substance 3D |
| `meta-skills` | Integration Patterns · Modern Design |

## Repository Structure

```
├── manifest.json          # Marketplace manifest
├── skills/                # Individual skill markdown files
└── bundles/               # Bundle definitions
```
