# Architecture Decision Matrix

Use this reference only when two or more credible options pass the project's non-negotiable gates and a structured comparison will improve the decision.

## Method

1. Derive criteria and weights from the project intake rather than using universal defaults.
2. Mark hard gates first. Do not allow a high weighted score to rescue a disqualified option.
3. Score remaining options from 0 to 5 using current cited evidence:
   - `0`: cannot meet the criterion
   - `1`: severe weakness or major unsupported work
   - `2`: material weakness
   - `3`: adequate
   - `4`: strong fit
   - `5`: exceptional fit with evidence
4. Multiply each score by its weight, then compare totals and sensitivity to uncertain assumptions.
5. Explain the decisive tradeoffs. Do not select mechanically from the total.

## Candidate Criteria

Choose only relevant criteria:

| Criterion | What to examine |
|---|---|
| Product fit | Required workflows, platforms, rendering, offline/realtime, integrations, and roadmap |
| Security and privacy | Threat model, controls, advisory history, data handling, residency, and least privilege |
| Compliance | Required certifications, contractual support, auditability, retention, and deletion |
| Accessibility | Standards support, component behavior, testing surface, and known constraints |
| Performance | Latency, throughput, client weight, startup, caching, and measured limits |
| Reliability | Availability model, failure isolation, recovery, durability, and operational maturity |
| Developer fit | Team knowledge, documentation, debugging, testing, tooling, and hiring market |
| Ecosystem health | Maintenance, release cadence, governance, compatibility, and dependency quality |
| Interoperability | Standards, APIs, data formats, integration surface, and replacement boundaries |
| Portability | Export, migration, self-hosting feasibility, lock-in, and data gravity |
| Delivery speed | Setup, iteration loop, available components, and vertical-slice effort |
| Operational burden | Deployment, scaling, monitoring, upgrades, incidents, backups, and support |
| Total cost | Build, service, compute, storage, bandwidth, observability, support, and migration |
| Longevity | Support horizon, business stability, deprecation policy, and likely maintainability |

## Comparison Table

| Criterion | Weight | Option A score/evidence | Option B score/evidence | Option C score/evidence |
|---|---:|---|---|---|
|  |  |  |  |  |

## Evidence Rules

- Link each material factual claim to a primary source and include the verification date.
- Mark estimates, benchmarks from non-equivalent workloads, and inferences explicitly.
- Use a small proof of concept for claims that cannot be settled from reliable documentation.
- Record pricing assumptions such as region, usage, traffic, storage, seats, support tier, and taxes.
- Recheck any fact whose change could reverse the decision.

## Tie and Sensitivity Rules

When options are close:

- Prefer the smaller operational and dependency footprint.
- Prefer portable data and clearer exit paths.
- Prefer the option the maintaining team can operate safely.
- Change uncertain high-weight assumptions to plausible alternatives and see whether the decision reverses.
- If the decision remains unstable, run a narrowly scoped POC instead of claiming false certainty.

