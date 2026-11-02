---
name: product-discovery-scope
description: Turn an idea, request, or presumed solution into an evidence-backed problem statement, user journeys, measurable outcomes, constraints, risks, scope, and thin validation plan. Use before architecture selection or when a project is expanding without clear product evidence.
---

# Product Discovery and Scope

## Outcome

Create a decision-ready project brief that identifies the real user and business problem, the smallest coherent outcome to test, what is deliberately excluded, and what evidence would justify building, changing direction, or stopping.

## Required Inputs

- idea, sponsor intent, affected people, current journey, and existing evidence
- desired outcomes, harms to avoid, deadlines, budget, team, and operating constraints
- channels, regions, accessibility, privacy, security, compliance, and support needs
- known systems, data, integrations, alternatives, dependencies, and approval boundaries
- assumptions, uncertainties, irreversible choices, and cost of delay or failure

## Safety and Permission Constraints

- Do not invent user research, demand, market size, costs, legal conclusions, or stakeholder agreement. Label evidence, assumptions, estimates, and open questions separately.
- Research participation and collected artifacts can contain sensitive data. Use informed consent, minimization, access control, retention, and appropriate qualified review.
- Include disabled, low-connectivity, low-literacy, assisted, and non-digital journeys when they are part of the affected population.
- Discovery does not authorize account creation, paid research, contacting people, scraping, data purchase, or building a production system. Obtain authorization at those boundaries.
- A sound discovery may recommend no build, process change, reuse, procurement, or a smaller experiment. Do not force a software outcome.

## Workflow

1. Reframe the requested solution as the user and organizational outcomes that need to change. Describe the current state and the cost or harm of leaving it unchanged.
2. Identify affected user groups, actors, exclusions, accessibility needs, and the complete journey before, during, and after the proposed digital interaction.
3. Inventory existing research, support evidence, analytics, policy, systems, competitors or substitutes, prior attempts, and constraints. Record provenance and gaps.
4. Write falsifiable assumptions about desirability, usability, feasibility, viability, safety, operations, and adoption. Rank them by consequence and uncertainty.
5. Define measurable success and guardrail outcomes with a baseline, time horizon, decision owner, and data source. Avoid vanity metrics and proxy-only success.
6. Shape the smallest coherent end-to-end outcome. State in-scope, out-of-scope, non-goals, dependencies, deadlines, budget envelope, and external approvals.
7. Choose the cheapest safe evidence for the highest-risk assumption: interview, observation, service-data review, paper or interactive prototype, technical spike, or concierge test.
8. Record build, buy, reuse, integration, and no-build alternatives without selecting a stack. Identify irreversible and R3 decisions for later approval.
9. Define exit criteria for proceed, revise, pause, or stop, then hand the brief to architecture selection only when decision-changing unknowns are visible.

## Required Output

- problem and opportunity statement
- user groups, needs, critical journeys, inclusion needs, and existing alternatives
- evidence register with assumptions and uncertainty ranking
- success metrics, guardrails, baseline, and decision thresholds
- scope, non-goals, dependencies, constraints, budget, timeline, and ownership
- validation plan, stop conditions, risks, and authorization boundaries
- project brief suitable for architecture decisions

## Completion Gate

Do not call discovery sufficient until the problem is stated independently of a favored solution, the primary journey and excluded users are visible, success and stop criteria are measurable, and the highest-impact assumptions have an evidence plan.

## Conditional Reference

Read [Discovery Evidence](references/discovery-evidence.md) when defining user needs, service scope, discovery exit criteria, or measurable benefits.
