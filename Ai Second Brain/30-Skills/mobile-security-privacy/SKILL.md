---
name: mobile-security-privacy
description: Threat-model and review security and privacy controls for iOS, Android, or cross-platform mobile apps across local storage, credentials, network traffic, platform interaction, permissions, WebViews, logs, backups, screenshots, resilience, and data declarations. Use before release or when adding sensitive data, native capabilities, or third-party SDKs.
---

# Mobile Security and Privacy

## Outcome

Produce a risk-based mobile control and verification plan that protects users even when devices, networks, app packages, inter-app inputs, SDKs, and local execution environments cannot be fully trusted.

## Required Inputs

- application architecture, target platforms and versions, distribution channels, backend boundaries, and supported device states
- data inventory, sensitivity, retention, residency, offline storage, backup, export, deletion, and notification behavior
- authentication, session, device binding, biometrics, authorization, recovery, and high-impact actions
- permissions, entitlements, intents, URL handlers, WebViews, extensions, IPC, clipboard, screenshots, logs, analytics, crash reporting, and third-party SDKs
- abuse cases, regulated obligations, adversary capability, fraud exposure, and resilience requirements

## Safety and Permission Constraints

- Treat the client, device, local clock, network, app package, accessibility surface, and runtime state as potentially attacker-controlled. Enforce authorization and business invariants on a trusted server boundary.
- Platform sandboxing, device encryption, key stores, code signing, app attestation, root detection, obfuscation, and certificate pinning are defense layers, not proof of confidentiality or trustworthy execution.
- Never hardcode server secrets or ship credentials that must remain confidential. A distributed client cannot keep a universal secret from its operator.
- Request the minimum permissions and entitlements at the moment of need. Provide a useful denied and revoked path, and keep store privacy declarations consistent with observed code and SDK behavior.
- Do not add security testing tools, SDKs, certificates, interception profiles, rooted devices, or sample apps without exact-version review and an isolated, authorized test environment with dummy data.
- Testing a production app, bypassing controls, accessing real user data, changing store declarations, rotating production credentials, or publishing a build is R3 and requires immediate authorization and a rollback plan.

## Workflow

1. Create a mobile-specific threat model across package, device, local storage, backups, inter-app communication, deep links, WebViews, network, APIs, notifications, logs, build pipeline, distribution, and third-party SDK boundaries.
2. Select applicable OWASP MASVS control groups and map them to project threats and data. Use MASTG tests as verification procedures, not as a one-size-fits-all tool list.
3. Minimize data and capability. Inventory every permission, entitlement, identifier, SDK, analytics event, crash field, pasteboard use, background mode, and network destination with a documented purpose and owner.
4. Classify local data by lock state, account state, backup eligibility, retention, sharing, and deletion. Use reviewed platform storage and key facilities, and prevent sensitive material from entering logs, caches, screenshots, notifications, or shared containers without need.
5. Use TLS with platform trust validation. Authenticate the server, bind sessions appropriately, rotate and revoke tokens, and avoid custom cryptography. Add pinning only for a justified threat model with safe key rotation and outage recovery.
6. Harden platform interaction: validate deep links and intents, restrict exported components and IPC, isolate untrusted web content, minimize JavaScript bridges, constrain file sharing, and treat clipboard and accessibility exposure as data flows.
7. Enforce sensitive transactions on the backend with fresh authorization and replay protection. Local biometrics can release a local key or improve UX but must not be the sole server authorization signal.
8. Review dependencies and SDKs for provenance, permissions, install behavior, data collection, network destinations, advisories, update policy, and removal. Reconcile privacy declarations against observed runtime traffic and data use.
9. Build a verification matrix using static review, unit and integration tests, platform analysis, controlled dynamic tests, backend negative tests, and MASTG procedures applicable to the threat model.
10. Test logout, account switch, device loss, revoked permissions, expired and stolen tokens, restored backups, malicious links and intents, hostile networks, tampered responses, old app versions, offline states, and compromised-device assumptions.
11. Record residual risk, exceptions, evidence, release owner, monitoring, incident response, credential rotation, remote revocation, forced-update criteria, and end-of-life deletion behavior.

## Required Output

- mobile threat model and data-flow inventory
- scoped MASVS control profile with rationale and mapped MASTG evidence
- permission, entitlement, SDK, identifier, and network-destination register
- local storage, key, backup, log, screenshot, notification, and deletion controls
- authentication, session, backend authorization, WebView, IPC, and link controls
- platform and backend verification results with residual risks
- privacy-declaration reconciliation, incident, revocation, rollback, and end-of-life plan

## Completion Gate

Do not call the app secure or privacy-compliant. Release readiness requires scoped controls to have reproducible evidence, high-impact findings to be resolved or explicitly accepted by an authorized owner, declarations to match actual behavior, and residual risk to be documented. High-risk or regulated applications require qualified independent review.

## Conditional Reference

Read [Mobile Security and Privacy Evidence](references/mobile-security-privacy-evidence.md) before selecting controls or tests. Use [Application Threat Modeling](../application-threat-modeling/SKILL.md), [Privacy and Data Governance](../privacy-data-governance/SKILL.md), and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for their respective boundaries.
