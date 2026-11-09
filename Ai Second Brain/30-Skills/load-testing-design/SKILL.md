---
name: load-testing-design
description: Design load, stress, spike, and soak tests with percentile latencies, realistic traffic, a production-like environment, and CI thresholds that re-baseline after infrastructure changes. Use when deciding whether a system holds up under expected and extreme load.
---

# Load Testing Design

## Outcome

Produce a load-testing practice that answers, with evidence, whether the system meets its latency and error targets under expected peak load — and where it breaks when load goes beyond that. The output is a repeatable test suite with stated thresholds, not a one-off report before launch.

Use [Test Strategy Design](../test-strategy-design/SKILL.md) to place load tests in the wider test portfolio, [Web Performance Plan](../web-performance-plan/Web%20Performance%20Plan.md) for user-centred performance budgets, and [Capacity and Cost Planning](../capacity-cost-planning/Capacity%20and%20Cost%20Planning.md) for turning load results into capacity and cost decisions.

## Snapshot and re-check

Research for this skill was checked 2026-11-09. Treat load-testing practice as durable, but re-check tool versions, platform features, and policy dates before citing them — they are a 2026-11-09 snapshot and may have moved on.

## Test types

Four types answer four different questions; running only one leaves the others unanswered:

- **Load** — expected peak traffic. Does the system meet its latency and error targets at the load it is actually built for?
- **Stress** — keep raising load past the peak until something breaks. The point is to find the breaking point and how the system fails, not to pass.
- **Spike** — a sudden surge, several times normal load, then a drop. Does the system absorb it and recover cleanly, or does it cascade?
- **Soak** — sustained load over a long period, commonly 2–24 hours. This is where memory leaks, connection-pool drift, and slow degradation show up — the failures a short test never sees.

## What to measure

Measure percentiles, never the mean alone: p50, p95, and p99 latency, plus throughput (requests per second), error rate, concurrency, and saturation of CPU, memory, and the database. The mean hides the experience of the slowest users; a good mean with a bad p99 is a system that fails a real fraction of its users while the headline number looks fine. Record the same measures for the dependencies the test touches, so a slow database or a saturated downstream service is visible rather than blamed on the app tier.

## Tools

Common tools in current use, each with a different fit: k6 (scripted in JavaScript/TypeScript, CI-friendly thresholds, a non-zero exit code on threshold failure), Locust (Python, good for teams already in Python), Apache JMeter (broad protocol coverage, a graphical interface, the enterprise legacy choice), Gatling (JVM-based, code-as-test), plus Artillery and Vegeta for lighter or constant-rate checks. For front-end performance under load, use Lighthouse and WebPageTest rather than a protocol-level load tool. Choose the tool the team will actually maintain; a load suite in a language nobody on the team reads will rot.

## Realistic load and environment

Derive the load profile from real traffic, not round numbers: peak requests per second, the mix of users and request types, and the endpoints that actually matter — sign-in and token refresh, checkout or the core transaction, and any fan-out such as notifications. A test that hammers one cheap endpoint proves little about a system whose real bottleneck is a different path.

Run the test against a production-like environment, not a developer laptop: same service topology, same versions, production-like data volume. A test run on a laptop measures the laptop. Keep load tests isolated from production systems unless a separately authorized, non-destructive production check is designed for that purpose — never point a load generator at production by accident.

## CI thresholds and re-baselining

Gate CI on thresholds rather than on vibes — for example, a p95 latency bound and an error-rate bound, with the actual numbers set from the system's own targets, not copied from an example. A threshold failure should block the change the way a failing unit test does. Re-baseline after infrastructure changes: a new runtime, a resized database, a changed cache policy, or a new dependency all shift what "normal" looks like, and a threshold set against the old baseline will either cry wolf or miss a real regression. Load testing is a routine CI activity, not a one-off exercise before launch.

## Failure modes

- Testing with round-number load that matches no real traffic pattern.
- Judging by the mean latency while p99 quietly degrades.
- Running the suite once before launch and never again, so the thresholds describe a system that no longer exists.
- Treating a passing load test as a guarantee: it is evidence about the tested profile in the tested environment, not a promise about untested traffic.

## Supporting skills

- [Test Strategy Design](../test-strategy-design/SKILL.md) — placing load tests in the test portfolio and defining entry and exit criteria.
- [Web Performance Plan](../web-performance-plan/Web%20Performance%20Plan.md) — user-centred performance budgets and field measurement.
- [Capacity and Cost Planning](../capacity-cost-planning/Capacity%20and%20Cost%20Planning.md) — turning load results into capacity, scaling, and cost decisions.
- [Observability and SLO Design](../observability-slo-design/Observability%20and%20SLO%20Design.md) — the telemetry and SLOs that load-test thresholds should mirror.

## State

Risk: R0 (draft).
Draft pending representative validation.
