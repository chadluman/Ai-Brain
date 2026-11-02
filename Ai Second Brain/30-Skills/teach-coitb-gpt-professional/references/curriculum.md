# COITB Certified GPT Professional Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. Preserve the published domain weights while ordering instruction by dependency. Grow one synthetic-data project so multiple-choice preparation remains connected to observable behavior.

## Learner Assumptions

- The certification targets learners with roughly 0–6 months of AI-tool or basic-prompt practice.
- Basic Python and JavaScript reading are part of the published scope. Teach the minimum language syntax first when the diagnostic shows a gap.
- No paid API account, live credential, workflow platform, frontend framework installation, or real user data is required for the core path.
- Practice content, fixtures, and documents are original, licensed, public-domain, or explicitly permitted.
- Completing this curriculum does not guarantee a passing score or prove production readiness.

## Final Observable Outcome

The learner can answer original questions across all five published domains and explain, build, debug, and evaluate a small GPT-assisted support-triage application. The project uses synthetic tickets, role-aware instructions, structured output, Python request and response handling, a server-side secret boundary, representative error fixtures, responsible-AI controls, and a simple UI or CLI. The learner can also explain where the COITB wording differs from current provider practice.

## Project Spine — Support Triage Assistant

Use a fictional organization and synthetic support requests. Build in stages:

- define labels such as `billing`, `account`, `technical`, and `other`;
- create a prompt that classifies a request and drafts a reply;
- define a JSON result with `category`, `urgency`, `reply`, `needs_human`, and `reason`;
- parse saved response fixtures in Python and JavaScript;
- add invalid JSON, authentication, rate-limit, timeout, and oversized-input fixtures;
- expose results through a CLI or a small UI backed by a local server boundary;
- add moderation or policy routing as a design exercise or reviewed optional implementation;
- evaluate ordinary, ambiguous, adversarial, sensitive-data, and escalation cases.

Default to an offline simulator: no account, key, package installation, external request, or spend. A live extension requires the review and authorization gates in `SKILL.md`.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce objective-level evidence and a prioritized study plan.
- **Demo:** Map one original scenario to its domain and objective, eliminate distractors, and verify the underlying behavior with a tiny fixture.
- **Guided lab:** Inspect an intentionally weak prompt, unsafe browser key, malformed response parser, and misleading output.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record results by domain, objective, and error type. Identify exam-lane/current-practice confusion separately.

## Module 1 — Generative-AI Foundations, 10%

- **Concepts:** traditional ML vs deep learning vs generative AI; training vs inference; tokens; embeddings as numerical representations; transformer attention, context, and sequence at a high level; capabilities and limitations; model versions as changing products.
- **Demo:** Trace a sentence from text to token identifiers to contextual processing to generated next-token probabilities; contrast an embedding vector with generated text.
- **Guided lab:** Sort small scenarios into prediction, classification, generation, retrieval, or deterministic rules and justify each boundary.
- **Independent variation:** Explain which approach should handle a policy lookup, a creative draft, and an exact invoice total.
- **Original exam practice:** concept distinctions, sequence ordering, capability selection, and limitation recognition.
- **Verification:** the learner explains the pipeline without claiming the model understands, searches, stores facts, or guarantees truth merely because its answer is fluent.

## Module 2 — Prompt Engineering and Output Control, 20%

- **Concepts:** roles and instruction priority; task, context, constraints, delimiters, examples, and output contract; zero-shot and few-shot prompting; decomposition; chain-of-thought as exam terminology; Markdown and JSON; ambiguity diagnosis; prompt injection boundaries; temperature, top-p, and output length as model-dependent controls.
- **Demo:** Start with “classify this ticket,” identify missing requirements, then refine it against a rubric rather than by taste.
- **Guided lab:** Create the triage prompt, two diverse examples, allowed labels, refusal or escalation behavior, and the JSON contract.
- **Independent variation:** Adapt the prompt to an education-help scenario without reusing support-specific assumptions.
- **Original exam practice:** select the useful prompting strategy, repair ambiguity, choose a delimiter, identify role conflicts, predict qualitative sampling effects, and recognize invalid JSON requirements.
- **Verification:** test at least ten synthetic inputs, including ambiguous and adversarial cases; compare results against expected labels and explain failures.

Do not score prompt quality from one pleasing answer. Keep a versioned prompt and the same evaluation cases so changes are comparable.

## Module 3A — Python and API Request Fundamentals, 40% Domain Part 1

