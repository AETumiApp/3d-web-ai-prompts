# Prompt — cinematic 3D landing page

A complete prompt for a full landing page built around a cinematic 3D narrative:
a hero, a scroll-driven middle act, and a close — sequenced like a short film,
shipped inside one performance budget. This is the "whole page" prompt; it
composes the hero and scroll-scene patterns into a single coherent experience.
Fill the brackets and send.

---

```
Build a cinematic 3D landing page for a Next.js 14 (App Router) + React 18 +
TypeScript project using three@0.160.0. Use only real three r160 APIs. If
anything is ambiguous, list assumptions at the top and proceed. Do not restyle
beyond the art direction below.

INTENT
A landing page for [product / brand] that unfolds as a short cinematic sequence:
1. HERO — [describe the opening shot and feeling, e.g. the product emerges from
   darkness under a single key light; feeling: arrival, importance].
2. REVEAL (scroll) — [describe the middle act, e.g. the camera orbits the
   product while three feature call-outs fade in at 30/60/90% scroll progress].
3. CLOSE — [describe the ending, e.g. the product settles into a hero pose above
   the primary CTA; feeling: confidence, invitation].
The 3D carries the emotion; the copy carries the meaning.

ART DIRECTION
- Palette: [2-4 hex values]. ACESFilmicToneMapping, SRGBColorSpace output.
- Lighting language: [e.g. single dramatic key + soft rim; no flat ambient].
- Restraint: [what it must NOT do — e.g. no bloom overload, no spinning-forever
  loops, motion serves the narrative not decoration].

PAGE ARCHITECTURE (required)
- app/page.tsx is a Server Component: ALL copy, headings and metadata are real
  server-rendered HTML; OpenGraph/Twitter image is a static screenshot of the
  hero. It loads each 3D act via next/dynamic({ ssr: false }).
- Each act is its own Client Component island, code-split. Share ONE three chunk
  across islands (don't bundle three per island).
- Every act has its own poster and no-WebGL fallback; the page reads as a normal
  stacked page with all copy visible when JS is off.
- Canvases are aria-hidden; all meaning is in the HTML around them.

MOTION & DRIVING MODEL
- HERO: an intro reveal on mount (respecting reduced-motion), then a slow idle or
  static hold. No perpetual expensive loop.
- REVEAL: a pinned/sticky scroll act where scene state is a PURE function of
  scroll progress p in [0,1] computed from the section's bounding rect;
  reversible; call-outs are real HTML toggled by p.
- CLOSE: settles to a static hero pose; the CTA is a real, focusable HTML
  button/link.

BUDGET & PERFORMANCE (page-level, split across acts)
- Total 3D asset payload over the wire <= [4] MB; state the split per act.
- Steady-state draw calls per visible act <= [30].
- LCP element is text or the hero poster, NOT a canvas (verify in Lighthouse
  mobile).
- Sustained >= [50] fps on a named mid-range phone; desktop >= 60.
- Cap pixel ratio Math.min(devicePixelRatio, 2); one RAF loop per active act;
  render-on-demand where an act is static; pause on tab-hidden.
- Adaptive quality ladder (high/medium/low) chosen from viewport width + DPR +
  hardwareConcurrency; high tier looks identical to the intended design.

ACCESSIBILITY & RESILIENCE
- prefers-reduced-motion: no autoplaying cinematics; each act renders a single
  static frame and the scroll act becomes plain stacked content with call-outs
  always visible.
- Text over any canvas meets WCAG AA against the darkest and lightest frames.
- Handle asset-load failure and webglcontextlost per act (poster + message,
  never a white screen).
- Full disposal on unmount for every act (geometry/material/texture/renderer,
  loaded-model traversal, controls, env maps); no leaked WebGL contexts when
  navigating away and back.

DELIVERABLE
- app/page.tsx (server component: copy, metadata, poster + dynamic loaders).
- One Client Component per act (Hero, Reveal, Close) with correct TypeScript.
- A short shared lib for the quality-tier selection and camera-lerp helpers if
  it reduces duplication.
After the code, provide: the per-act budget split you hit (asset MB, draw
calls), how p is computed for the scroll act, the tier-selection logic, and what
a human must verify on a real device.
```

---

**Tips**

- Give it a **three-beat story** (hero → reveal → close) explicitly. A landing
  that's just "3D everywhere" reads as noise; a sequence reads as a film.
- Insist on **one shared `three` chunk**. Three islands each importing `three`
  is the quiet way a "fast" landing ships a fat bundle.
- Storyboard the beats in the prompt if you can — even one line per act — so the
  camera moves serve the narrative instead of wandering.
- Compose from the building blocks: this prompt is the hero
  ([`threejs-hero.md`](./threejs-hero.md)) plus the scroll act
  ([`scroll-scene.md`](./scroll-scene.md)) under one budget. Steal their
  constraint blocks if you want to tune a single act harder.
