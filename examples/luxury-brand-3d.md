# Prompt — luxury brand 3D signature moment

A complete prompt for a restrained, expensive-feeling 3D brand "signature
moment" — the kind of single, perfect gesture a luxury brand uses instead of a
busy scene. The whole craft here is **restraint**: material honesty, one
considered light, slow motion, and impeccable typography contrast. Fill the
brackets and send.

---

```
Build a luxury brand 3D signature moment for a Next.js 14 (App Router) + React
18 + TypeScript project using three@0.160.0. Use only real three r160 APIs. The
brief is RESTRAINT: one perfect gesture, not a busy scene. If anything is
ambiguous, list assumptions at the top and proceed.

INTENT
A quiet, premium hero for [brand / product] that conveys [the single quality:
e.g. crafted, timeless, precise]. The visual is [describe one considered gesture:
e.g. a machined [object] rotating a few degrees under a single soft key light,
its material catching one slow highlight]. It sits behind the wordmark
"[brand]" and the line "[tagline]" and must make them feel more expensive, never
compete with them.

MATERIAL & LIGHT (the whole game)
- Physically-based material with honest properties: [metalness/roughness or
  glass/transmission] tuned to read as [real material]. No plastic sheen, no
  rainbow specular.
- Environment map for reflections (RGBELoader if an HDRI is provided; otherwise
  a neutral studio env). ACESFilmicToneMapping, SRGBColorSpace output.
- ONE dominant light with soft shadowing; at most a whisper of fill. The mood
  comes from a single considered light, not from many.
- Colour is disciplined: [1-3 hex values], mostly neutral, one accent used
  sparingly.

MOTION (slow and deliberate)
- Motion is minimal: a slow rotation or a single settle, [<= 12s] per cycle,
  eased gently. Nothing spins forever at a distracting speed.
- prefers-reduced-motion: hold a single beautiful static frame (a considered
  hero pose), no loop.

ARCHITECTURE (required)
- page.tsx is a Server Component: the wordmark, tagline and metadata are real
  server-rendered HTML; OG/Twitter image is a static screenshot of the moment.
  The 3D loads via next/dynamic({ ssr: false }).
- The scene is a Client Component island, code-split. Canvas is aria-hidden; all
  meaning is in the HTML.
- Poster fallback (matching the moment's tone) during load and for no-WebGL — no
  layout shift when the canvas replaces it.

TYPOGRAPHY CONTRAST (do not skip)
- The wordmark and tagline meet WCAG AA against the darkest AND lightest frames
  the scene can produce. If the material's highlight could wash out the text,
  constrain the highlight's travel or add a subtle protective treatment behind
  the type. State how you guaranteed contrast.

CONSTRAINTS
- Cap pixel ratio Math.min(window.devicePixelRatio, 2). Render-on-demand where
  the moment is static; one RAF loop while animating; pause on tab-hidden.
- No per-frame allocations. Handle resize and webglcontextlost (-> poster).
- Adaptive: on low-end / narrow viewports, keep the material and light but drop
  shadow resolution / DPR rather than changing the look.
- Full cleanup on unmount: dispose geometry/material/texture/env map/renderer,
  cancel RAF, remove listeners, remove the canvas.
- Performance budget: <= 20 draw calls, <= [1.5] MB assets, >= 55 fps on a
  named mid-range phone.

DELIVERABLE
Two files with correct TypeScript:
1. app/page.tsx (server component: wordmark, tagline, metadata, poster, loader).
2. app/signature/Signature.tsx (client component, the moment).
After the code, note: the material params chosen and why they read as [material],
how contrast was guaranteed against both frame extremes, and anything to verify
on a real device.
```

---

**Tips**

- **Restraint is the spec.** If the assistant reaches for bloom, particles, or a
  second and third light, push back — luxury reads as one considered gesture,
  not a feature list. A lower draw-call budget than usual is intentional here.
- **The material is the product.** Spend the prompt's detail on metalness /
  roughness / transmission and the environment map, not on motion. An honest PBR
  material under one good light out-classes any animation.
- **Typography contrast is where "premium" is won or lost.** A wordmark that
  dips below AA when the highlight sweeps past looks cheap instantly — demand a
  guarantee against both frame extremes, not the average.
- Neutral palettes and a single accent age better than saturated schemes; say so
  in the ART DIRECTION if the brand allows it.
