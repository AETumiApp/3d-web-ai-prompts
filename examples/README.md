# 3D web AI prompts — a premium prompt library

A library of complete, copy-pasteable prompts for building 3D web features with
an AI coding assistant (Claude Code, Cursor, Codex). Each one carries clear
intent, art direction, hard constraints (performance, reduced-motion, capability
fallback, accessibility) and a defined deliverable — so the generated code lands
close to production on the first pass.

Hub: <https://aetumi.app/3d-web-ai-prompts>

## The prompts

| Prompt | Builds | Reach for it when |
| --- | --- | --- |
| [`threejs-hero.md`](./threejs-hero.md) | A client-only Three.js hero backdrop with server-rendered copy, poster fallback, adaptive quality and full cleanup. | You want a 3D moment behind a headline. |
| [`webgl-shader-background.md`](./webgl-shader-background.md) | A full-viewport animated shader background — one fullscreen quad, custom GLSL, cheap and ambient. | You want atmosphere without payload (no models, one draw call). |
| [`scroll-scene.md`](./scroll-scene.md) | A scroll-driven ("scrollytelling") scene where camera and objects are a pure function of scroll progress. | The story unfolds as the user scrolls. |
| [`product-viewer.md`](./product-viewer.md) | An interactive `.glb` product viewer — orbit, zoom, auto-framing, studio lighting, keyboard fallback. | A customer needs to inspect a product in 3D. |
| [`cinematic-landing.md`](./cinematic-landing.md) | A whole landing page sequenced as a short film — hero → scroll reveal → close — under one budget. | You're building the entire page, not one section. |
| [`luxury-brand-3d.md`](./luxury-brand-3d.md) | A restrained luxury "signature moment" — one gesture, honest material, one light, impeccable type contrast. | The brief is premium and the craft is restraint. |

## How to use them

1. Open the prompt that matches your feature.
2. Fill in every `[bracketed]` field — intent, art direction, colours, headline,
   model path, budget numbers, the named baseline phone.
3. Paste it into your assistant and let it generate.
4. Review against the constraints the prompt embedded — **they are the
   acceptance criteria**.

## Shared assumptions in every prompt

- **Stack:** Next.js 14 (App Router), React 18, TypeScript, `three@0.160.0` —
  real r160 APIs only.
- **Architecture:** server-rendered HTML for copy + metadata; the 3D mounts as a
  client-only island via `next/dynamic({ ssr: false })`.
- **Non-negotiables:** capped pixel ratio, single RAF loop, no per-frame
  allocations, `prefers-reduced-motion` handling, a poster/no-WebGL fallback,
  context-loss handling, adaptive quality, and full GPU-resource disposal on
  unmount.

## Companion repos

- Reference implementation of the client-island pattern:
  <https://aetumi.app/nextjs-threejs-starter>
- Briefs, planning prompts, a perf-refactor prompt and the production checklist:
  <https://aetumi.app/claude-code-threejs>
- The cross-assistant workflow these prompts slot into, and the quality bar:
  <https://aetumi.app/ai-coding-3d-web>
- Driving generation with grounded project context via MCP:
  <https://aetumi.app/aetumi-mcp>
