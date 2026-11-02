# Product Economics Evidence

Verified: 2026-10-21

## Primary and Maintainer Sources

- [UK Government: Service Costing in Government](https://www.gov.uk/government/publications/service-costing-in-government/service-costing-in-government) requires a defined service, time period, output or unit, cost structure, assumptions, limitations, accountability, and links from inputs to outputs and outcomes.
- [U.S. GAO Cost Estimating and Assessment Guide](https://www.gao.gov/products/gao-20-195g) describes a repeatable estimate process covering purpose and scope, technical baseline, work breakdown, assumptions, data, methods, sensitivity and risk, documentation, presentation, and updates using actual costs.
- [U.S. GAO Schedule Assessment Guide](https://www.gao.gov/products/gao-16-89g) explains why cost credibility depends on a reliable, integrated schedule and schedule-risk analysis.
- [FinOps Framework: Planning and Estimating](https://www.finops.org/framework/capabilities/planning-estimating/) treats estimates as scenario-based inputs to forecasts and calls for understood parameters, documentation, and planned updates.
- [FinOps Framework: Forecasting](https://www.finops.org/framework/capabilities/forecasting/) combines historical spend with future plans and service changes, then revisits estimates against actuals.
- [FinOps Framework: Unit Economics](https://www.finops.org/framework/capabilities/unit-economics/) connects allocated technology cost to a defined business unit and, where feasible, marginal revenue or value.

## Decision Boundaries

- GAO and government costing guidance is deliberately rigorous and should be scaled to the decision. A small reversible prototype needs a lighter model than a long-lived or regulated service, but still needs traceable assumptions.
- Provider calculators and list prices are inputs, not forecasts. Actual cost also depends on utilization, region, architecture, data transfer, observability, discounts, taxes, support, failure behavior, and human operation.
- A useful unit has a stable definition and a causal relationship to the service. Avoid vanity denominators that improve while the user outcome, reliability, or total cost worsens.
- Historical extrapolation alone misses launches, migrations, commitments, architecture changes, seasonality, and demand shocks. Forecasts need explicit future-plan inputs.
- Reconcile estimates with actuals without silently overwriting the baseline; variance is evidence about the model and the system.
