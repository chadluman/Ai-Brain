---
name: content-moderation-operations
description: Design or review user-generated and AI-generated content policy, detection, reporting, blocking, enforcement, appeals, transparency, moderator safety, and incident handling. Use when users can publish, message, upload, review, stream, or generate content visible to others; do not use it to make legal determinations or perform covert surveillance.
---

# Content Moderation Operations

## Outcome

Produce a risk-proportionate moderation system that protects users, preserves due process and accessibility, gives operators executable policy, and can explain and correct consequential decisions.

## Required Inputs

- content and interaction types, visibility, virality, discovery, messaging, live features, monetization, anonymity, and AI generation
- users, likely ages, languages, countries, vulnerable groups, creators, buyers or sellers, and distribution stores
- credible harms, illegal-content questions, platform rules, community standards, severity, likelihood, velocity, and reversibility
- reporting, blocking, filtering, age controls, human review, automation, escalation, support, appeals, and transparency capacity
- evidence, privacy, retention, law-enforcement, emergency, moderator-wellbeing, accessibility, and incident-response boundaries

## Safety and Permission Constraints

- Do not invent legal definitions of illegal, harmful, extremist, exploitative, infringing, or age-restricted content. Maintain a dated jurisdiction matrix and route high-impact determinations to qualified legal, child-safety, trust-and-safety, and subject-matter owners.
- Do not scan private communications, deploy biometric or invasive classifiers, share reports, contact authorities, preserve data beyond policy, or change production enforcement without explicit authorization and the applicable legal and privacy review.
- Automated systems can be wrong, biased, evaded, and context-blind. Use confidence and severity thresholds, human review where consequences warrant it, clear reasons, appeal, and urgent exception handling.
- Minimize exposure to harmful material. Restrict evidence access, redact unnecessary identity, separate moderator and ordinary support privileges, provide wellness controls, and never put real harmful content in the vault.
- Preserve emergency and legally required evidence only through an authorized, access-controlled process. Do not let a takedown silently destroy the audit trail or required user remedy.

## Workflow

1. Map the service features and content lifecycle from creation or upload through recommendation, sharing, monetization, reporting, restriction, removal, appeal, restoration, retention, and deletion.
2. Conduct a feature-specific risk assessment. Consider content, conduct, contact, commerce, child, privacy, intellectual-property, self-harm, fraud, harassment, non-consensual imagery, exploitation, and offline harm as applicable; score severity, likelihood, reach, velocity, and detectability.
3. Write a layered policy taxonomy: illegal or urgent escalation, prohibited by service, age or region restricted, visibility limited, user-controlled, and allowed. Define examples, context, exceptions, evidence, decision owner, and re-review date without turning examples into rigid loopholes.
4. Reduce risk through product design before moderation: audience controls, safe defaults, friction, rate and reach limits, age-appropriate design, block and mute, reply restrictions, upload constraints, provenance, recommendation controls, and creator education.
5. Provide accessible in-context reporting for content and users, blocking where interaction requires it, status and receipt, emergency route, duplicate handling, reporter privacy, anti-retaliation, misuse controls, and timely triage.
6. Combine user reports, trusted sources, deterministic rules, classifiers, sampling, and human review according to the threat. Validate language, dialect, image, audio, accessibility, and regional coverage and record model or rule version and confidence.
7. Define an enforcement state machine: no action, warning, label, age gate, reach limit, feature limit, temporary hold, removal, account restriction, suspension, ban, preservation, and restoration. Separate content action from account action and apply proportionality and consistency checks.
8. Give affected users clear, specific reasons and an accessible appeal except where prohibited or unsafe. Keep appeal independent enough for meaningful review, track reversals, and feed errors back into policy and tooling.
9. Protect moderators and operations: least privilege, assignment limits, redaction, safe previews, escalation, dual control for high-impact actions, wellness support, quality sampling, disagreement review, and incident rotation.
10. Verify current store and jurisdiction rules for the exact audience and feature. Test reporting, blocking, urgent escalation, false positive, false negative, multilingual context, coordinated abuse, appeal, restoration, account deletion, outage, and evidence retention with synthetic content.
11. Monitor prevalence and exposure, report handling, response time, reversals, repeat harm, reporter abuse, disparate error, moderator load, incidents, and transparency obligations. Do not optimize only removal volume.

## Required Output

- service and content lifecycle map plus dated risk and applicability matrix
- policy taxonomy, community standards, examples, exceptions, and decision ownership
- product prevention, reporting, blocking, detection, review, enforcement, appeal, and restoration design
- evidence, privacy, access, retention, moderator-safety, emergency, and incident controls
- coverage and quality metrics with false-positive, false-negative, language, accessibility, and user-harm tests
- store and regulatory evidence, unresolved qualified-review questions, rollout, rollback, and re-review triggers

## Completion Gate

Do not call moderation ready until high-severity risks have owned response paths, ordinary users can report and protect themselves, policies are actionable across target languages and features, consequential decisions are reviewable and reversible where appropriate, moderators are protected, store and jurisdiction evidence is current, and realistic synthetic tests expose acceptable error and recovery behavior.

## Conditional Reference

Read [Content Moderation Evidence](references/content-moderation-evidence.md) when mapping platform transparency, complaints, child-safety duties, or mobile-store user-generated-content requirements.
