# Prompt — WebGL shader background

A complete prompt for a full-viewport animated shader background rendered with
Three.js — a single fullscreen quad driven by a fragment shader. Cheap, ambient,
and behind your content. Fill the brackets and send.

---

```
Build a full-viewport animated shader background for a Next.js 14 (App Router)
+ React 18 + TypeScript project using three@0.160.0. Use only real three r160
APIs (ShaderMaterial, PlaneGeometry, OrthographicCamera). If anything is
ambiguous, state assumptions and proceed.

INTENT
A calm, slow-moving [describe: e.g. flowing gradient / soft noise field /
aurora-like waves] in the palette [list 2-4 hex colours]. It sits behind page
content as ambience; it must never distract or reduce text contrast.

APPROACH (required)
- Render a single fullscreen quad: a PlaneGeometry(2, 2) with an
  OrthographicCamera, so the fragment shader fills the viewport. This is far
  cheaper than a 3D scene.
- Drive the effect with a custom ShaderMaterial. Uniforms: uTime (seconds),
  uResolution (vec2), and uColorA/uColorB[/uColorC] for the palette.
- Keep the fragment shader GLSL simple and readable: use smooth value/gradient
  math or a small noise function (e.g. a compact simplex/value noise); comment
  the key lines. No external texture fetches.
- Make the animation tileable in time (loops seamlessly) if it runs
  indefinitely.

ARCHITECTURE
- Client Component ('use client'); mount three in useEffect via a dynamic
  import('three') to keep it out of the server bundle.
- The host page loads it with next/dynamic({ ssr: false }); the container div
  carries a CSS gradient in the same palette as the no-WebGL / loading fallback.
- aria-hidden on the container; it is decorative only.

CONSTRAINTS
- Cap pixel ratio at Math.min(window.devicePixelRatio, 2). For a heavy shader,
  render at 0.75x resolution and let CSS scale it up (state the trade-off).
- Update uResolution on resize; keep one requestAnimationFrame loop.
- Respect prefers-reduced-motion: freeze uTime at a pleasant constant (render a
  single static frame) instead of animating.
- Pause the loop on document 'visibilitychange' when the tab is hidden.
- Handle webglcontextlost (preventDefault) -> fall back to the CSS gradient.
- Full cleanup on unmount: cancelAnimationFrame, remove listeners, dispose
  geometry, material and renderer, remove the canvas.

DELIVERABLE
One Client Component file (e.g. components/ShaderBackground.tsx) with correct
TypeScript and the inline vertex + fragment shaders. After the code, note the
approximate GPU cost, the resolution scale chosen, and confirm the
reduced-motion and no-WebGL fallbacks.
```

---

**Tips**

- If text sits on top, tell it the text colour so it can keep contrast within
  the animated range (WCAG AA against both the lightest and darkest frames).
- Value/gradient noise is cheaper than layered fBm — if the background is meant
  to be subtle, ask for the cheapest thing that reads well, not the fanciest.
- A shader background is often the right choice *instead of* a 3D hero when you
  want ambience without payload: no models, no lights, one draw call.
