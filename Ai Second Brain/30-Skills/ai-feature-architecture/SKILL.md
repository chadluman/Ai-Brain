---
name: ai-feature-architecture
description: Design or review an AI-powered product feature across use-case fit, model and provider selection, data boundaries, retrieval, tools, prompt injection, evaluations, human control, observability, latency, and cost. Use for generative AI, assistants, retrieval, classification, or agents; do not give models consequential authority without explicit controls.
---

# AI Feature Architecture

## Outcome

Produce the smallest AI-assisted workflow that adds measurable value, keeps deterministic controls around consequential behavior, and can be evaluated, observed, limited, replaced, or disabled.

## Required Inputs

- user goal, current workflow, success metrics, unacceptable outcomes, and deterministic alternative
- input and output data classes, jurisdictions, retention, provider training, and privacy constraints
- task type, languages, modalities, context size, latency, availability, and cost targets
- tool actions, permissions, reversibility, financial impact, and required human decisions
- quality, safety, fairness, security, abuse, support, and domain-expert owners
- expected volume, fallback, provider portability, and monitoring needs

If success and unacceptable outcomes cannot be expressed as testable cases, stop before provider or agent selection.

## Safety and Permission Constraints

- Treat model output as untrusted probabilistic data. Validate structure and facts before use; do not use fluency as evidence.
- Treat retrieved documents, webpages, messages, tool output, and memory as untrusted data that may contain prompt injection.
- Keep instructions, data, and authority separate. Allow-list tools and arguments, minimize permissions, constrain destinations and spend, and require human confirmation at consequential boundaries.
- Enforce authorization at each retrieval and tool call. The model must not decide its own access.
- Minimize submitted data and verify current provider retention, training, region, subprocessors, deletion, and abuse-monitoring behavior.
- Publishing AI output, acting on real accounts, handling sensitive data, spending money, or making high-impact decisions is R3 and requires explicit authorization plus appropriate human and qualified review.

## Workflow

1. Compare a deterministic workflow, simple model call, retrieval-assisted call, bounded tool workflow, and agent. Choose the least autonomous option that satisfies the user journey.
2. Define the task contract: inputs, outputs, uncertainty, citations, refusal, escalation, latency, cost, and prohibited actions.
3. Build a representative evaluation set before tuning. Include ordinary, edge, adversarial, multilingual, stale-data, permission, prompt-injection, and tool-failure cases.
4. Compare current candidate models and providers on measured task quality, safety, structured output, tool behavior, context, modalities, latency, availability, data handling, regional support, pricing, rate limits, and exit effort.
5. Design context and retrieval with source provenance, chunk and version policy, access filtering before retrieval, freshness, citations, poisoning defense, and deletion propagation.
6. Define tool schemas narrowly. Validate every argument in deterministic code, re-authorize at execution, use idempotency, cap iterations and spend, isolate untrusted execution, and log approved actions.
7. Layer guardrails around—not instead of—authorization and invariant checks. Define human review for uncertainty, high impact, novelty, and policy exceptions.
8. Measure task success, critical failure rate, false accept and reject behavior, groundedness where applicable, tool choice, policy compliance, latency, availability, and cost. Review samples with domain experts.
9. Version prompts, models, tools, retrieval corpora, policies, and evals. Gate releases on regression thresholds and canary observable changes.
10. Monitor without leaking sensitive prompts or outputs. Provide user feedback, correction, appeal, fallback, kill switch, and incident paths.

## Required Output

- deterministic-versus-AI decision and scoped task contract
- current model and provider comparison with dated evidence
- data, retrieval, authorization, prompt-injection, and tool threat model
- evaluation dataset design, metrics, thresholds, and results
- human approval, escalation, fallback, and kill-switch design
- latency, availability, rate-limit, and cost budget
- observability, privacy, versioning, rollback, and provider-exit plan

## Completion Gate

Do not call the feature ready until representative and adversarial evals meet declared thresholds, tool calls cannot exceed deterministic authority, sensitive-data behavior is verified, failure and provider-outage paths work, and consequential actions remain explicitly controlled.

## Conditional Reference

Read [AI Feature Evidence](references/ai-feature-evidence.md) when defining risk, evals, prompt-injection defenses, or provider-specific implementation claims.
