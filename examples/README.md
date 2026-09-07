# 3D web AI prompts — examples

A small library of complete, copy-pasteable prompts for building 3D web features
with an AI coding assistant (Claude Code, Cursor, Codex). Each one carries clear
intent, hard constraints (performance, reduced-motion, fallback) and a defined
deliverable — so the generated code lands close to production.

Hub: <https://aetumi.app/3d-web-ai-prompts>

## The prompts

| Prompt | Builds |
| --- | --- |
| [`threejs-hero.md`](./threejs-hero.md) | A client-only Three.js hero backdrop with server-rendered copy, poster fallback and full cleanup. |
| [`webgl-shader-background.md`](./webgl-shader-background.md) | A full-viewport animated shader background — one fullscreen quad, custom GLSL, cheap and ambient. |
| [`scroll-scene.md`](./scroll-scene.md) | A scroll-driven ("scrollytelling") scene where camera and objects are a pure function of scroll progress. |
| [`product-viewer.md`](./product-viewer.md) | An interactive `.glb` product viewer — orbit, zoom, auto-framing, studio lighting, keyboard fallback. |

## How to use them

1. Open the prompt that matches your feature.
2. Fill in every `[bracketed]` field — intent, colours, headline, model path,
   budget numbers.
3. Paste it into your assistant and let it generate.
4. Review against the constraints the prompt embedded (they're the acceptance
   criteria).

## Shared assumptions in every prompt

- **Stack:** Next.js 14 (App Router), React 18, TypeScript, `three@0.160.0` —
  real r160 APIs only.
- **Architecture:** server-rendered HTML for copy + metadata; the 3D mounts as a
  client-only island via `next/dynamic({ ssr: false })`.
- **Non-negotiables:** capped pixel ratio, single RAF loop, `prefers-reduced-motion`
  handling, a poster/no-WebGL fallback, and full GPU-resource disposal on
  unmount.

## Companion repos

- Reference implementation: <https://aetumi.app/nextjs-threejs-starter>
- Briefs, planning prompt and production checklist:
  <https://aetumi.app/claude-code-threejs>
- The cross-assistant workflow these prompts slot into:
  <https://aetumi.app/ai-coding-3d-web>

---

## Example backlog / roadmap

# 3D Web AI Prompt Example Backlog

## Planned prompt families

### Three.js hero

Prompt for a responsive 3D hero with semantic HTML copy, a lazy-loaded scene and reduced-motion fallback.

### Ecommerce product viewer

Prompt for product rotation, hotspots, variants and analytics-friendly interaction events.

### Scroll-driven product story

Prompt for deterministic scroll progress, camera chapters, mobile fallback and performance constraints.

### WebGL shader background

Prompt for a reusable visual component with explicit fragment complexity, resize behavior and reduced-motion rules.

### Agency delivery brief

Prompt that starts from client goals and asks the AI coding assistant for architecture, implementation plan, QA and handoff documentation.

### Code review prompt

Prompt for auditing an existing Three.js or WebGL implementation for leaks, frame cost, loading, accessibility and responsive issues.

## Evaluation criteria

A useful prompt should make it easy to answer:

- What is being built?
- Why does the user need it?
- Which part belongs in 3D?
- Which part remains semantic HTML?
- What happens on mobile?
- What happens with reduced motion?
- How will performance be measured?
- What output should the AI return?

## AETumi links

- https://aetumi.app/3d-prompts/
- https://aetumi.app/threejs/
- https://aetumi.app/mcp/
