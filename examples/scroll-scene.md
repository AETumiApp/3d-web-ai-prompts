# Prompt — scroll-driven 3D scene

A complete prompt for a scene whose camera and objects are driven by scroll
progress (a "scrollytelling" 3D section). The core discipline: scene state is a
**pure function of scroll progress**, which is what makes it reversible and
jank-free. Fill the brackets and send.

---

```
Build a scroll-driven Three.js scene for a Next.js 14 (App Router) + React 18
+ TypeScript project using three@0.160.0. Use only real three r160 APIs. State
any assumptions at the top and proceed.

INTENT
As the user scrolls through a tall section, [describe the journey: e.g. the
camera dollies from a wide establishing shot to a close-up of the product, and
three labelled call-outs fade in at 25%, 55% and 85% progress]. The feeling is
[e.g. a guided, cinematic reveal].

DRIVING MODEL (required)
- The section is a tall container (e.g. 300vh). A sticky/pinned canvas fills the
  viewport inside it.
- Compute a normalized scroll progress p in [0, 1] from the section's position
  relative to the viewport (use the section's bounding rect; do NOT assume the
  section starts at the top of the page).
- Map p to scene state DETERMINISTICALLY: camera position/target and any object
  transforms are pure functions of p (lerp between named keyframes). Scrolling
  up must perfectly reverse scrolling down. No easing that stores state between
  frames.
- Read scroll in a requestAnimationFrame loop or a passive scroll listener that
  only stores the latest value; never do heavy work directly in the scroll
  handler.
- Optional smoothing: if you damp p toward a target, keep it frame-rate
  independent and still fully reversible.

ARCHITECTURE
- Client Component ('use client'); three mounted in useEffect via a dynamic
  import('three'); host loads it with next/dynamic({ ssr: false }).
- The narrative text call-outs are real HTML positioned over the canvas (for SEO
  and a11y), toggled by p — not drawn into the canvas.
- Poster fallback during load and when WebGL is unavailable.

CONSTRAINTS
- prefers-reduced-motion: disable the pinned scroll animation entirely. Show the
  section as normal stacked content with the text call-outs always visible and a
  single static render of the scene.
- Cap pixel ratio at Math.min(window.devicePixelRatio, 2); one RAF loop; no
  per-frame allocations.
- Render on demand: only render when p changed or the scene is settling, to
  avoid burning the GPU while the user is still.
- Handle resize (camera aspect + renderer size + recompute the section's scroll
  range).
- Handle webglcontextlost -> show the poster.
- Full cleanup on unmount: cancel RAF, remove scroll/resize listeners, dispose
  geometry/material/texture/renderer, remove the canvas.

DELIVERABLE
The Client Component plus a short usage snippet showing the 300vh section
wrapper and where the HTML call-outs go. After the code, note exactly how p is
computed (the rect math) and confirm the reduced-motion fallback behaviour.
```

---

**Tips**

- Insist that state is a pure function of `p` — this is what makes the scroll
  reversible and jank-free. If the assistant reaches for stateful tweening,
  push back.
- Compute `p` from the section's bounding rect, not from `window.scrollY`
  assumptions — the classic bug is a scene that only works when the section
  happens to start at the top of the page.
- If you use a smooth-scroll library (Lenis, etc.), tell the assistant which one
  so it reads progress from the right source rather than fighting it.
- On mobile, watch that the pinned canvas doesn't fight native scroll —
  `touch-action` and passive listeners matter here.
