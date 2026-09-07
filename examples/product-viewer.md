# Prompt — interactive 3D product viewer

A complete prompt for an interactive product viewer: load a `.glb`, orbit it,
light it well, auto-frame it regardless of authored scale, and keep it
accessible and fast. Fill the brackets and send.

---

```
Build an interactive 3D product viewer for a Next.js 14 (App Router) + React 18
+ TypeScript project using three@0.160.0. Use only real three r160 APIs,
including GLTFLoader, DRACOLoader and OrbitControls from three/examples/jsm.
State assumptions at the top and proceed.

INTENT
Let a customer inspect [the product] by rotating and zooming it. Model file:
[/models/product.glb], Draco-compressed. The product should read as [material
cues: e.g. brushed aluminium and matte plastic] under studio-style lighting.

FEATURES (required)
- Load the .glb with GLTFLoader + DRACOLoader (set the decoder path). Show a
  determinate or indeterminate loading indicator using GLTFLoader's onProgress,
  and a poster/fallback until the model is ready.
- OrbitControls for rotate + zoom, with enableDamping true. Clamp zoom
  (min/max distance) and optionally the polar angle so the product can't be
  viewed from impossible angles. Disable panning.
- Frame the model automatically: compute its bounding box (Box3), centre it at
  the origin, and position the camera to fit it in view regardless of the
  model's authored scale. This is mandatory — models arrive at wildly different
  scales.
- Lighting: an environment map (RGBELoader if an HDRI is provided) or a simple
  3-point rig (key + fill + rim) so metals and highlights read correctly. Use
  ACESFilmicToneMapping and SRGBColorSpace output.

ARCHITECTURE
- Client Component ('use client'); three mounted in useEffect via a dynamic
  import('three'); host loads it with next/dynamic({ ssr: false }).
- Product name, description and price stay as real HTML next to the viewer (SEO
  + a11y); the canvas is aria-hidden.
- Provide a keyboard-accessible fallback control (real DOM buttons to rotate
  left/right and reset) so the product is inspectable without a mouse drag.

CONSTRAINTS
- Cap pixel ratio at Math.min(window.devicePixelRatio, 2). Render on demand:
  render only while controls are actively changing (OrbitControls 'change'
  event) or during damping, not in a perpetual loop when idle.
- prefers-reduced-motion: skip any intro auto-spin; start static.
- Handle resize; handle a failed model load gracefully (show the poster + a
  short message, don't white-screen); handle webglcontextlost.
- Full cleanup on unmount: traverse the loaded scene and dispose every mesh's
  geometry, material(s) AND textures; dispose controls, renderer and the
  environment map; cancel any RAF; remove listeners; remove the canvas.
- Performance budget: interactive within [2] seconds on broadband, >= 50 fps
  while orbiting on a mid-range phone.

DELIVERABLE
The Client Component with correct TypeScript, plus a usage snippet showing it
loaded via next/dynamic with the poster. After the code, note the model's
draw-call/triangle count if known and confirm the disposal traversal covers
textures.
```

---

**Tips**

- Ask for the auto-framing (bounding-box fit) explicitly — it's the single most
  common "why is it tiny / clipped" bug, and it's trivial to specify and easy to
  forget.
- If you have an HDRI, name it so the assistant wires up `RGBELoader` for the
  environment map instead of hand-building lights — an env map usually reads
  more "product-photography" than a manual rig.
- The disposal traversal is where viewers leak: a single top-level `dispose()`
  misses nested geometries and textures. Demand the `traverse` version and
  verify it by navigating in and out of the page repeatedly.