- **Concepts:** environment variables; HTTP method, URL, headers, JSON body, status, and response; official SDK vs direct HTTP; request and response objects; synchronous flow; role arrays in the published Chat Completions shape; current Responses API differences.
- **Demo:** Read a credential-free Python function that builds a request dictionary and consumes a saved response fixture. Compare the exam-lane Chat Completions fields with current Responses fields.
- **Guided lab:** Implement fixture loading, result extraction, type checks, and a useful error when required fields are absent.
- **Independent variation:** Parse a refusal or partial response without assuming that text always exists in one fixed location.
- **Original exam practice:** complete missing request fields, select the correct role, distinguish header/body data, trace nested JSON, and identify a hard-coded secret.
- **Verification:** unit tests pass for success, missing field, malformed JSON, refusal, and unexpected shape; no credential or network is needed.

## Module 3B — JavaScript, React Boundary, and Rendering, 40% Domain Part 2

- **Concepts:** `fetch` or axios request structure; promises and errors at the level needed to read exam snippets; JSON parsing; UI loading, success, refusal, and failure states; browser/server trust boundary; React/Vite as published examples rather than mandatory architecture.
- **Demo:** Trace browser input to a local backend contract and render a saved result without exposing a provider key.
- **Guided lab:** Build a minimal form or CLI-equivalent that sends synthetic text to the local triage boundary and renders category, urgency, reply, and human-review status.
- **Independent variation:** Add cancellation or duplicate-submit protection and an accessible error state.
- **Original exam practice:** choose `response.json()` at the right stage, identify an unsafe `VITE_OPENAI_API_KEY`, select a dynamic render path, and diagnose an unhandled rejected promise.
- **Verification:** inspect client assets and logs for secrets; exercise loading, success, malformed response, rate-limit fixture, timeout, and retry-stop behavior.

## Module 3C — Controls, Errors, Automation, and External APIs, 40% Domain Part 3

- **Concepts:** 400-class input errors, 401 authentication, 403 permissions, 429 rate or quota conditions, timeouts, 5xx service failures, bounded retry, `Retry-After`, token or context limits, request IDs, idempotency for external actions, N8N/Flowise/Zapier workflow concepts, and least-privilege connectors.
- **Demo:** Classify fixture errors as fix-before-retry, retry-with-bound, or escalate; diagram an automation that drafts an email but requires human approval before sending.
- **Guided lab:** Add typed error mapping, a bounded retry decision, redacted diagnostics, and a dead-letter or manual-review state to the project.
- **Independent variation:** Design a Notion or email integration without implementing it; list data, scopes, endpoints, external effects, confirmation, failure, and revocation.
- **Original exam practice:** select an appropriate error handler, identify endless retry, choose secure secret storage, order an automation flow, and separate read from write permissions.
- **Verification:** every error fixture produces the declared user state and operator evidence; no retry occurs for invalid keys, malformed input, denied permissions, or exhausted budget.

## Module 4 — Responsible AI, Security, and Compliance, 15%

- **Concepts:** bias and harmful representation; hallucination and misinformation; copyright and source rights; fairness, accountability, and transparency; human oversight; data minimization; secrets; retention; content moderation; GDPR, FERPA, and COPPA issue recognition; model output as untrusted data.
- **Demo:** Review a support assistant that leaks an API key, sends unnecessary customer data, fabricates a refund policy, and auto-sends without review.
- **Guided lab:** Create a data-flow table for each field, destination, purpose, retention need, access group, and deletion path. Add escalation rules for uncertainty and sensitive requests.
- **Independent variation:** Assess a tutoring assistant involving student records and a child-directed writing tool; identify questions for a privacy or legal reviewer.
- **Original exam practice:** choose the relevant risk or regulation context, identify the missing transparency or human-control step, and distinguish moderation from authorization.
- **Verification:** no real or sensitive data appears in fixtures; the learner can state what the system must refuse, flag, minimize, disclose, or escalate and why.

## Module 5 — Applied Use Cases and Solution Design, 15%

- **Concepts:** summarization, document assistance, support, automation, education, writing, research, code completion, and refactoring; deterministic alternatives; retrieval vs generation; measurable value; failure cost; human-in-the-loop; evaluation criteria.
- **Demo:** Compare a deterministic FAQ lookup, a GPT draft, a retrieval-grounded answer, and a tool-using agent for the same support journey.
- **Guided lab:** Write a one-page design for the triage assistant: user, job, inputs, outputs, success, prohibited outcomes, fallback, cost boundary, and test cases.
- **Independent variation:** Choose one published use case and defend why GPT is or is not appropriate relative to a simpler alternative.
- **Original exam practice:** select a suitable use case, identify an over-automated design, match a workflow to a business problem, and choose observable success criteria.
- **Verification:** the learner explains the value and the failure mode, not merely the technology; the design retains a non-AI or human recovery path.

