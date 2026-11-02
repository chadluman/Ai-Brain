# Capacity and Cost Evidence

Verified: 2026-10-21

## Primary Industry Sources

- [Google SRE introduction](https://sre.google/sre-book/introduction/) describes capacity planning as forecasting organic and inorganic demand beyond provisioning lead time, incorporating planned events, and regularly load testing the resource-to-service-capacity relationship.
- [Google SRE production best practices](https://sre.google/sre-book/service-best-practices/) recommends validating forecasts, deriving capacity from load tests, accounting for launch behavior, planning for failures, and designing graceful degradation and load shedding.
- [FinOps Framework: Allocation](https://framework.finops.org/framework/capabilities/allocation/) defines strategies for assigning direct and shared technology costs through ownership and metadata, and measuring unallocated spend.
- [FinOps Framework terminology](https://framework.finops.org/assets/terminology/) defines forecasting, demand drivers, direct, indirect, and shared cost, and usage optimization concepts.

## Decision Boundaries

- These sources supply reasoning patterns, not a universal redundancy number, cost target, or team structure. Project consequences and SLOs determine the margin.
- Provider list price is not total cost. Include request tiers, storage operations, transfer, logging, backups, support, taxes, discounts, minimums, engineering work, and exit cost.
- Autoscaling does not remove quotas, cold starts, initialization, connection limits, downstream bottlenecks, or the need for overload protection.
- Optimization without ownership and outcome metrics can transfer cost into reliability failures, staff toil, vendor lock-in, or user harm.
- Load-test results apply only to the tested code, data, topology, configuration, and traffic shape. Record all of them and re-run after material change.
