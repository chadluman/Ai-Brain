---
name: privacy-data-governance
description: Design or review personal-data collection, purpose, minimization, consent or other authority, retention, user controls, vendor sharing, analytics, deletion, export, and privacy verification for web and mobile products. Use when a feature can identify, profile, track, infer about, or materially affect a person; do not treat it as legal advice.
---

# Privacy and Data Governance

## Outcome

Produce a traceable data design in which each personal-data flow has a specific necessary purpose, limited access and retention, understandable user controls, and verifiable deletion or export behavior.

## Required Inputs

- users, jurisdictions, ages, vulnerability, and product context
- every collected, generated, inferred, imported, logged, and shared data element
- purpose, necessity, decision effect, source, recipients, storage, retention, and deletion path
- analytics, advertising, experimentation, AI, support, fraud, safety, and legal-hold needs
- vendors, subprocessors, regions, transfers, contracts, and export or deletion capabilities
- applicable qualified legal, privacy, security, and accessibility owners

If jurisdiction, age population, sensitive-data scope, or controller/processor roles are uncertain, flag qualified review rather than inventing a compliance conclusion.

## Safety and Permission Constraints

- Collect the minimum data needed for a defined user-serving purpose. Do not retain data merely because it may become useful.
- Treat identifiers, device signals, URLs, free text, telemetry, support content, derived profiles, and combinations as potentially personal data.
- Do not equate consent banners with valid consent, lawful processing, privacy, or control. Avoid deceptive or bundled choices.
- Separate production data from development, testing, analytics, and model-training uses. Default to synthetic or de-identified test data.
- Never place personal data or secret values in the vault. Record data categories and approved systems only.
- Real-data migration, new tracking, data sale or sharing, production exports or deletion, policy publication, and regulator or user communication are R3 and require immediate authorization and qualified review where applicable.

## Workflow

1. Create a data inventory and flow map from user or source through clients, APIs, storage, logs, analytics, vendors, backups, and deletion.
2. For each flow, record purpose, necessity, authority, sensitivity, users affected, controller or processor, recipients, region, retention, and owner.
3. Remove optional collection, reduce precision and linkability, prefer on-device or aggregate processing, and avoid persistent identifiers when a shorter-lived alternative works.
4. Define just-in-time, accessible explanations and controls. Make acceptance, refusal, withdrawal, objection, and later changes as clear and usable as the original choice.
5. Enforce purpose and access boundaries technically. Prevent production data from silently entering logs, analytics, support tools, exports, AI systems, or secondary product uses.
6. Select vendors only after reviewing contracts, data uses, subprocessors, locations, security, retention, deletion, export, training, telemetry, and exit behavior.
7. Define retention from business and legal needs, not storage convenience. Automate deletion across primary stores, indexes, caches, derived data, vendors, and scheduled backup expiry.
8. Design identity verification and abuse resistance for access, correction, export, deletion, and account-transfer requests without collecting excessive new data.
9. Test denied consent, withdrawal, opt-out signals, export completeness, deletion, account closure, vendor failure, backup expiry, and logging redaction.
10. Re-review when purpose, data, audience, jurisdiction, vendor, AI use, pricing model, or policy changes.

## Required Output

- data inventory and end-to-end flow map
- purpose and necessity matrix with unresolved legal questions
- user notice, choice, withdrawal, and rights workflow
- access, retention, deletion, backup, and vendor controls
- analytics, tracking, AI, and secondary-use boundaries
- privacy-focused test evidence
- owners, review triggers, incident path, and exit plan

## Completion Gate

Do not call the design complete until every data category has a necessary purpose, owner, destination, retention rule, and deletion path; unexpected secondary uses are blocked; and rights workflows are tested. Only qualified reviewers can make jurisdiction-specific compliance determinations.

## Conditional Reference

Read [Privacy Evidence](references/privacy-evidence.md) when creating the data map, minimization rules, user controls, or review boundary.
