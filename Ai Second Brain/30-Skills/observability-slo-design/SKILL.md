---
name: observability-slo-design
description: Define service-level indicators and objectives, telemetry, dashboards, alerts, and diagnostic context around user-critical journeys. Use when launching or operating a service, reducing noisy alerts, or selecting logs, metrics, and traces; do not collect telemetry without a purpose and data review.
---

# Observability and SLO Design

## Outcome

Create a user-centered reliability model and minimal diagnostic telemetry that detects important harm, supports safe changes, and avoids uncontrolled cost or sensitive-data collection.

Read [observability evidence](references/observability-evidence.md) before selecting signal formats, propagation, or SLO methods.

## Inputs

Identify critical journeys and dependencies, user populations, expected traffic, acceptable failure and latency, business and safety consequences, existing telemetry, privacy and retention requirements, tenant boundaries, regions, deployment model, incident response, on-call capacity, and budget.

## Workflow

1. Define service boundaries and user-visible outcomes. Write an SLI as a measurable ratio or distribution with good events, valid events, data source, exclusions, window, and known bias.
2. Set an SLO from product need and achievable evidence. Define the error budget and the decisions it informs; avoid 100 percent targets unless failure is truly impossible by construction.
3. Instrument the smallest set of logs, metrics, traces, and events needed to measure the SLI and diagnose likely failures. Prefer interoperable context and stable semantic naming.
4. Classify every telemetry field. Exclude credentials, tokens, request bodies, personal data, tenant secrets, and high-risk identifiers by default; define redaction and access before collection.
5. Control metric label cardinality, log volume, trace sampling, retention, export destinations, and query cost. Preserve enough unsampled or tail evidence for rare critical failures where justified.
6. Build views from user impact to component cause: SLO and journey health, releases, dependencies, saturation, queues, and data freshness. Keep runbook links and ownership close to actionable alerts.
7. Alert on urgent, actionable user harm or fast error-budget burn. Route lower urgency trends to review rather than paging.
8. Test instrumentation and alerts through synthetic failures, deployment markers, sampling checks, clock and correlation behavior, backend outage, and retention or quota exhaustion.
9. Review false positives, missed incidents, cost, privacy, and unused signals; remove telemetry that does not support a decision.

## Safety and Scope

- Telemetry is production data. Exporting it to a third party, enabling session replay, or changing retention or access is R3 when real or private data is involved.
- Trace and request IDs can become correlation identifiers. Do not encode user or secret data in them.
- An SLO is a product reliability decision, not a vendor dashboard default or a guarantee to every user.
- Observability cannot repair missing failure handling, authorization, backups, or tests.

## Completion

Deliver the service and journey map, SLIs and SLOs, error-budget policy, signal and field inventory, privacy and retention controls, dashboards, actionable alerts and runbooks, cost controls, validation evidence, owners, and review triggers.
