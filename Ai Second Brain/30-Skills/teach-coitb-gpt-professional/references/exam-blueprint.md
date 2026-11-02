# COITB Certified GPT Professional Exam Blueprint

Verified against official COITB pages on 2026-10-25. Recheck immediately before a study plan, mock exam, registration decision, or claim about current exam logistics.

## Credential and Exam Summary

- Official credential name: **Certified GPT Professional Certification**.
- Published length: **75 minutes**.
- Published item count: **60**.
- Published passing score: **71% or higher**.
- Recommended experience: **0–6 months** of hands-on practice with AI tools or basic prompts.
- Delivery described by the badge page: online remote proctoring or an authorized test center; language listed as English.

Official format wording is inconsistent as of verification: the [exam outline](https://www.coitb.org/certification-resources/exam-outlines/certified-gpt-professional-outline) says **multiple-choice**, while the [badge page](https://www.coitb.org/certification-resources/badges/certified-gpt-professional) says **multiple-choice and scenario-based items**. Prepare for both direct questions and applied scenarios. The public sources do not expose live questions or an item-writing specification.

## Published Domains and Question Coverage

The “60-item equivalent” column is arithmetic derived from the published weights, not a COITB promise about every exam form.

| Domain | Weight | 60-item equivalent | Published coverage, paraphrased |
|---|---:|---:|---|
| 1. Foundations of Generative AI and GPT Models | 10% | 6 | Traditional machine learning vs deep learning vs generative AI; tokens and embeddings; transformers at a high level, including attention, context, and sequence; general capability differences among named GPT generations |
| 2. Prompt Engineering and Output Control | 20% | 12 | System, user, and assistant context; zero-shot, few-shot, and chain-of-thought techniques; delimiters, formats, tone, and constraints; diagnosing ambiguity or missing instructions; JSON and Markdown output; temperature, top-p, and token limits |
| 3. OpenAI Syntax and GPT Integration | 40% | 24 | Account and API-key setup; Python calls through the OpenAI library or HTTP requests; JavaScript/Node.js calls through fetch or axios; Chat Completions requests and roles; JSON response parsing; React/Vite rendering; environment variables; authentication, rate-limit, and token-limit errors; sampling and length controls in code; N8N or Flowise automation; external API integration |
| 4. Responsible AI, Security, and Compliance | 15% | 9 | Bias, misinformation, and copyright concerns; API-key and user-data protection; fairness, accountability, and transparency; privacy of user or proprietary prompts; content filtering or moderation; recognizing GDPR, FERPA, and COPPA contexts |
| 5. Applied GPT Use Cases and Industry Solutions | 15% | 9 | Summarizers and document assistants; customer-support chatbots; N8N, Flowise, or Zapier workflows; tutoring, writing, and research assistance; code completion and refactoring |

Weights total 100%. A 60-item mock that mirrors them exactly therefore contains 6, 12, 24, 9, and 9 items respectively. Use that only as a local practice design.

## Likely Public-Objective Question Forms

These are original teaching interpretations of the published objectives, not observed or recalled exam questions:

| Domain | Useful original question forms | Practical evidence |
|---|---|---|
| Foundations | distinguish learning paradigms; order tokenization, embedding, attention, and generation concepts; select a capability for a scenario; explain why an embedding is not generated prose | diagram a minimal request path and explain each representation |
| Prompting | improve an ambiguous prompt; choose zero-shot vs few-shot; identify role priority; select delimiters or output constraints; predict how sampling or length settings affect behavior; repair malformed structured-output instructions | produce and evaluate prompt variants against a small rubric |
| Integration | complete or debug Python/JavaScript request code; distinguish request from response fields; parse nested JSON; choose server-side secret handling; diagnose 400/401/429/5xx scenarios; identify a safe React/backend boundary; design a bounded automation flow | build an offline client around fixtures, then optionally a reviewed live server-side call |
| Responsible AI | identify bias or misinformation risk; choose an appropriate human-review or moderation control; classify sensitive-data exposure; recognize a GDPR, FERPA, or COPPA issue; reject a client-side key | write a data-flow and risk review for the project |
| Use Cases | select GPT, deterministic code, retrieval, or human escalation; decompose a summarizer or support flow; identify value, failure, and verification criteria; choose an appropriate automation boundary | demonstrate one useful workflow with synthetic data and an evaluation set |

## Exam Lane vs Current Implementation Lane

The official outline contains time-sensitive product examples. Preserve them for exam recognition, but teach current implementation separately.

| Published exam wording | Current-practice interpretation verified 2026-10-25 |
|---|---|
| GPT-3.5, GPT-4, and GPT-4o as version examples | Treat these as historical examples of changing model capabilities. Recheck the current [OpenAI model documentation](https://developers.openai.com/api/docs/models) before choosing or coding against a model. Do not memorize a universal “best” model. |
| `/v1/chat/completions`, `messages`, and system/user roles | Know the named Chat Completions syntax for the exam. OpenAI's [migration guide](https://developers.openai.com/api/docs/guides/migrate-to-responses) recommends the Responses API for current work and documents `instructions`, `input`, typed output, and `output_text`; it also states Chat Completions remains supported. |
| JSON formatting through prompt wording | Understand prompt constraints and JSON parsing for the exam. For current supported models, prefer schema-constrained [Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs) when the application requires a dependable response shape. Still validate business rules in code. |
| Temperature, top-p, and max tokens | Know what the published parameters are intended to control. Current support and names vary by model and endpoint; verify compatibility and use the current output-token setting rather than copying an old snippet. |
| Role-based prompts and chain-of-thought prompting | Know the terminology and why examples or decomposition can improve results. Current prompt design may use developer instructions, and hidden reasoning should not be requested or treated as evidence. Ask for concise rationales or checkable intermediate artifacts. |
| React/Vite displays model output | The browser may display results, but [OpenAI authentication guidance](https://developers.openai.com/api/reference/overview#authentication) says credentials belong in a server environment variable or key manager and must not be exposed in client-side code. Use browser → learner-owned backend → provider. |
| N8N, Flowise, Zapier, and external services | Know the workflow role each can play. Before real credentials or data are connected, review the exact tool, nodes, endpoints, scopes, retention, telemetry, cost, and removal path. |
| Generic error handling | Distinguish invalid input, authentication, permission, rate-limit, quota, timeout, and provider errors. Current [error guidance](https://developers.openai.com/api/docs/guides/error-codes) requires bounded retries only for transient failures, honoring `Retry-After` where present. |
| Content filtering or moderation APIs | Understand moderation as one layer, not a complete safety policy. Recheck the current [Moderation guide](https://developers.openai.com/api/docs/guides/moderation) and combine provider signals with application rules and human escalation. |

Current OpenAI behavior is provider-specific and volatile. The exam outline—not current OpenAI documentation—defines what COITB says it tests. The current documentation governs any real implementation.

## Responsible-AI and Legal Recognition Baseline

- The [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) is voluntary guidance for incorporating trustworthiness into AI design, use, and evaluation; it is not a product certification.
- The [European Commission's GDPR principles](https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en) summarize lawfulness, fairness, transparency, purpose limitation, minimization, storage limitation, accuracy, security, and accountability.
- The U.S. Department of Education's [FERPA summary](https://studentprivacy.ed.gov/faq/what-ferpa) concerns access to, amendment of, and control over disclosure of personally identifiable information from education records.
- The FTC's [COPPA guidance](https://www.ftc.gov/business-guidance/resources/complying-coppa-frequently-asked-questions) addresses covered online collection from children under 13, including notice, parental consent, access, security, retention, and collection minimization duties.

Teach recognition, data minimization, and escalation. Applicability and compliance conclusions require current qualified legal review.

## Local Readiness Heuristic

This is a teaching heuristic, not COITB policy or a score prediction:

- complete at least three original mixed practice sets and one 60-item, 75-minute mock;
- score at least 85% on each of the final two mixed sets and the final mock;
- score at least 75% within every domain rather than relying on Domain 3 to conceal a safety or foundation gap;
- explain every corrected answer in new words and solve a changed variant;
- complete the curriculum capstone with synthetic data, server-side secret boundaries, parsed structured output, deliberate error cases, and a written responsible-AI review;
- distinguish at least five exam-lane concepts from their current-practice implementation without confusing either.

If the exam date is close, prioritize high-weight weak objectives. If time permits, repair prerequisites before increasing question volume.

## Re-Verification Triggers

Recheck when COITB changes the credential title, objectives, weights, item count, duration, format, passing score, delivery, language, price, badge term, policies, or practice assessment; when OpenAI changes endpoints, roles, SDKs, parameter support, authentication, data controls, moderation, or model lifecycle; or before any account, purchase, credential, live API, external integration, or exam-day guidance.
