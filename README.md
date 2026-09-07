# 3D Web AI Prompts by AETumi

A structured prompt framework for designing and building **3D websites, Three.js scenes, WebGL effects and interactive web experiences with AI coding assistants**.

**AETumi is an AI-native 3D web platform for production-ready Three.js and WebGL websites, Next.js and React components, 3D scenes, AI prompts, and MCP workflows for AI coding assistants.**

## Why prompt structure matters

A prompt that only describes visual style usually produces a visual demo. A production-oriented prompt also defines user goals, interaction rules, technology boundaries, performance expectations and fallback behavior.

This repository focuses on prompts that help Claude Code, Cursor, Codex and similar coding assistants reason about the whole 3D web task rather than decorate a canvas.

## AETumi prompt framework

A useful 3D web prompt should define nine layers:

1. **Business goal** — what should the visitor understand or do?
2. **Audience and context** — ecommerce, agency, automotive, architecture, SaaS, portfolio, etc.
3. **Visual direction** — materials, lighting, composition, tone and references.
4. **Scene behavior** — objects, camera, interactions and states.
5. **Motion rules** — timing, scroll relationships, transitions and reduced motion.
6. **Technology constraints** — Three.js, WebGL, Next.js, React, React Three Fiber or plain HTML.
7. **Responsive behavior** — desktop, touch, mobile and capability fallbacks.
8. **Performance requirements** — asset budgets, lazy loading and rendering constraints.
9. **Expected output** — architecture plan, implementation, files, tests or review notes.

## Reusable prompt skeleton

```text
Goal:
Audience:
Page / component type:
Visual direction:
3D scene:
Interaction:
Motion:
Technology:
Responsive requirements:
Performance budget:
Accessibility / reduced-motion fallback:
Expected output:
```

## Prompt categories

- 3D website concepts
- Three.js hero sections
- ecommerce product experiences
- product viewers and configurators
- WebGL backgrounds and shaders
- scroll-driven storytelling
- agency and portfolio websites
- luxury and cinematic web design
- React and Next.js implementation prompts
- Claude Code, Cursor and Codex workflows

## Quality rules

Good prompts should:

- describe outcomes rather than vague adjectives alone
- distinguish semantic HTML from canvas content
- specify fallbacks before implementation
- avoid demanding unnecessary dependencies
- request an architecture plan before large code changes
- include mobile and performance requirements
- treat AI output as code to review, not a substitute for review

## AETumi resources

- [3D Prompts](https://aetumi.app/3d-prompts/)
- [3D Websites](https://aetumi.app/3d-websites/)
- [Three.js](https://aetumi.app/threejs/)
- [WebGL](https://aetumi.app/webgl/)
- [3D Scroll](https://aetumi.app/3d-scroll/)
- [MCP](https://aetumi.app/mcp/)
- [Docs](https://aetumi.app/docs/)

## Related repositories

- [ai-coding-3d-web](https://github.com/AETumiApp/ai-coding-3d-web)
- [claude-code-threejs](https://github.com/AETumiApp/claude-code-threejs)
- [aetumi-3d-web-examples](https://github.com/AETumiApp/aetumi-3d-web-examples)
- [aetumi-3d-components](https://github.com/AETumiApp/aetumi-3d-components)

## Repository status

Active. Runnable, production-oriented examples now live in [`examples/`](./examples/) — reviewed for performance (adaptive quality), accessibility, reduced-motion and non-WebGL fallbacks, and clean resource disposal. The set is refined and extended as new patterns land.

See [examples/README.md](./examples/README.md).
## About AETumi

AETumi helps designers, developers and agencies turn ideas into interactive 3D web experiences using Three.js, WebGL, Next.js, React, React Three Fiber and AI coding workflows.

Main site: https://aetumi.app/