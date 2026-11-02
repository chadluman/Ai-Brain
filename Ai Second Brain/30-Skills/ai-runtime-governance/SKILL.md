---
name: ai-runtime-governance
description: Operate an AI feature in production across version control, telemetry, privacy, latency, availability, token and cost budgets, rate limits, fallbacks, provider changes, canaries, incidents, user recourse, and retirement. Use after architecture and evaluation thresholds exist; do not collect prompts or outputs by default merely for observability.
---

# AI Runtime Governance

## Outcome

Produce an operable AI service with attributable versions, privacy-minimized signals, bounded resource use, measurable service and quality objectives, controlled changes, safe degradation, and a tested shutdown and exit path.

## Required Inputs

- task contract, users, critical journeys, unacceptable outcomes, evaluation thresholds, and accountable owners
- providers, exact model identifiers, prompts, policies, tools, retrieval corpus, routing, regions, quotas, and lifecycle guarantees
- request volume, burst, context, output, tool-loop, latency, availability, quality, and cost budgets
- data classifications, provider retention and training terms, telemetry purpose, sampling, access, residency, and deletion needs
- fallbacks, deterministic or human alternatives, incident paths, vendor exit, export, and decommission obligations

## Safety and Permission Constraints

- Route architecture and provider choice through [AI Feature Architecture](../ai-feature-architecture/SKILL.md) and release quality through [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md). This skill owns production operations.
- Do not log full prompts, outputs, retrieval passages, system instructions, tool arguments, or memory by default. Prefer identifiers, sizes, classifications, hashes, and derived measures; opt in to content only with purpose, authorization, redaction, access, and retention controls.
- Treat provider model aliases and silent behavior changes as change risk. Record the model actually returned when available and re-evaluate material drift.
- Do not retry non-idempotent tools or expensive generations blindly. Bound attempts, tokens, time, concurrency, queue depth, and spend per request, user, tenant, and period.
- Production provider activation, sensitive-data routing, cross-region transfer, large spend, real-user experimentation, or emergency policy bypass is R3 and requires immediate authorization and rollback.

## Workflow

1. Create a deployable version tuple: application, model and provider, endpoint or region, prompt, policy, tool schemas, retrieval corpus and index, grader, feature flags, and runtime configuration.
2. Define service and quality objectives separately. Track availability, time to first and final response, queue time, timeout, provider and tool errors, token use, cost, and the task-specific quality and critical-failure measures that matter.
3. Design privacy-minimized telemetry and an explicit content-capture mode. Classify every field, cap cardinality, sample intentionally, redact before export, restrict access, set retention and deletion, and test that secrets and private source content do not leak.
4. Meter resource use before provider calls. Enforce input, context, output, iteration, tool, concurrency, and cost limits; apply user and tenant quotas, admission control, backpressure, and abuse controls.
5. Define routing and fallback semantics. Compare pinning, quality or cost tiers, regional routing, hedging, caching, smaller models, deterministic workflows, queues, and human escalation. Never silently downgrade a safety or data-residency property.
6. Model provider and dependency failure: rate limits, slow streams, partial output, malformed structure, unavailable model, quota exhaustion, policy refusal, price or terms change, revoked credentials, regional outage, and tool or retrieval failure.
7. Gate every change with representative evals, non-production integration, canary exposure, version-attributed telemetry, automatic and manual rollback criteria, and an independent kill switch. Do not combine unrelated model, prompt, corpus, and policy changes without need.
8. Reconcile usage and cost. Compare application meters, provider usage, invoices, retries, cache behavior, tool costs, and tenant allocation; alert on anomalies and denial-of-wallet patterns.
9. Run incident response with AI-specific evidence, privacy controls, provider escalation, user communication and recourse, correction, rollback, and regression cases. Preserve only necessary evidence under controlled access.
10. Test provider exit and retirement. Export permitted configuration and evidence, switch to the fallback, drain requests, revoke credentials, delete provider data and derived stores, preserve required audit records, and verify that users receive a safe non-AI path.

## Required Output

- version and ownership registry with provider lifecycle and re-evaluation triggers
- service, quality, safety, latency, availability, and cost objectives
- telemetry schema, data classification, sampling, redaction, access, retention, and deletion plan
- quotas, budgets, admission, retry, timeout, routing, fallback, and degradation design
- change gate, canary, rollback, kill-switch, incident, and user-recourse procedures
- usage and invoice reconciliation, provider-exit, data-deletion, and retirement evidence plan

## Completion Gate

Do not call the AI runtime operational until version attribution works end to end, privacy controls prevent unintended content capture, budgets and denial-of-wallet defenses are enforced, provider and dependency failures degrade safely, canary and rollback paths pass, production quality has accountable monitoring, and fallback plus provider exit are tested.

## Conditional Reference

Read [AI Runtime Governance Evidence](references/ai-runtime-governance-evidence.md) when selecting telemetry fields, cost controls, risk processes, or production change gates.
