---
name: capacity-cost-planning
description: Forecast and validate service capacity, quotas, scalability, operating cost, unit economics, ownership allocation, overload controls, and spend guardrails. Use before launch, growth events, architecture commitments, vendor changes, or when reliability and cost are diverging.
---

# Capacity and Cost Planning

## Outcome

Create an evidence-based capacity and operating-cost model tied to user demand, service objectives, failure headroom, unit economics, and actionable controls rather than a single optimistic traffic or price estimate.

## Required Inputs

- critical journeys, SLOs, workloads, dependencies, regions, and failure modes
- current and forecast users, requests, storage, transfer, jobs, messages, model tokens, and growth events
- measured resource demand, latency curves, quotas, rate limits, lead times, and scaling boundaries
- provider pricing dimensions, discounts, minimums, taxes, support, egress, and operational labor
- budget, runway, cost owners, allocation metadata, alert thresholds, and acceptable degraded modes

## Safety and Permission Constraints

- Treat price pages, calculators, benchmarks, and historical bills as time-bound evidence. Record date, region, tier, currency, taxes, assumptions, and exclusions.
- Do not load-test production or a paid provider without authorization, traffic limits, data controls, provider-policy review, abort criteria, and spend caps.
- Do not reduce security, privacy, backup, recovery, accessibility, or required reliability solely to meet a cost target. Escalate the constraint and tradeoff.
- Paid reservations, commitments, scaling-limit increases, provider changes, broad load tests, or production load shedding are R3 and require immediate authorization and rollback or exit analysis.

## Workflow

1. Model demand by workload and time window, separating organic growth, known launches, abuse, retries, backfills, and recovery work. Record low, expected, high, and incident scenarios.
2. Define success from user-centered SLOs, latency targets, throughput, durability, freshness, and recovery needs. Identify the largest tolerable failure and required headroom.
3. Measure resource demand with representative data and requests. Find saturation points and latency curves for compute, memory, connections, storage, IOPS, network, queues, and downstream quotas.
4. Convert demand into required capacity with explicit redundancy, safety margin, autoscaling delay, regional constraints, provider quotas, and provisioning lead time.
5. Build a monthly and per-unit cost model covering fixed, variable, stepped, burst, egress, logs, backups, third parties, support, and human operations. Keep formulas and assumptions inspectable.
6. Allocate ownership with stable environment, product, team, and cost-center metadata. Define fair treatment of shared costs and surface unallocated spend.
7. Set budgets, anomaly alerts, rate and quota guards, per-tenant limits, log and retention controls, model-token limits, and approved escalation paths. Alert thresholds need an owner and response.
8. Define graceful degradation, admission control, queue bounds, load shedding, caching, and recovery behavior. Protect critical work before saturation.
9. Validate forecasts against actuals, load-test evidence, launch behavior, and invoices. Track unit cost, forecast error, headroom, saturation, unallocated cost, and cost per reliable user outcome.
10. Re-evaluate at material demand, architecture, price, quota, SLO, region, or feature changes; do not let one-time estimates become permanent truth.

## FinOps Discipline and Cost Traps

- Clean before committing: remove unused resources, right-size over-provisioned ones, and delete orphaned volumes, snapshots, and idle endpoints before buying reservations or committed-use discounts. A commitment on top of waste locks the waste in.
- Treat free tiers as time-bound traps, not permanent capacity: limits, eligibility windows, and included usage change without a product change on your side. One reported case is an RDS free-tier account cutoff in mid-July 2025. [secondary-sourced — not verified against AWS documentation; confirm current free-tier terms before relying on them.] Model what the workload costs at full price before depending on a free tier.
- Budget observability as a first-class cost: log volume, metric cardinality, trace retention, and query load scale with traffic and can exceed compute spend. The cardinality controls in [Observability and SLO Design](../observability-slo-design/SKILL.md) are cost controls, not only hygiene.
- Apply reserved and spot discipline together: reserve only steady-state baseline capacity you can measure, use spot or on-demand for variable and interruptible work, and re-check utilization against the commitment before renewing. An unused reservation is a fixed cost, not a saving.

## Required Output

- scenario-based demand forecast and assumptions
- measured resource-to-capacity model and bottleneck evidence
- redundancy, quota, headroom, scaling, and overload plan
- itemized monthly and unit-cost model with sensitivity ranges
- ownership allocation, budget, anomaly, and spend-control policy
- load-test plan, abort conditions, observed results, and forecast-error review
- commitment, portability, rollback, and provider-exit analysis

## Completion Gate

Do not call capacity and cost ready until critical workload limits are measured, the plan survives the defined failure scenario, cost assumptions are reproducible, shared and unallocated spend are visible, and overload plus spend controls have accountable operators.

## Conditional Reference

Read [Capacity and Cost Evidence](references/capacity-cost-evidence.md) when selecting forecasting, load-test, allocation, optimization, or overload controls.
