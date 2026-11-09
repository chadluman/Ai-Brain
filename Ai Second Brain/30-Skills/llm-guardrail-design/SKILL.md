---
name: llm-guardrail-design
description: Layer guardrails at every boundary of an LLM application — input validation and jailbreak checks, retrieval filtering, output filtering, and tool-use limits — and measure them like any other component, so a guardrail's false positives are visible alongside its catch rate.
---

# LLM Guardrail Design

## Outcome

An LLM application whose boundaries are each guarded, not just its front door: hostile or mistaken input is caught before it reaches the model, poisoned or over-broad retrieval is filtered before it enters context, unsafe output is filtered before it reaches the user, and the agent's tools are limited so that even a successful injection can do little — and the guardrails themselves are measured, so a guardrail that blocks good traffic is recognised as a quality regression, not as safety.

## Supporting skills

Load only what the gap requires:

- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for guardrails as one scoping layer of the feature — use-case fit, data boundaries, tools, and human control around them.
- [AI Runtime Governance](../ai-runtime-governance/SKILL.md) for rate limits, budgets, and production policy once the guardrails are running.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for measuring the guardrails: golden sets, graders, and regression evidence.

## Alpha status

Guardrail tooling and the threat lists behind it change between releases: detection models are updated, rail frameworks add or rename features, and the OWASP list is revised. The research behind this skill was checked 2026-11-07; re-check the tool docs and the current OWASP list before relying on any feature, category, or limit stated here. Nothing in this skill is a promise that a particular guardrail exists, works, or stays the same.

## The threat list: OWASP LLM Top 10 2025

Use the OWASP Top 10 for LLM Applications 2025, maintained by the OWASP GenAI Security Project, as the threat list when designing guardrails — not as a checklist to tick off, but as the set of failure classes to ask about for each boundary. The entries most often in scope for guardrail design are:

- **LLM01 Prompt Injection** — the top-ranked risk: user prompts, or content the model reads later, alter the model's behaviour or output in unintended ways. Injected content does not need to be visible to humans, as long as the model parses it.
- **LLM02 Sensitive Information Disclosure** — the model reveals data it should not: personal data, secrets, or one user's data to another user.
- **LLM07 System Prompt Leakage** — the system prompt itself is extracted through the conversation.
- **LLM08 Vector and Embedding Weaknesses** — the retrieval layer is attacked: poisoned documents in the index, or embeddings that leak or mislead.
- **LLM10 Unbounded Consumption** — the application lets a caller burn unlimited tokens, calls, or cost.

The full list also covers supply chain, data and model poisoning, improper output handling, excessive agency, and misinformation. The OWASP site itself was not opened in the research behind this skill, so the list above rests on secondary summaries — re-check the current list before treating any entry as settled, and treat the list as a starting point for threat modelling, not as proof that every entry applies to every application.

## Guardrails at every boundary, not one choke point

No single layer catches everything. Layer guardrails at each boundary, so a failure at one layer is still caught at the next:

- **Input — validation and jailbreak or injection check.** Validate the shape of the input before it reaches the model, and check it for jailbreak and injection attempts. Jailbreak detection can be layered: a self-check that asks a model to identify jailbreak attempts, heuristic pattern-based detection, and a dedicated detection model or third-party service. None of these is foolproof — OWASP itself notes it is unclear whether foolproof prevention of prompt injection exists — so treat detection as a filter that reduces risk, not as a guarantee.
- **Retrieval — filtering before context.** Filter retrieved chunks before they enter the prompt: drop poisoned or irrelevant chunks, enforce permission and tenant filters at retrieval time, and mark retrieved text with its provenance so the model and the reader can tell it apart from instructions. A document in the corpus can carry hidden instructions, and the model will follow them when the chunk is retrieved unless the boundary is enforced in code. Retrieval filtering is also where permission leakage is stopped: the filter is a metadata or tenant condition on the query, never a prompt instruction. The model cannot be the access control.
- **Output — filtering before the user.** Filter the model's output before it is shown or acted on: PII redaction, moderation or toxicity checks, and a grounding check that the answer is supported by the retrieved context. Output filtering is the last chance to catch a leak or a hallucinated claim — and it is also where a filter can wrongly block a good answer, which is why false positives are measured (see below).
- **Tool use and agency — limits on what the agent can do.** Bound the agent's authority: least-privilege tools, one toolset per task rather than one god-agent, validation of every tool-call argument in code before execution, human approval for consequential actions (send, delete, publish, pay, change permissions), and budgets on iterations, time, and cost. The damage from an injection is usually agentic, not textual — injected text drives a tool call, which exfiltrates data or takes an unauthorised action. Limits on tools are what keep a successful injection small.

## NeMo Guardrails and Presidio

Two tools were verified in the research behind this skill. Use them as components, not as a safety verdict.

