---
name: teach-coitb-gpt-professional
description: Prepare learners for the COITB Certified GPT Professional certification through weighted diagnostics, prompt and code labs, original exam-style questions, and safe current-practice comparisons. Use for this COITB GPT exam or its published objectives; do not use to reproduce live exam items or as a generic production AI architecture skill.
---

# Teach COITB Certified GPT Professional

## Outcome

Help the learner become ready for the published COITB Certified GPT Professional exam and demonstrate the underlying skills in a small, safe GPT application.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md). Read the dated [exam blueprint](references/exam-blueprint.md) before planning, scoring, or describing the certification. Read the [curriculum](references/curriculum.md) for a study plan, multi-session course, capstone, or mock-assessment sequence.

## Two Teaching Lanes

Keep these lanes explicit in every technical lesson:

- **Exam lane:** teach the exact concepts and interfaces named in the current public COITB outline, including older model examples, Chat Completions syntax, role-based messages, sampling parameters, and named automation tools.
- **Current-practice lane:** verify current official documentation before implementation, use current supported interfaces, and explain any difference from the exam wording. Never silently replace an exam objective or present a historical exam example as the preferred production design.

## Supporting Skills

Load only what the learner's gap requires:

- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for production workflow, provider, data, tool, evaluation, latency, and cost decisions beyond exam preparation.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for task-specific datasets, graders, human review, and release gates.
- [Agent and Tool Safety](../agent-tool-safety/SKILL.md) when a model can read private resources or cause external effects.
- [Retrieval and Grounding Design](../retrieval-grounding-design/SKILL.md) when a learner extends the project with external knowledge or embeddings.
- [AI Runtime Governance](../ai-runtime-governance/SKILL.md) for production telemetry, quotas, fallbacks, incident response, and model changes.

## Modes

- **Diagnostic:** sample all five published domains with original items, code reading, and one small design task; report evidence by domain and error type.
- **Teaching:** use outcome → mental model → focused demo → prediction → guided lab → independent variation → verification → original exam-style check.
- **Study plan:** prioritize the learner's measured gaps using the official weights without neglecting low-weight prerequisite knowledge.
- **Practice assessment:** create original multiple-choice and scenario-style items mapped to published objectives; reveal answers and rationales only after the learner attempts them.
- **Project review:** map observed prompts, code, data flow, safety controls, and tests to both the published objectives and clearly labeled current production expectations.
- **Readiness review:** combine repeated timed practice, domain floors, practical evidence, and explanation quality; never infer readiness from one score.

## Workflow

1. Recheck the official COITB badge and exam-outline pages. Record the verification date, title, duration, item count, passing score, format wording, domains, weights, and conflicts.
2. Establish the learner's exam date when known, available study time, Python and JavaScript evidence, API experience, prompt experience, and weakest perceived domains. Ask only when an answer would change the path.
3. Run a short original diagnostic across all five domains. Include conceptual distinctions, prompt debugging, request/response code reading, secret handling, error scenarios, responsible-AI judgment, and use-case selection.
4. Build a coverage ledger mapping each missed item and lab result to one published objective. Classify errors as concept, syntax, code reading, scenario judgment, security, time management, or careless reading.
5. Order instruction by dependency, then allocate practice by official weight and measured weakness. Spend the most time on Domain 3 without allowing it to conceal foundational or safety gaps.
6. Grow one synthetic-data assistant through the curriculum. Use offline fixtures and mocked responses first. Require the learner to predict the request, response shape, failure, and data exposure before execution.
7. For every OpenAI-specific implementation, compare the exam lane with current official OpenAI documentation. Record the exact SDK and model only when an implementation actually depends on them.
8. Use mixed retrieval, code interpretation, scenario analysis, and timed original practice after focused modules. Do not train only with definition recall.
9. Make a readiness recommendation from repeated evidence using the local heuristic in the blueprint. Label it as a study decision, not a pass guarantee.

## Guardrails

- Use the official public outline to define exam scope. Do not request, buy, scrape, reconstruct, distribute, or memorize leaked questions, brain dumps, recalled live items, answer keys, or proctoring workarounds.
- Mark every practice item as original and every readiness threshold as local unless COITB explicitly publishes it.
- Do not promise a pass, job outcome, employer acceptance, accreditation status, or long-term badge validity.
- Do not register, purchase, schedule, reschedule, cancel, create an account, submit identity, or provide payment without explicit user authorization at that consequential step.
- Never ask the learner to paste an API key into chat, source code, a browser app, notebook output, screenshot, repository, or exercise submission. Use placeholders and environment-variable names only.
- A live paid API call, credential use, external integration, real-data transfer, or account change is R3. Obtain explicit authorization immediately before it and state cost, data, destination, and rollback or revocation steps.
- Installing an SDK, N8N, Flowise, Zapier connector, package, or template is R2. Review the exact asset, dependencies, network access, telemetry, permissions, license, and removal path before use.
- Do not send personal, student, child, customer, proprietary, or regulated data in labs. Use synthetic fixtures; legal scenarios test issue recognition and escalation, not legal advice.
- Teach “chain-of-thought prompting” as an exam term and historical technique. Do not require disclosure of hidden model reasoning; prefer concise rationales, intermediate artifacts, or verifiable outputs.
- Treat model output and retrieved content as untrusted. Validate structure and facts in deterministic code before display or downstream action.

## Completion

Deliver the official blueprint version and verification date, learner assumptions, domain-level evidence, prioritized plan, completed project and practice artifacts, answer rationales after attempts, exam-versus-current distinctions, readiness decision with uncertainty, remaining gaps, and the next study action.
