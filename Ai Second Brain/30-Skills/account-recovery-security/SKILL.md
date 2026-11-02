---
name: account-recovery-security
description: Design or review secure account and authenticator recovery, password reset, lost-device handling, support-assisted recovery, and post-compromise restoration. Use when recovery or high-risk identity changes could bypass normal authentication or enable account takeover.
---

# Account Recovery Security

## Outcome

Produce a recovery system that restores legitimate access without becoming a weaker alternate login path, detects and contains takeover, protects user privacy, supports accessible help, and leaves auditable evidence without sensitive recovery material.

Use [Identity and Authentication Selection](../identity-auth-selection/SKILL.md) for assurance and authenticator choices, [Customer Support Readiness](../customer-support-readiness/SKILL.md) for support operations, and [Incident Response](../incident-response/SKILL.md) when compromise is suspected. This skill owns recovery proof, state transitions, and restoration controls.

## Required Inputs

- account value, user population, identity-proofing history, target authentication assurance, regulated or high-harm actions, and likely takeover paths
- bound authenticators, saved or issued recovery codes, prearranged contacts, verified channels, devices, sessions, and support capabilities
- email and phone ownership risks, SIM swap, mailbox compromise, lost devices, shared devices, accessibility, travel, and exclusion concerns
- identity, authenticator, password, recovery address, phone, payment, payout, tenant, role, and ownership change journeys
- notification, cooldown, rate, fraud review, appeal, retention, privacy, deletion, and legal constraints

## Safety and Permission Constraints

- Recovery is an authentication path and may define the effective assurance of the account. Do not rely on knowledge-based questions, public personal data, or recently changed recovery information as sole proof.
- Do not reveal whether an account exists through messages, timing, rate behavior, support scripts, or analytics. Do not send passwords or reusable secrets.
- Store recovery codes as verifier material using protection appropriate to their entropy and use; never store plaintext codes, real user data, identity documents, support recordings, or reset tokens in the vault.
- Avoid SMS or email as the only recovery proof for high-value accounts when takeover of that channel is a credible threat. A convenient fallback must not silently defeat phishing-resistant sign-in.
- Resetting real accounts, changing authenticators or recovery channels, viewing identity evidence, revoking sessions, or locking users out is R3 and requires immediate authorization, accountable operators, and a reversal or appeal route.

## Workflow

1. Model recovery separately for ordinary lost-authenticator, forgotten-password, locked-out, suspected-compromise, deceased or transferred owner, managed workforce, and high-value administrative cases. Define success, unacceptable false acceptance, and unacceptable exclusion for each.
2. Inventory existing authenticators, trusted devices, sessions, recovery codes and contacts, proofing records, channel age, recent changes, and support evidence. State which combinations can satisfy each recovery level.
3. Prefer pre-enrolled, independent evidence: remaining strong authenticators, single-use recovery codes, prearranged contacts, or repeated identity proofing. Require multiple independent signals, cooldown, or manual escalation when harm is high.
4. Build reset requests with uniform public responses and bounded timing. Use random, single-use, short-lived, purpose- and account-bound tokens; rate limit by account, source, device, and channel without creating denial-of-service lockouts.
5. Protect recovery-channel and authenticator changes as step-up events. Reauthenticate with an existing strong factor where possible, notify established channels, expose pending changes, delay high-risk effects when justified, and provide a safe cancel or report route.
6. Treat support-assisted recovery as privileged access: verified operator identity, minimal evidence display, scripts that resist social engineering, separation or approval for high-impact cases, no operator-chosen new authenticator, complete decision reason, and appeal.
7. After successful recovery, bind new authenticators deliberately; revoke compromised authenticators, active sessions, refresh tokens, outstanding recovery links and codes; review profile, recovery, MFA, API key, payout, and authorization changes; and notify through all safe established channels.
8. Detect enumeration, spraying, token guessing, SIM swap or mailbox takeover indicators, recent-channel abuse, help-desk coercion, repeated failed claims, impossible location or device shifts, and recovery followed by sensitive action. Limit collected telemetry to defined purposes and retention.
9. Test legitimate lost-device and accessibility journeys plus enumeration, replay, token theft, expired and wrong-account tokens, concurrent requests, channel change races, recovery-code reuse, compromised mailbox or phone, support social engineering, notification failure, provider outage, and false-positive appeal.
10. Document lockout, degraded-mode, incident, customer communication, rollback, data deletion, and provider exit procedures. Never weaken proof silently during an outage.

## Required Output

- recovery threat model, assurance targets, evidence combinations, state machine, and user journeys
- reset token, recovery code and contact, channel-change, authenticator lifecycle, notification, cooldown, revocation, and post-compromise rules
- support authority, approvals, evidence minimization, scripts, audit fields, escalation, appeal, and operator-safety design
- abuse signals, rate and privacy controls, monitoring, incident, outage, migration, and rollback plan
- accessibility and adversarial test evidence with false-acceptance and false-rejection review

## Completion Gate

Do not call recovery ready until no recovery path is an unexplained assurance downgrade, existence is not disclosed, all tokens and codes are bounded and single-use, recent or weak channels cannot independently take over high-value accounts, post-recovery sessions and authenticators are contained, support powers are constrained, users are notified and can appeal, and negative and accessibility tests pass.

## Conditional Reference

Read [Account Recovery Evidence](references/account-recovery-evidence.md) when selecting recovery methods, notification and reset controls, phishing-resistant authenticators, or support-assisted safeguards.
