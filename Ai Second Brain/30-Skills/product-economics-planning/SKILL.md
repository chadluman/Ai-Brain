---
name: product-economics-planning
description: Build an auditable product delivery and operating-cost model with ranges, unit economics, schedule effects, ownership, scenarios, and update triggers. Use for budget decisions, architecture comparisons, pricing inputs, scale planning, or deciding whether a product is economically sustainable.
---

# Product Economics Planning

## Outcome

Create a traceable economic model that connects delivery work and recurring service costs to demand, capacity, schedule, risk, and business outcomes, while making uncertainty and decision boundaries visible.

## Required Inputs

- decision, product scope, service period, lifecycle stage, currency, geography, and accounting boundary
- delivery plan, people and vendor assumptions, dependencies, milestones, and support model
- architecture candidates, environments, demand scenarios, retention, data growth, and reliability targets
- provider pricing evidence, contracts, taxes, discounts, quotas, and commitment terms when available
- measurable service or business unit, expected volume, revenue or outcome hypothesis, and current baseline
- budget ceiling, cash timing, contingency policy, owners, and review cadence

## Safety and Permission Constraints

- Label actuals, quoted prices, public list prices, estimates, assumptions, exclusions, and contingencies separately. Never present a point estimate as certainty.
- Recheck current provider pricing, region, units, taxes, transfer, support, minimums, free-tier conditions, and contract terms before a decision. Do not infer future prices.
- Include labor, testing, security, accessibility, compliance, operations, observability, support, migration, downtime, lock-in, and exit costs where material; do not optimize only the visible cloud bill.
- Do not create paid resources, accept contracts, purchase commitments, change budgets, or expose private billing data without authorization. Treat financial and regulated decisions as requiring qualified review.
- A favorable model does not approve an architecture, provider, price, or launch. Route those decisions through their relevant ADR and approval gates.

## Workflow

1. Define the decision, scope, service period, output unit, cost boundary, owners, exclusions, and required accuracy.
2. Build a work and service breakdown that connects scope to delivery activities, environments, runtime components, support, and retirement. Avoid double counting shared work.
3. Establish a technical and schedule baseline. Identify dependencies, critical timing assumptions, provisioning lead times, and how delay changes cost or value.
4. Estimate each cost driver from traceable evidence. Use an appropriate method, a low/base/high range, confidence, source date, and explicit quantity and rate.
5. Model demand and architecture scenarios, including idle minimum, expected use, peak or growth, failure headroom, non-production, data growth, transfer, logging, backup, and support.
6. Allocate direct and shared costs with documented rules. Choose a stable, decision-useful unit such as cost per active account, completed transaction, supported tenant, or successful outcome.
7. Compare marginal cost and, where appropriate, marginal revenue or outcome value. Test sensitivity to the few assumptions that can reverse the decision.
8. Add risk and contingency without hiding known scope. Show cash timing, commitments, cancellation or exit exposure, and the effect of schedule slippage.
9. Present alternatives using the same boundary and period. Explain nonfinancial consequences such as reliability, portability, accessibility, security, staff load, and time to learn.
10. Assign forecast owners and a review cadence. Compare forecast to actuals after milestones and operation; explain variance, update the model, and retain the original baseline.

## Required Output

- decision, scope, period, currency, cost boundary, owners, and exclusions
- work and service breakdown with technical and schedule baseline
- traceable cost-driver table with quantity, rate, source, date, range, and confidence
- low/base/high demand and cost scenarios plus sensitivity analysis
- allocation rules, unit-cost definition, and relevant revenue or outcome relationship
- cash, commitment, contingency, exit, and schedule-risk view
- recommendation, decision thresholds, variance plan, and re-estimation triggers

## Completion Gate

Do not call the estimate decision-ready until another reviewer can reproduce its arithmetic, material lifecycle costs and exclusions are visible, alternatives share the same boundary, uncertainty can change the recommendation, and owners will reconcile the forecast with actuals.

## Conditional Reference

Read [Product Economics Evidence](references/product-economics-evidence.md) when defining a cost boundary, estimate structure, schedule risk, forecast, allocation, or unit metric.