## Module 6 — Mixed Review and Timed Practice

- **Outcome:** Transfer knowledge across domains under the published time constraint.
- **Demo:** Solve one scenario containing prompt, code, security, and use-case clues; identify which facts are relevant before selecting an answer.
- **Guided lab:** Complete a 20-item original mixed set and perform an error autopsy.
- **Independent task:** Complete an original 60-item, 75-minute mock with 6/12/24/9/9 domain distribution.
- **Verification:** score by domain and objective, retest changed variants, and update the coverage ledger. Do not reuse the same wording as proof of mastery.

## Original Practice-Item Rules

For each item:

1. Map it to one published objective and one primary reasoning demand.
2. Write an original stem and original options; never imitate a dump or claimed live item.
3. Make one option best under the facts given. Avoid trivia not supported by the public outline.
4. Use plausible distractors tied to a misconception: role confusion, client-side secrets, blind retry, JSON/string confusion, deterministic-vs-generative mismatch, or policy-vs-authorization confusion.
5. For code items, keep snippets minimal and include enough context to decide.
6. After the learner answers, reveal the correct option, objective, rationale, why each distractor fails, and one transfer question.
7. Mark current-provider details with a verification date and source. Do not let volatile trivia dominate an exam-aligned item.

Use a balance of definition, comparison, code-reading, debugging, architecture, and scenario judgment. A full mock should not contain 60 near-identical recall questions.

## Capstone Acceptance Criteria

The learner can demonstrate or submit:

- a concise task contract and data-flow diagram;
- a versioned prompt with roles, context, constraints, examples where justified, and a structured output contract;
- Python parsing of success, refusal, malformed, and error fixtures;
- JavaScript or pseudocode showing a safe browser-to-backend boundary;
- no key, secret, real personal data, or proprietary content in code or fixtures;
- bounded error handling that distinguishes retryable from action-required failures;
- at least 20 evaluation cases with expected behavior, including ambiguity, misinformation, bias, sensitive data, prompt injection, and escalation;
- an exam/current comparison for endpoint, roles, response parsing, parameters, and structured output;
- a responsible-AI review with limitations, human control, moderation boundary, and qualified-review questions;
- a five-minute explanation and one live modification chosen by the tutor.

Label the artifact **practice implementation**. It is not a production deployment.

## Assessment Rubric

Score each dimension from 0 to 3: 0 not demonstrated, 1 needs guidance, 2 functional, 3 reliable and explainable.

| Dimension | Evidence |
|---|---|
| Foundations | Correct mental model for models, tokens, embeddings, attention, context, and limitations |
| Prompt design | Clear instructions, appropriate examples, controlled output, and measured iteration |
| Python/API syntax | Correct request construction, environment-variable boundary, response parsing, and code tracing |
| JavaScript/UI integration | Correct asynchronous flow, backend secret boundary, and observable states |
| Failure handling | Correct classification, bounded retry, useful diagnostics, and recovery |
| Responsible AI | Data minimization, privacy recognition, bias/misinformation controls, moderation limits, and human escalation |
| Use-case judgment | Appropriate AI boundary, measurable value, simpler alternative, and fallback |
| Exam transfer | Accurate objective mapping, time management, rationale, and success on changed variants |

A high aggregate cannot offset a zero in secret handling, personal-data safety, or the ability to distinguish model output from verified fact.

## Setup, Run, and Test Boundary

- Core path: use a text editor, Python standard library, JavaScript runtime only if already available, and checked-in synthetic JSON fixtures. Do not install anything solely to begin.
- Before any package installation, select an exact version and complete the repository's R2 review.
- Before any live provider call, obtain explicit authorization, confirm the account and spend boundary, use a server-side `OPENAI_API_KEY`, minimize submitted data, and define key revocation and local cleanup.
- Record commands and expected results only after the learner's environment is known. Never provide a command that echoes a secret.

## Review Cadence

- Short path: diagnostic, Modules 2 and 3, Module 4, one mixed set, capstone repair, final mock.
- Full path: Modules 0–6 in order, with cumulative reviews after Modules 2, 3C, and 5.
- Recheck the official outline and current provider documentation immediately before the final mock or any live implementation.
