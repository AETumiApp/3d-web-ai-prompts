# Prompt — Three.js hero section

A complete, copy-paste prompt for an AI coding assistant. Fill the brackets and
send. It asks for a client-only Three.js hero on Next.js 14 with a poster
fallback, reduced-motion support and full cleanup.

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

ARCHITECTURE (required)
- page.tsx is a Server Component: it holds the SEO metadata, the <h1> and hero
  copy as real HTML, and loads the 3D via next/dynamic(() => import(...),
  { ssr: false }).
- The scene lives in a Client Component ('use client') that mounts three inside
  useEffect with a dynamic import('three').
- Show a poster fallback (a div with role="img" and an aria-label, or a static
  image) while the scene loads and when WebGL is unavailable.
- The canvas is aria-hidden; all meaning stays in the HTML.

CONSTRAINTS
- Cap pixel ratio: renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)).
- One requestAnimationFrame loop; no allocations inside the loop (reuse scratch
  objects).
- Respect prefers-reduced-motion: if reduced, render exactly one static frame
  and do not start the loop.
- Handle resize (update camera.aspect + renderer size).
- Full cleanup on unmount: cancelAnimationFrame, removeEventListener, dispose
  geometry/material/renderer, remove the canvas element.
- Performance budget: <= 30 draw calls, >= 50 fps on a mid-range phone.

DELIVERABLE
Two files with correct TypeScript:
1. app/page.tsx (server component, metadata + copy + dynamic loader + poster)
2. app/hero/Hero.tsx (client component, the scene)
After the code, add a 3-line note: any assumption made, the draw-call count,
and anything a human must verify on a real device.
```

---

**Tips**

- If you have a `.glb` model, add an asset line to INTENT ("load
  `/models/x.glb`, Draco-compressed") and ask it to use `GLTFLoader` +
  `DRACOLoader` from `three/examples/jsm/...`.
- Keep the headline in the prompt so the assistant tunes contrast/legibility
  against it.
