---
name: frontend-rendering-selection
description: Select static, server, client, streamed, or hybrid rendering for a web project's routes and journeys. Use when architecture, discoverability, initial performance, personalization, caching, or offline behavior depends on where HTML and logic run; do not assume one rendering mode must cover the whole application.
---

# Frontend Rendering Selection

## Outcome

Produce a route-level rendering decision that balances user experience, discoverability, freshness, interactivity, privacy, reliability, operational load, and cost.

Read [rendering tradeoffs](references/rendering-tradeoffs.md) before comparing approaches.

## Inputs

For each important route or journey, establish content freshness, public discoverability, personalization, authentication, interaction intensity, offline requirements, device and network constraints, latency geography, traffic shape, cacheability, deployment model, data sensitivity, and team operating capacity.

## Workflow

1. Divide the product into route classes that can change independently.
2. Start with the least client-side execution that preserves the required experience. Prefer usable HTML before optional enhancement for public and content-first journeys.
3. Compare static generation, server rendering, client rendering, streaming, and hybrid or island patterns against the route's constraints.
4. Describe data flow, cache boundaries, invalidation, personalization, failure behavior, and the JavaScript required before each critical action works.
5. Check that private or user-specific content cannot enter shared caches, build artifacts, or another user's streamed response.
6. Estimate build time, server compute, origin load, CDN behavior, client transfer and execution, observability, deployment coupling, and rollback complexity.
7. When the choice remains uncertain, build a thin representative route and measure field-relevant outcomes under representative device, network, data, and cache conditions.
8. Record the material decision in an ADR and define triggers for revisiting it.

## 2026 Currency

Framework versions constrain rendering modes, so check the rendering model of the exact version selected in [Frontend Framework Selection](../frontend-framework-selection/SKILL.md) — do not assume a framework's current rendering defaults match an older version's. Versions below are the research snapshot dated 2026-11-09; re-check current releases before citing them.

- **Next.js 16 / Cache Components.** Cache Components are the recommended caching model in Next.js 16 (recommended for every app from 16.4, default for new projects, slated to become the default in Next.js 17). This changes the server-rendering default: decide cache boundaries per route explicitly rather than assuming dynamic rendering, and record what is cached, for how long, and how it invalidates.
- **Astro 5 / Server Islands.** Server Islands allow partial dynamic rendering inside otherwise static pages, and Astro ships zero JavaScript by default — content-first routes can stay static with islands carrying only the dynamic parts.
- **React 19.3 Server Components and Svelte 5 Runes.** Server Components move rendering and data loading to the server for routes that need it, while Runes make Svelte reactivity explicit; either way, the framework version — not the framework name — decides which rendering modes are actually available to a route.

## Guardrails

- Do not select a framework first and retrofit its preferred rendering model to every route.
- Search-engine visibility is one constraint, not the only reason to send meaningful HTML.
- Streaming can improve progressive delivery but does not remove data-fetching, caching, hydration, accessibility, or error-boundary obligations.
- Client rendering is valid for some highly interactive or offline experiences; document the startup, failure, and unsupported-JavaScript behavior.
- A laboratory result from one device or network is not a universal performance claim.

## Completion

Deliver a route matrix, selected modes and rationale, data and cache boundaries, client-JavaScript budget, failure and fallback behavior, performance evidence or POC plan, operational and cost consequences, ADR links, and re-evaluation triggers.
