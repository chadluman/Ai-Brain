---
name: llm-observability-tracing
description: Instrument prompts, tools, and retrieval with traces for an LLM application — trace and span shape, metadata-only logging by default, cost, latency, and quality dashboards together — so the failing step in a bad run can be found from the trace instead of guessed.
---

# LLM Observability Tracing

## Outcome

An LLM application whose runs can be followed step by step after the fact: every prompt, tool call, and retrieval is a traceable span with its inputs, outputs, latency, and cost attached, dashboards show quality, cost, and latency together, and a bad output in production leads to the step that failed instead of to a guess.

## Supporting skills

Load only what the gap requires:

- [Observability SLO Design](../observability-slo-design/SKILL.md) for service-level indicators and objectives, telemetry, dashboards, and alerts in general — this skill adds only what is specific to LLM traces.
- [AI Runtime Governance](../ai-runtime-governance/SKILL.md) for operating the feature in production: telemetry and budgets, fallbacks, canaries, incidents, and retirement.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for scoring traces — turning runs into eval data, datasets, and regression evidence.

## Alpha status

The tools and conventions this skill describes change between releases: tracing platforms rename features, and the OpenTelemetry GenAI conventions are still under active development. The research behind this skill was checked 2026-11-07; re-check the tool's own docs before relying on any feature, attribute name, or limit stated here. Nothing in this skill is a promise that a particular tool exists, works, or stays the same.

## Trace and span shape for LLM apps

A trace is the record of what the application did on one request, from the initial user input to the final response. A trace is made of spans, each span covering one step. For an LLM application the span tree typically looks like this:

- A top-level span for the whole request or agent invocation, carrying the session or conversation identifier and the user or tenant identifier.
- A child span per LLM call, carrying the model, the prompt version, input and output token counts, finish reason, latency, and cost.
- A child span per tool invocation, carrying the tool name, its arguments, the result or error, and its latency.
- A child span per retrieval step, carrying the query, which store or index was searched, how many candidates were returned, and which ones were passed into the prompt.

One useful shape, from the OpenTelemetry GenAI conventions, is a top-level `invoke_agent` span with child `chat` spans per LLM call and `execute_tool` spans per tool invocation. The exact names matter less than the shape: one trace per request, spans nested by what called what, and every span carrying enough context to find it again — by user, session, time window, model version, or prompt version. If a span cannot be tied back to the request that produced it, it is noise, not observability.

Record the prompt version and model version on every trace. A regression that cannot be attributed to a prompt change or a model change cannot be fixed with confidence, and a silent provider-side model update can move quality, cost, and latency all at once.

## The tools, and what each is for

Five options were verified in the research behind this skill. They overlap, and the choice is about what the team already runs and whether the data may leave its network — not about which one is "best" in general.

- **Langfuse** — open-source AI engineering platform for LLM observability, prompt management, and evaluation. Tracing via its SDKs, OpenTelemetry, or a gateway; prompt versioning and labels; datasets and experiments; scoring by code, LLM-as-judge, or human labelling; evaluation of production traces. Self-hostable or cloud. It is based on OpenTelemetry, which reduces lock-in.
- **LangSmith** — LangChain's platform for capturing, debugging, evaluating, and monitoring agent behaviour. Tracing via environment variables or its SDK, with no extra code for LangChain agents; datasets and experiments; offline and online evaluators; annotation queues; dashboards and alerts; automations such as rules, webhooks, and online evals; automatic detection of recurring issues. Cloud, hybrid, or self-hosted.
- **Arize Phoenix** — open-source AI observability platform built on OpenTelemetry for tracing, evaluation, prompt engineering, and experimentation. Tracing via OpenInference auto-instrumentation; datasets and LLM or code evaluators; pre-built metrics including faithfulness, hallucination, toxicity, retrieval relevance, tool calling, exact match, and PII detection; CI integration; cost tracking; span-attribute masking. Runs locally, in a notebook, in a container, or in hosted cloud.
- **OpenTelemetry GenAI conventions** — a vendor-neutral standard vocabulary for GenAI telemetry, not a product. It standardises span attributes such as the operation name, provider name, request and response model, input and output token usage, finish reasons, and conversation ID, plus metrics for call duration and token usage. Caveat: the conventions are under active development, not Stable — expect breaking changes, and re-check before building durable tooling on a specific attribute name.
- **Helicone** — open-source LLM observability platform built as a proxy or gateway: point the base URL at it, or use its AI Gateway, and it logs requests, giving spend, performance, and usage dashboards, session and agent tracing, caching, custom rate limits, and security features. Caveat: its legacy per-provider proxies are maintained but no longer actively developed — new projects should use the AI Gateway.

