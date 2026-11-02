---
name: backend-runtime-framework-selection
description: Select or review a backend language runtime and application framework from workload, deployment, support, security, ecosystem, team, and migration evidence. Use when choosing among server runtimes or frameworks for an API, web backend, worker, service, CLI, or scheduled workload.
---

# Backend Runtime and Framework Selection

## Outcome

Choose the smallest supported runtime and framework combination that fits the workload and operating model, with an upgrade path and evidence from a representative vertical slice.

## Required Inputs

- workload types, protocols, concurrency, CPU and memory profile, startup needs, latency targets, and throughput envelope
- delivery stage, lifespan, availability, scaling, deployment, portability, and compliance requirements
- data stores, queues, identity, observability, background work, native libraries, and third-party SDK requirements
- team skills, hiring and support constraints, build and debugging workflow, release capacity, and maintenance budget
- target operating systems, architectures, containers, functions, edge environments, or managed hosts
- existing code, interoperability needs, migration constraints, and acceptable vendor or ecosystem lock-in

## Safety and Permission Constraints

- Do not choose by popularity, synthetic benchmark, novelty, or language preference alone. Benchmark the actual critical path and include operational work.
- Reject end-of-life runtimes and unsupported runtime, framework, operating-system, architecture, database-driver, or deployment combinations unless an authorized exception has a time-bounded migration plan.
- Runtime installers, framework CLIs, templates, package managers, native extensions, containers, plugins, and dependencies are executable assets requiring exact-version review.
- Confirm licenses for the runtime distribution, framework, libraries, build tools, and production support. A language name does not determine the license or support terms of a vendor build.
- Do not transmit source, production data, credentials, or telemetry to hosted build, error, or AI services without explicit review and authorization.
- Provisioning paid infrastructure or deploying a public or production service is R3 and requires immediate authorization and rollback steps.

## Workflow

1. Write a workload profile with critical paths, resource shape, protocols, state, concurrency, failure behavior, security boundaries, and deployment constraints.
2. Define non-negotiable compatibility: supported runtime line, target OS and architecture, hosting support, framework and driver support, patch cadence, and end-of-support horizon.
3. Shortlist the smallest credible set, including no full framework or an existing organizational stack where it meets the requirements.
4. Compare exact runtime, distribution, framework, and key library versions on lifecycle, security response, type and memory safety, concurrency model, startup, resource use, diagnostics, testing, dependency surface, ecosystem health, portability, and licensing.
5. Evaluate framework value by required features actually used. Count generated code, middleware, reflection or magic, transitive dependencies, upgrade coupling, and escape hatches as costs.
6. Map build, package, configuration, secret, migration, observability, profiling, deployment, rollback, and incident-debugging paths. Verify that the team can operate them.
7. Build a thin vertical slice through the hardest integration. Measure representative startup, latency distribution, throughput, memory, CPU, error behavior, build time, artifact size, and operator diagnostics.
8. Run failure and maintenance exercises: dependency outage, timeout, cancellation, graceful shutdown, overload, runtime patch, framework minor or major upgrade, and rollback.
9. Record the choice in an ADR with rejected options, measured evidence, total operating cost, support dates, upgrade owner, and an exit boundary around framework-specific code.

## Required Output

- workload and compatibility profile
- exact-version runtime, distribution, and framework comparison
- support, license, vulnerability, dependency, and hosting evidence
- vertical-slice measurements and failure results
- build, deploy, observe, profile, patch, upgrade, and rollback plan
- ADR with tradeoffs, cost, ownership, and migration boundary

## Completion Gate

Do not call the stack selected until the exact candidate versions support every required target and critical integration, the representative slice has measured normal and failure behavior, and the team has demonstrated a supported patch, diagnostics, and rollback path.

## Conditional Reference

Read [Backend Runtime and Framework Evidence](references/backend-runtime-framework-evidence.md) before comparing current support claims. Use [Hosting and Runtime Selection](../hosting-runtime-selection/SKILL.md) for deployment topology and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) before adopting packages or images.
