---
name: web-form-design
description: Design or review an accessible, secure, resilient web form from data collection through server processing and user feedback. Use for sign-up, checkout, search, settings, uploads, or multi-step flows; do not treat client-side validation as a security boundary.
---

# Web Form Design

## Outcome

Produce a form flow that asks only for necessary data, works with native browser and assistive behavior, validates authoritatively on the server, prevents unsafe state changes, and gives users clear recovery paths.

Read [form evidence](references/form-evidence.md) before choosing controls, validation, or security behavior.

## Inputs

Identify the user goal, data fields and sensitivity, legal or retention constraints, authentication state, side effects, duplicate-submission risk, localization, device and input modes, abandonment cost, time limits, offline or interrupted behavior, upload needs, and abuse cases.

## Workflow

1. Minimize fields and data retention. Define each field's purpose, owner, validation rule, storage destination, retention, and deletion behavior.
2. Use the correct native form, label, input, button, fieldset, legend, autocomplete, inputmode, and type semantics. Add custom controls only when native behavior cannot meet a real requirement.
3. Make instructions, required state, format expectations, and privacy consequences available before input. Do not rely on placeholder text as the only label or instruction.
4. Use client-side validation for timely assistance. Apply the same authoritative business and security validation on the server, independent of client code and static types.
5. On failure, preserve safe user input, identify errors in text, associate each message with its control, provide a summary when useful, move focus deliberately, and avoid erasing progress.
6. Protect state-changing requests according to the session and request model. Address CSRF, authorization, replay and duplicate submission, rate limits, idempotency, mass assignment, injection, and sensitive values in URLs or logs.
7. Define loading, success, partial success, timeout, retry, interruption, expired-session, conflict, and server-failure states. Confirm consequential submissions and make reversals available where possible.
8. Test the critical flow with keyboard, screen reader, zoom, touch, autofill, password managers where relevant, client JavaScript unavailable or failed, slow and duplicate requests, invalid server responses, and supported browsers.

## Safety Boundaries

- Never trust hidden fields, disabled controls, client validation, client-generated identifiers, prices, roles, or authorization claims.
- Never include secret values or sensitive personal data in example submissions, URLs, analytics, logs, or vault notes.
- File upload, payment, identity proofing, health, legal, and regulated forms require their specialized security and compliance playbooks.
- Do not add analytics, session replay, CAPTCHA, fraud, address, or identity services without dependency, privacy, accessibility, data-flow, and account authorization review.

## Completion

Deliver the field and data inventory, semantic structure, client and server validation contract, error and status behavior, security controls, idempotency and recovery rules, accessibility and failure tests, retention and telemetry boundaries, evidence dates, and known risks.
