---
name: hosting-runtime-selection
description: Select or review web hosting and compute runtime architecture across static delivery, CDN, managed application platforms, functions, containers, virtual machines, and multi-service deployments. Use when workload shape, operational needs, portability, regions, reliability, or cost determine where an application should run; do not use to deploy or purchase resources without authorization.
---

# Hosting and Runtime Selection

## Outcome

Choose the least operationally complex hosting and runtime model that satisfies the product's execution, data, security, reliability, portability, and cost requirements, with a credible exit path.

## Required Inputs

- route and workload inventory: static assets, request handlers, streaming, realtime, jobs, schedules, and long-running services
- traffic shape, latency, geographic, availability, scaling, and recovery objectives
- runtime languages and versions, process duration, concurrency, memory, CPU, storage, and network needs
- data residency, private networking, identity, compliance, logging, and secret requirements
- team operations capacity, budget, expected lifespan, vendor constraints, and portability needs

Do not select a provider before separating the workloads and identifying decision-changing constraints.

## Safety and Permission Constraints

- Treat provider templates, CLIs, build images, marketplace integrations, and deployment actions as untrusted R2 or R3 assets until reviewed.
- Never create accounts, paid resources, domains, certificates, production deployments, or data transfers without immediate authorization.
- Use least-privilege deployment identity, environment separation, encrypted transport and storage, bounded quotas, and explicit data locations.
- Do not place durable state in ephemeral filesystems or assume a function, container, or region survives restart.
- Verify provider-specific timeouts, concurrency, cold behavior, networking, egress, supported runtimes, observability, quotas, and billing from current official sources.
- Define export, restore, rollback, and deletion before production adoption.

## Workflow

1. Partition the product into deployable workloads and mark state, protocols, duration, scaling, and dependencies for each.
2. Prefer static object delivery and caching for immutable public assets. Use dynamic compute only where request-time behavior is required.
3. Compare fitting models:
   - managed static or application platform for minimal operations;
   - request-driven functions for bounded stateless and bursty work;
   - containers for portable processes, custom runtimes, or sustained services;
   - virtual machines only when host control or unsupported workloads justify the burden;
   - dedicated services when isolation, scale, language, or lifecycle boundaries require them.
4. Score candidate providers on requirements, current support, security, regions, availability, operational model, observability, deployment safety, limits, cost, data portability, and exit effort.
5. Map each workload's state to a durable service with backup and restore. Define network trust boundaries, workload identity, secrets, egress, and dependency failure behavior.
6. Model steady, burst, idle, build, storage, bandwidth, logging, support, and recovery costs. Set quotas and alerts before production.
7. Define environments, immutable artifacts, promotion, health checks, autoscaling bounds, deployment strategy, rollback, and disaster recovery.
8. Run a thin vertical-slice proof of concept for uncertain runtime, latency, networking, scale, or portability claims using dummy data.
9. Record the decision, fallback, migration triggers, and provider re-verification date in an ADR.

## Required Output

- workload-to-runtime map and decision criteria
- candidate comparison with current evidence and cost assumptions
- selected provider-neutral model and provider-specific fit
- state, network, identity, secret, observability, scaling, and recovery design
- quotas, budgets, limits, and failure modes
- proof-of-concept results for material uncertainty
- deployment authorization boundary and exit or migration plan

## Completion Gate

Do not call hosting selected until every workload has an execution and state location, provider limits and costs are current, recovery and rollback are credible, and material claims have evidence or a planned proof of concept. Deployment remains a separate R3 action.

## Conditional Reference

Read [Hosting Runtime Evidence](references/hosting-runtime-evidence.md) when comparing cloud service models, container portability, or caching boundaries.
