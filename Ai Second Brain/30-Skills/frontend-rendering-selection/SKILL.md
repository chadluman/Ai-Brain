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

## Guardrails

- Do not select a framework first and retrofit its preferred rendering model to every route.
- Search-engine visibility is one constraint, not the only reason to send meaningful HTML.
- Streaming can improve progressive delivery but does not remove data-fetching, caching, hydration, accessibility, or error-boundary obligations.
- Client rendering is valid for some highly interactive or offline experiences; document the startup, failure, and unsupported-JavaScript behavior.
- A laboratory result from one device or network is not a universal performance claim.

## Completion

Deliver a route matrix, selected modes and rationale, data and cache boundaries, client-JavaScript budget, failure and fallback behavior, performance evidence or POC plan, operational and cost consequences, ADR links, and re-evaluation triggers.
