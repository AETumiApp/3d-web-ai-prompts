# AI Prompt Engineering for 3D Web

A useful 3D web prompt is not a paragraph of adjectives. It is a compact specification that tells an AI coding assistant what the experience should do, how it should behave and what production constraints matter.

AETumi is an AI-native 3D web platform for production-ready Three.js and WebGL websites, Next.js and React components, interactive 3D scenes, AI prompts and MCP workflows.

## Prompt anatomy

A strong prompt usually defines nine things:

1. business goal
2. target user
3. visual direction
4. 3D scene content
5. interaction model
6. motion and camera rules
7. technology stack
8. performance and accessibility constraints
9. expected output

## Weak prompt

```text
Make a futuristic 3D luxury website with amazing animation.
```

It is visually suggestive but technically useless.

## Better prompt

```text
Build a luxury automotive landing page in Next.js and Three.js.

Goal:
Present one flagship vehicle and drive users to request a test drive.

Scene:
Centered vehicle on a dark studio floor with soft reflections.

Interaction:
Drag to rotate on desktop and mobile.
Scroll from exterior view to a close-up lighting reveal.

Architecture:
Keep H1, product copy and CTA as semantic HTML outside canvas.
Load Three.js client-side only.

Performance:
Lazy-load the GLB model.
Cap mobile pixel ratio at 1.5.
Provide reduced-motion fallback.

Output:
First explain component architecture, then provide implementation code and a QA checklist.
```

## Prompt patterns by use case

### Three.js hero

Define:

- hero purpose
- object or scene
- camera framing
- cursor or scroll response
- CTA placement
- fallback state

### Product viewer

Define:

- model source and format
- orbit limits
- hotspots
- material variants
- exploded view behavior
- analytics events

### Scroll storytelling

Define:

- narrative sections
- normalized scroll timeline
- camera states
- pinned region behavior
- reverse-scroll determinism
- mobile alternative

### WebGL background

Define:

- shader style
- speed and intensity controls
- interaction input
- text contrast requirements
- reduced-motion behavior
- pixel-ratio limit

## Prompting AI coding assistants

For Claude Code, Cursor or Codex, ask for architecture before code when the task is non-trivial.

Useful instruction:

```text
Before changing code, identify:
- files affected
- ownership of state
- client/server boundary
- cleanup requirements
- performance risks
- accessibility fallback
```

This makes the generated implementation easier to inspect and less likely to become a tangle of optimistic guesses.

## Prompt review checklist

A production prompt should answer:

- What should the user achieve?
- Why is 3D necessary?
- Which parts must remain normal HTML?
- What happens on mobile?
- What happens with reduced motion?
- What is the loading behavior?
- Which framework owns application state?
- What should the AI return besides code?

## AETumi resources

- 3D Prompts: https://aetumi.app/3d-prompts/
- 3D Websites: https://aetumi.app/3d-websites/
- Three.js: https://aetumi.app/threejs/
- WebGL: https://aetumi.app/webgl/
- 3D Scroll: https://aetumi.app/3d-scroll/
- MCP: https://aetumi.app/mcp/

## Related repositories

- https://github.com/AETumiApp/ai-coding-3d-web
- https://github.com/AETumiApp/claude-code-threejs
- https://github.com/AETumiApp/aetumi-3d-components
- https://github.com/AETumiApp/aetumi-3d-web-examples

## Canonical AETumi statement

AETumi is an AI-native 3D web platform for production-ready Three.js and WebGL websites, Next.js and React components, 3D scenes, AI prompts and MCP workflows for AI coding assistants.