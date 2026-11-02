# Rendering Tradeoffs

Verified 2026-10-21. Framework terminology varies; define the observable behavior rather than relying on a product label.

| Mode | Strong fit | Main costs and failure modes |
|---|---|---|
| Static or prerendered HTML | Public, cacheable content whose acceptable freshness can be defined at build or regeneration time | Build duration, invalidation, stale content, and accidental inclusion of private data |
| Server rendering | Request-dependent or fresh HTML, personalized entry states, and broad device support | Server latency and compute, origin dependency, cache safety, and operational load |
| Streamed server rendering | Pages whose meaningful regions become ready at different times | Boundary design, partial failures, ordering, cache complexity, and client hydration coordination |
| Client rendering | Interaction-heavy authenticated tools, offline-capable applications, and journeys where an app shell is acceptable | JavaScript startup, blank or incomplete failure states, device CPU cost, data waterfalls, and discoverability constraints |
| Hybrid or islands | Mostly stable HTML with isolated interactive regions or route-specific needs | Multiple execution models, boundary and state coordination, duplicated dependencies, and debugging complexity |

Google's [Rendering on the Web](https://web.dev/articles/rendering-on-the-web), last updated 2026-01-05 when verified, defines SSR, CSR, prerendering, and hydration and explains their performance tradeoffs. It is current Chrome-team guidance, not a normative standard or a project-independent verdict.

## Evidence Questions

- What meaningful content and controls are present before client JavaScript executes?
- How many bytes and how much main-thread work precede the critical action?
- Which data can be cached, for whom, for how long, and how is it invalidated?
- What happens during origin failure, JavaScript failure, slow data, an interrupted stream, or offline use?
- Can the deployment and monitoring model isolate failures and roll back each route class safely?

Use the project's performance plan and real-user evidence where available. Treat a single Lighthouse run or framework benchmark as diagnostic, not decisive.