- **NeMo Guardrails** (NVIDIA, open-source Python) is a package for adding programmable guardrails to LLM applications, to block, alter, or validate unsafe, off-topic, malicious, or policy-violating inputs and responses. It organises its checks as rails: input rails, dialog rails, retrieval rails, execution rails, and output rails — the same boundary layering this skill describes, expressed as flows. Its jailbreak detection layers include self-check, heuristic pattern detection, a dedicated detection model, and third-party integrations. Its PII detection and masking can run through several detectors, including Presidio, and can detect-and-block or mask before processing, on user inputs, model outputs, and retrieved content.
- **Presidio** is open-source PII detection and anonymisation (an analyser, an anonymiser, and related tools). Its own warning matters more than its feature list: because it uses automated detection, there is no guarantee it will find all sensitive information, and additional systems and protections should be employed. It typically performs pseudonymisation — replacing detected values with placeholders — not complete anonymisation. That warning applies to every automated detector, not only to Presidio: a detector that reports nothing found has not proven nothing sensitive is present. Treat PII detection as a net with holes, and keep the other boundaries (retrieval filtering, output filtering, access control) in place behind it.

## Secrets never live in a system prompt

Never put secrets, credentials, or authorisation logic in a system prompt. The system prompt should not be considered a secret, and it should not be used as a security control — it can leak (OWASP LLM07), it can be extracted through conversation, and it is visible to anyone who can read the configuration. Credentials live in the tool layer, behind code that checks authorisation before the tool runs. If a design only works because the model was told a secret in its instructions, the design is broken: rewrite it so the model proposes and code disposes, with authorisation enforced downstream of the model.

The same rule applies to retrieved content. Treat everything a tool or a document returns as data, never as instructions — including web pages, emails, tickets, files, and database rows. Mark untrusted content clearly when it is injected into a prompt (delimiters, source labels), and never concatenate system instructions and untrusted pasted content into one undifferentiated block.

## Guardrails as evaluated components

A guardrail is a component of the application, so it is evaluated like one. Add cases to the golden eval set for each guardrail, and measure both sides:

- **Catch rate** — jailbreak cases, PII-leak cases, and injection cases (direct, in the user's own prompt, and indirect, hidden in content the model reads later) that the guardrail blocks or neutralises.
- **False-positive rate** — legitimate requests the guardrail blocks or degrades. A guardrail that blocks a visible share of good traffic is a quality regression, and it should be treated as one: measured, reported, and fixed, not celebrated as caution.

Run the guardrail cases on every change to the guardrail, the prompt, or the model, as part of the same regression run as the rest of the eval set. Mark safety and compliance cases as blocking — a failure there stops the change, without being averaged away by good scores elsewhere. And re-check the guardrail after any fine-tuning run: tuning can unlearn guardrails even on benign data, so a tuned model needs its safety evals re-run before it ships.

Rate limits belong in the same picture: unbounded consumption is a threat in its own right, so bound calls, tokens, and cost per user and per task, and treat a limit being hit as an event to log and review, not as silent failure.

## Validation exercises

These exercises use hub projects only as practice targets. They are tutorial and demo starting points, not deployable systems, and nothing from them is copied into the vault.

- Run the hub's `trustworthy-rag` project as a reference implementation of grounded RAG, and attack it on paper first: list which of its boundaries an injected document, a poisoned chunk, or an over-broad retrieval could cross, and which layer in this skill would catch each one. Then add one injection case and one PII-leak case to a golden set for it and record whether the existing layers catch them.
- Run the hub's `parlant-conversational-agent` project as a compliance-driven conversational agent, and write down which of its behaviours are guardrails (policy enforced in code) and which are only prompt instructions — then move one prompt-only rule into a code-enforced check and note what changed.
- Build a small guardrail test set of your own: ten jailbreak attempts, ten PII-leak probes, ten indirect-injection cases hidden in retrieved text, and ten legitimate requests that resemble them. Run a guardrail configuration against all forty, and report catch rate and false-positive rate side by side.

## Design checklist

Before relying on guardrails for an LLM application, answer every line:

- [ ] Guardrails sit at every boundary — input, retrieval, output, and tool use — not at one choke point.
- [ ] The OWASP LLM Top 10 2025 was used as the threat list, re-checked against the current list, and the entries in scope for this application are named.
- [ ] No secret, credential, or authorisation rule lives in a system prompt; credentials live in the tool layer and authorisation is enforced in code.
- [ ] Retrieved text is treated as data, marked with provenance, and permission-filtered at retrieval time — never by prompt instruction.
- [ ] PII detection is treated as pseudonymisation with incomplete recall, per Presidio's own warning, with other boundaries behind it.
- [ ] The guardrails are in the golden eval set — jailbreak, PII-leak, and injection cases — with catch rate and false-positive rate measured side by side, and safety cases marked as blocking.
- [ ] Rate, token, and cost limits are set per user and per task, and hitting a limit is logged and reviewed.
- [ ] Safety evals are re-run after every tuning or model change, before the change ships.

## State

This skill has not yet been exercised on a real LLM application with guardrails measured against jailbreak, PII-leak, and injection cases. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