Other platforms exist — Braintrust for logging and evals, DeepEval with its hosted lifecycle, RAGAS for RAG metrics, OpenAI Evals as a framework and registry — but they were not separately verified as tracing tools in this research, so this skill does not present them as such. Re-check before choosing on their behalf.

## Metadata-only logging by default; content capture is opt-in, with redaction

By default, capture metadata only: model, prompt version, token counts, latency, cost, finish reason, error, user and session identifiers. Prompts, completions, tool arguments, and retrieved passages are content, and content can contain sensitive data — names, account numbers, health details, credentials spoken or pasted in, and documents a user should not have seen. The OpenTelemetry GenAI conventions make content opt-in for exactly this reason.

Before enabling content capture for any span, answer in writing: what content is captured, where it is stored, who can read it, how long it is kept, and how it is redacted. Redact secrets and personal data before the trace is stored, not after someone finds it in a log. Remember that traces and eval datasets are storage: a leaked secret or a cross-user document in a trace is a data leak, and purging it means purging the trace and any dataset built from it, not just the live output. When in doubt, leave content off and diagnose from metadata — a span that says which step failed, how long it took, and what it cost is usually enough to start.

## Dashboards: cost, latency, and quality together

Dashboard the three families together, on the same view, per prompt and model version — never quality alone:

- **Quality** — mean and per-slice judge or human scores, hallucination or faithfulness rate, error rate.
- **Cost** — tokens and cost per completed task, per model and prompt version. Cost per task, not just per token: a cheaper model that doubles its tool calls can cost more per finished job.
- **Latency** — p50, p95, and p99 per step (retrieval vs generation vs tool) and end to end.

Alert on sustained drift or a threshold breach, not on a single noisy run — eval scores are distributions, and one bad run is noise. Alert in both directions: a quality drop and a cost or latency spike after a prompt or model change. A change that looks like a quality win while tripling cost or latency is a tradeoff, not a win, and the dashboard should make that visible without anyone having to ask.

## Using traces for incident diagnosis

When a bad output reaches production, the trace is the first thing to pull — before editing the prompt and hoping:

1. Pull the traces for the affected requests, by user, session, or time window, and identify the failing step: prompt, retrieval, tool call, or model call, with its inputs, outputs, latency, and cost.
2. Freeze the blast radius first — point the production prompt label or flag at the last-known-good version, or disable the affected feature — rather than editing live.
3. Add the failing inputs to the golden eval set before fixing, so the fix is verified against the incident.
4. Run the offline eval on the fix, then bring it back through shadow or canary, not straight to full traffic.
5. Write the post-mortem into the eval set. The golden set grows from every incident.

Keep a one-page incident checklist before it is needed: who can roll back, where the label or flag lives, how to pull traces for a time window, and how to purge a trace or dataset that contains leaked data. The rollback path must work when the person who shipped the change is unavailable.

## Validation exercises

These exercises use hub projects only as practice targets. They are tutorial and demo starting points, not deployable systems, and nothing from them is copied into the vault.

- Run the hub's `eval-and-observability` project as a reference implementation of end-to-end RAG evaluation with tracing. Instrument a small RAG app of your own with one of the tools above, produce a trace for a single question, and check that every span in the tree — retrieval, LLM call, and any tool call — carries model, prompt version, token counts, latency, and cost.
- Take one deliberately bad run (a retrieval miss, a wrong tool argument, or a hallucinated citation) and diagnose it from the trace alone: name the failing step, quote the span that proves it, and write down what the trace did not show that you still had to guess.
- Build the three-family dashboard for that app — quality, cost per task, and p50/p95/p99 latency per step — and set one alert on sustained drift, not on a single run. Record what threshold you chose and why, and note that it is your calibration, not a standard.

## Design checklist

Before relying on tracing for an LLM application, answer every line:

- [ ] Every request produces one trace, with spans nested by what called what, and each span carries model, prompt version, token counts, latency, and cost.
- [ ] Prompt version and model version are recorded on every trace, so a regression is attributable.
- [ ] Logging is metadata-only by default; content capture, if enabled, is opt-in, with redaction, retention, and access written down.
- [ ] The dashboard shows quality, cost per task, and latency per step together, per prompt and model version.
- [ ] Alerts fire on sustained drift or threshold breach, in both directions (quality drop and cost/latency spike), not on a single noisy run.
- [ ] A trace can be pulled by user, session, or time window, and the incident path — freeze, pull traces, add to the golden set, eval, shadow or canary back — is written down before it is needed.
- [ ] The chosen tool's caveats are respected: OpenTelemetry GenAI attribute names are treated as unstable, and new Helicone setups use the AI Gateway, not a legacy proxy.

## State

This skill has not yet been exercised on a real LLM application with traces used to diagnose a failing run. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
