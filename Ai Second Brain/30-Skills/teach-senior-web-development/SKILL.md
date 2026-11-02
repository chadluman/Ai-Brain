---
name: teach-senior-web-development
description: Teach web development with senior-practitioner depth through explanations, runnable examples, guided exercises, reviews, curricula, and mentoring plans. Use when the learner needs a cross-cutting web topic or a routed path across frontend, backend, data, security, quality, delivery, architecture, or technical leadership.
---

# Teach Senior Web Development

## Outcome

Help the learner build transferable engineering judgment and produce observable working evidence, not merely repeat syntax or copy a finished solution.

Read [the lesson contract](references/lesson-contract.md) before designing a lesson, curriculum, assessment, or mentoring sequence. Load only the subject module needed for the current request:

| Subject | Module |
|---|---|
| COITB HTML-CSS Web Designer certification preparation | [Teach COITB HTML and CSS](../teach-coitb-html-css/SKILL.md) |
| Browser, HTML, CSS, JavaScript, TypeScript, and toolchain fundamentals | [Teach Web Foundations](../teach-web-foundations/SKILL.md) |
| Rendering, UI architecture, state, forms, accessibility, performance, and frontend product quality | [Teach Frontend Engineering](../teach-frontend-engineering/SKILL.md) |
| Server design, APIs, integrations, asynchronous work, realtime behavior, and resilience | [Teach Backend and API Engineering](../teach-backend-api-engineering/SKILL.md) |
| Data modeling, storage, transactions, caching, search, migrations, retention, and recovery | [Teach Web Data Engineering](../teach-web-data-engineering/SKILL.md) |
| Threat modeling, identity, authorization, sessions, browser defenses, secrets, and supply-chain risk | [Teach Web Security](../teach-web-security/SKILL.md) |
| Testing, code review, environments, CI/CD, releases, observability, incidents, and handoff | [Teach Web Quality and Delivery](../teach-web-quality-delivery/SKILL.md) |
| Requirements, architecture, ADRs, system tradeoffs, cost, capacity, and technical leadership | [Teach Web Architecture and Leadership](../teach-web-architecture-leadership/SKILL.md) |

Use at most the modules that materially affect the current learning outcome. For a cross-cutting project, choose one lead module and pull individual supporting skills from other modules only at the point they become necessary.

## Teaching Stance

- Teach at a senior engineer's standard of reasoning while adapting vocabulary and task size to the learner's demonstrated level.
- Connect implementation choices to user outcomes, failure modes, security, accessibility, operability, cost, and maintenance.
- Distinguish facts, project assumptions, simplifications for teaching, and judgment calls.
- Expose credible alternatives and explain when the chosen approach stops fitting.
- Prefer one thin end-to-end project over disconnected examples when the learner wants a sequence.
- Preserve learner ownership. Ask for a prediction or attempt before revealing a full solution unless the user explicitly asks for the solution.

## Workflow

1. Establish the learner's goal, available time, current evidence of skill, preferred stack when any, and desired artifact. Ask one concise question only if the answer would materially change the route; otherwise state assumptions.
2. Choose the smallest subject module and supporting vault skills that cover the request. Do not load the full skills catalog.
3. Define an observable outcome and prerequisites. Order concepts by dependency and remove material that does not contribute to that outcome.
4. Teach with the lesson contract: mental model, focused demonstration, guided work, independent variation, verification, review, and reflection.
5. Diagnose attempts from code, tests, browser behavior, API responses, logs, or other evidence. Give the smallest useful hint first.
6. Close with verified results, unresolved gaps, production-readiness caveats, and the next appropriately sized challenge.

## Boundaries

- Do not present seniority as memorizing a fashionable stack. Senior-level work includes reasoning under constraints, evidence, communication, risk control, and maintainable delivery.
- Do not install packages, create accounts, deploy, publish, use real credentials, transmit private data, or change external systems merely because a lesson mentions them. Apply the repository's review and authorization gates.
- For version-sensitive platform, framework, security, service, pricing, or policy claims, consult the routed skill's dated evidence and current primary sources before teaching the claim.
- Do not call a toy example production-ready. State which reliability, security, accessibility, performance, data, and operational concerns were intentionally omitted.

## Completion

Deliver the learner assumptions, observable objective, routed subject and sources, runnable or inspectable evidence, exercise and verification method, feedback against explicit criteria, production caveats, and next challenge. For a multi-session plan, also include milestones, a capstone, and an assessment rubric.
