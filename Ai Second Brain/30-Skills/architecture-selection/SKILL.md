---
name: architecture-selection
description: Select and document a fit-for-purpose architecture for a new or materially changing web, mobile, or application project. Use when requirements must be translated into compared technology choices and ADRs; do not use for routine implementation in an already-decided stack.
---

# Architecture Selection

## Outcome

Produce a current, evidence-backed, minimally sufficient architecture that fits the specific project's product, delivery, security, cost, maintenance, and portability constraints.

## Inputs

Read the root `AGENTS.md` and the project's intake brief. If no brief exists, create one from `60-Templates/Project Intake.md` using known facts and clearly marked assumptions.

Resolve only gaps that could materially change architecture, cost, risk, or scope. Continue with reversible assumptions when safe; do not invent hard requirements.

## Workflow

1. Classify the delivery stage and highest applicable risk level.
2. Identify the architecture domains the project actually needs: clients, rendering, backend, data, identity, integrations, AI, economic systems, infrastructure, delivery, and operations.
3. Separate non-negotiable gates from preferences.
4. Research credible current candidates through primary sources. Verify capabilities, support status, compatibility, pricing, limits, licensing, security guidance, export paths, and material operational constraints.
5. Compare only options that pass the gates. Use [the decision matrix](references/decision-matrix.md) when two or more credible candidates remain and structured comparison will clarify the decision.
6. Select the smallest complete architecture. Prefer open standards, portable data, replaceable boundaries, and managed operational burden when fit is otherwise comparable.
7. Record each material choice with `60-Templates/Technology ADR.md`. Keep independent decisions in separate ADRs when they can change independently.
8. Define a thin vertical slice that tests the riskiest important assumptions end to end.

## Architecture Shape (2026 Currency)

The sources reviewed in November 2026 reverse the earlier microservices-by-default stance: start with the smallest deployable that fits, and split only on evidence.

- **Default to a modular monolith.** One deployable unit with enforced internal module and domain boundaries — see [Codebase Module Boundaries](../codebase-module-boundaries/SKILL.md) — keeps deployment, debugging, and transactions simple while preserving the option to extract a service later.
- **Avoid the distributed monolith.** Services deployed separately but tightly coupled — sharing databases, releasing in lockstep, failing together — pay distribution costs without independence. If services cannot deploy, scale, or fail independently, they are one system pretending to be several; prefer the monolith until independence is real.
- **Team-size heuristics (secondary sources, not rules).** A single small team (roughly 1–5 people) fits a monolith; a growing single team (roughly 3–15) fits a modular monolith; separately deployed services fit when multiple teams contend on one codebase, release coordination becomes the bottleneck, or scaling profiles differ sharply. Treat the ranges as starting points, not thresholds that decide the question alone.
- **Strangler-fig extraction triggers.** Extract a service only when a specific boundary shows specific pressure: scaling needs an order of magnitude apart, a team blocked on release coordination, or a component needing an independent lifecycle. Migrate by proxying traffic and moving one route at a time rather than a big-bang rewrite, and record each extraction in an ADR with a rollback plan.

Evidence note: a 2026 industry article cites a CNCF survey figure (42%) for organisations that adopted microservices and later consolidated some services back. The underlying survey was not opened in this research, so treat the figure as unverified and do not cite it as fact; the direction of the consensus reversal is the usable finding, not the number.

## Safety and Permission Boundaries

- Treat third-party code, skills, extensions, templates, and dependencies as untrusted until they pass the root security-review gate.
- Research and recommendations do not authorize installation, account creation, paid resources, credential creation, data transmission, deployment, publication, or destructive changes.
- Never place secret values in the vault, examples, commands, logs, or diagrams.
- Use authoritative current sources for regulated, financial, medical, legal, privacy, or safety-critical requirements and call out the need for qualified review.
- Economic balances, credits, or stored value require an auditable ledger design and explicit reconciliation and correction behavior.

## Decision Quality

- Do not equate new, popular, expensive, or feature-rich with best.
- Treat scores as decision aids, not objective truth. Explain decisive tradeoffs in plain language.
- Prefer a short proof of concept or benchmark when a high-impact claim remains uncertain.
- State what was verified, the verification date, what is inferred, and what remains unknown.
- Include an exit path when vendor lock-in, pricing volatility, data gravity, or service discontinuation is material.
- Stop researching when the decision criteria are satisfied; more sources are not automatically more confidence.

## Required Deliverable

Return or create:

- Executive recommendation and important assumptions
- System boundaries and data flow, with a diagram only when it adds clarity
- Technology choices with decisive rationale and dated primary evidence
- Material ADRs and rejected alternatives
- Security, privacy, reliability, accessibility, and cost implications
- POC or vertical-slice plan with measurable success thresholds
- External accounts, expected costs, and R3 approval boundaries
- Known unknowns, exit strategy, and re-evaluation triggers

Do not present the architecture as approved or implementation-ready until required gates, evidence, and user decisions are complete.

