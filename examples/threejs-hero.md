# Prompt — Three.js hero section

A complete, copy-paste prompt for an AI coding assistant. Fill the brackets and
send. It asks for a client-only Three.js hero on Next.js 14 with a poster
fallback, reduced-motion support, adaptive quality and full cleanup.

---

```
Build a Three.js hero section for a Next.js 14 (App Router) + React 18 +
TypeScript project using three@0.160.0. Do not invent APIs; use only real
three r160 APIs. If anything is ambiguous, list assumptions at the top and
proceed.

INTENT
A hero that shows [describe the visual: e.g. a slowly rotating faceted crystal
lit from one side] and conveys [the feeling: e.g. precision, calm confidence].
It is a backdrop behind the headline "[headline text]" — the 3D must not
compete with the copy for legibility.

ART DIRECTION
- Palette: [2-4 hex values]. Tone mapping ACESFilmic, SRGB output colour space.
- Restraint: [what it must NOT do — e.g. no bloom, no lens flare, one slow
  motion under 10s/cycle].

ARCHITECTURE (required)
- page.tsx is a Server Component: it holds the SEO metadata, the <h1> and hero
  copy as real HTML, and loads the 3D via next/dynamic(() => import(...),
  { ssr: false }).
- The scene lives in a Client Component ('use client') that mounts three inside
  useEffect with a dynamic import('three').
- Show a poster fallback (a div with role="img" and an aria-label, or a static
  image) while the scene loads and when WebGL is unavailable. No layout shift
  when the canvas replaces the poster.
- The canvas is aria-hidden; all meaning stays in the HTML.

CONSTRAINTS
- Cap pixel ratio: renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)).
- One requestAnimationFrame loop; no allocations inside the loop (reuse scratch
  Vector3/Matrix4/Quaternion objects).
- Respect prefers-reduced-motion: if reduced, render exactly one static frame
  and do not start the loop.
- Handle resize (update camera.aspect + renderer size).
- Pause the loop on document 'visibilitychange' when the tab is hidden.
- Handle webglcontextlost (preventDefault) -> show the poster / attempt restore.
- Adaptive: below [768]px width or DPR-constrained, reduce geometry detail /
  effect cost by a named factor. Keep the desktop look unchanged.
- Full cleanup on unmount: cancelAnimationFrame, removeEventListener, dispose
  geometry/material/texture/renderer, remove the canvas element.
- Performance budget: <= 30 draw calls, >= 50 fps on a mid-range phone
  ([name one]).

DELIVERABLE
Two files with correct TypeScript:
1. app/page.tsx (server component, metadata + copy + dynamic loader + poster)
2. app/hero/Hero.tsx (client component, the scene)
After the code, add a 3-line note: any assumption made, the measured draw-call
count, and anything a human must verify on a real device.
```

---

**Tips**

- If you have a `.glb` model, add an asset line to INTENT ("load
  `/models/x.glb`, Draco-compressed") and ask it to use `GLTFLoader` +
  `DRACOLoader` from `three/examples/jsm/...`.
- Keep the headline in the prompt so the assistant tunes contrast/legibility
  against it — and demand AA contrast against both the lightest and darkest
  frames the scene shows, not the average.
- Pair with the [task brief](https://aetumi.app/claude-code-threejs) so the
  budget and acceptance criteria travel with the code.
