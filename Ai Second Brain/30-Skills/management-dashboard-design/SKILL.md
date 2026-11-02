---
name: management-dashboard-design
description: Design or review operational and management dashboards that connect trustworthy metrics to specific decisions, comparisons, drill-downs, alerts, and accountable actions. Use for KPI and portfolio views; do not use for privileged user-account mutations or as a substitute for analytics event design.
---

# Management Dashboard Design

## Outcome

Produce a decision-oriented dashboard whose audience can understand what changed, whether the evidence is trustworthy and current, why it matters, and what authorized action or investigation follows without mistaking a visualization for the underlying system of record.

Use [Analytics and Experimentation Design](../analytics-experimentation-design/SKILL.md) for event and outcome measurement, [Observability and SLO Design](../observability-slo-design/SKILL.md) for service telemetry and alerts, [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for personal-data boundaries, and [User Administration Console](../user-administration-console/SKILL.md) when a view leads to privileged user operations.

## Required Inputs

- audiences, decisions, review cadence, questions, accountable owners, escalation paths, and actions the dashboard should support
- goals, metric definitions, targets, guardrails, baselines, comparison periods, segments, and known interpretation risks
- authoritative sources, lineage, grain, time zone, attribution, late-arriving data, revisions, freshness, completeness, quality checks, and reconciliation
- access roles, tenant or organizational scope, sensitive dimensions, small-cohort risk, retention, export, sharing, and publication boundaries
- screen, device, accessibility, localization, presentation, refresh, performance, and operational constraints

If no decision changes when a metric changes, remove the metric from the primary dashboard or state its separate reporting purpose.

## Safety and Permission Constraints

- Do not present a proxy, forecast, sampled value, cached aggregate, experimental metric, or incomplete period as authoritative fact. Label definition, scope, source, freshness, revision behavior, and uncertainty where they affect interpretation.
- Preserve denominator, unit, time basis, inclusion and exclusion rules, comparison basis, and target semantics. Do not use truncated axes, incompatible scales, cherry-picked windows, cumulative-period comparisons, or color-only status to imply a conclusion the data does not support.
- Apply least-privilege access to every metric, dimension, drill-down, query, export, alert, and cached result. Aggregation is not automatically anonymous; suppress, bucket, or restrict small and sensitive cohorts.
- Do not rank or penalize people using unvalidated proxies, opaque scores, incomplete attribution, or metrics they cannot inspect and contest. Separate descriptive evidence from decisions that require policy, investigation, or qualified review.
- A dashboard may link to an action but must not bypass the action's authorization, confirmation, approval, audit, or recovery controls.
- Connecting production data, widening access, publishing a dashboard, exporting sensitive records, changing live alerts, or taking consequential action from dashboard data is R3 and requires immediate authorization, exact scope, monitoring, and rollback or revocation.

## Workflow

1. Start with an audience-decision inventory. For each question define the decision, decision owner, cadence, acceptable latency and error, evidence needed, action threshold, and what the dashboard must not be used to decide.
2. Write a metric contract before composing cards or charts: plain-language meaning, formula, numerator and denominator, unit, grain, scope, population, exclusions, source, attribution window, event time versus processing time, time zone, aggregation, target, guardrails, revision policy, owner, and version.
3. Prove lineage and quality from source to display. Reconcile important aggregates to systems of record, define duplicate, missing, late, corrected, and backfilled behavior, expose data-quality failures, and keep the previous trustworthy state distinguishable from a current partial state.
4. Organize the dashboard from decision summary to explanation and action. Lead with a small set of status and trend signals, then comparisons, contributors, segments, drill-downs, definitions, and next steps. Give stable URLs or shareable state only within access and privacy boundaries.
5. Choose the least complex representation that answers the question. Use direct values for current status, tables for exact comparison, and familiar charts for patterns over time or categories. Avoid decorative gauges, three-dimensional effects, dual axes, and interactions that hide essential meaning behind hover.
6. Give every view context: title as a question or conclusion, current value, unit, period, baseline or target, direction and magnitude of change, definition version, source, last successful refresh, coverage or completeness, active filters, and a plain-language interpretation.
7. Make filtering and comparison explicit. Define default period and scope, time zone, segment compatibility, reset behavior, URL state, empty combinations, comparison validity, and whether totals recompute. Prevent a filter from silently changing denominators or mixing incompatible cohorts.
8. Separate dashboards, reports, and alerts. Use dashboards for recurring decisions and investigation, reports for scheduled context-rich snapshots, and alerts for bounded changes that require attention. Every alert needs an owner, threshold rationale, deduplication, suppression, escalation, and recovery signal.
9. Provide accessible equivalents. Use semantic headings and tables, programmatic names, visible focus, sufficient contrast, non-color encodings, text summaries of meaningful trends, and access to exact underlying values. Support zoom, reflow, keyboard, screen reader, reduced motion, print or presentation use where required, and long localized labels.
10. Design loading, no-data, not-applicable, insufficient-sample, delayed, stale, partial, corrected, permission-denied, source-outage, and query-failure states. Never display zero when the value is missing or not yet computed.
11. Validate with representative decision makers and independent metric owners. Test comprehension, false conclusions, accessibility, source reconciliation, filter and time-zone correctness, export parity, access control, performance, stale-state behavior, alert routes, and an incident or unusual-period scenario.
12. Review use after launch. Remove unused tiles, revise misleading definitions through versioned change, record decision outcomes and false alarms, and re-evaluate access, cost, and retention as audiences or sources change.

## Required Output

- audience, decision, question, cadence, owner, threshold, and prohibited-use inventory
- versioned metric dictionary with formulas, lineage, freshness, quality, comparisons, targets, guardrails, and revision rules
- dashboard information architecture, layout rationale, drill-down and filter contracts, stable-link behavior, and complete state matrix
- chart and table specifications with textual interpretations, accessible equivalents, responsive behavior, and localization constraints
- access, privacy, small-cohort, cache, export, sharing, alert, and action handoffs
- reconciliation, comprehension, accessibility, performance, permission, stale-data, and incident-scenario test evidence

## Completion Gate

Do not call the dashboard ready until every primary element serves a named decision, metrics have versioned definitions and accountable owners, displayed values reconcile within stated tolerances, freshness and missingness cannot be confused with success or zero, comparisons are valid, access and small-cohort risks are controlled, visual meaning has accessible equivalents, and consequential actions retain their own authorization and recovery gates.

## Conditional Reference

Read [Management Dashboard Design Evidence](references/management-dashboard-design-evidence.md) when defining dashboard metrics, data visualizations, exact tables, accessible alternatives, freshness and context, or the distinction among dashboards, reports, and alerts.
