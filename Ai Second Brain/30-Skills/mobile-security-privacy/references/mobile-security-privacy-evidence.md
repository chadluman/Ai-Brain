# Mobile Security and Privacy Evidence

Verified: 2026-10-21

## Verification Baseline

- [OWASP Mobile Application Security Verification Standard](https://mas.owasp.org/MASVS/) organizes mobile controls across storage, cryptography, authentication and authorization, network communication, platform interaction, code quality, resilience, and privacy.
- [OWASP Mobile Application Security Testing Guide](https://mas.owasp.org/MASTG/) supplies technical procedures for verifying MASVS controls through applicable tests, techniques, and platform knowledge.
- [OWASP MASTG testing tools](https://mas.owasp.org/MASTG/tools/) warns that tool output can contain false positives and false negatives, compatibility varies, and a tool does not provide a conclusive security result. Tools listed there remain untrusted executable assets until individually reviewed.

## Android Platform Evidence

- [Android security checklist](https://developer.android.com/privacy-and-security/security-tips) describes platform sandboxing, permissions, secure framework facilities, authentication considerations, and application security checks.
- [Android security best practices](https://developer.android.com/privacy-and-security/security-best-practices) covers private storage, safe inter-app sharing, URI grants, WebView risks, permissions, network security, dependency updates, and other implementation controls.
- [Android privacy guidance](https://developer.android.com/privacy-and-security/about) emphasizes data minimization, permissions, user transparency, and current platform privacy behavior.

## Apple Platform Evidence

- [Apple Platform Security: Data Protection overview](https://support.apple.com/guide/security/data-protection-overview-secf6276da8a/web) documents per-file platform encryption and data-protection classes. Automatic platform protection does not decide which data the app should store or expose.
- [Apple Platform Security: App security overview](https://support.apple.com/guide/security/app-security-overview-sec35dd877d0/web) describes code signing, sandboxing, distribution, notarization, and mediated data access as platform layers.
- [Apple Keychain Services](https://developer.apple.com/documentation/security/keychain-services) is the official developer boundary for storing passwords, keys, certificates, and other small secrets on Apple platforms. Access policy and lifecycle still require project design and testing.

## Interpretation Boundaries

- MASVS is a requirements baseline and MASTG is testing guidance; neither certifies an application by itself.
- Root or jailbreak detection, obfuscation, attestation, and anti-tamper controls raise attacker cost but must not move server authorization or financial invariants onto the client.
- Device encryption and sandboxes reduce exposure but do not prevent leaks through backups, UI surfaces, logs, analytics, notifications, screenshots, clipboard, exported components, or compromised runtimes.
- Certificate pinning can create availability and recovery failures. Use it only when the threat model justifies it and key rotation and emergency bypass are safely designed.
- Store privacy labels and policy forms change and are declarations, not independent verification. Recheck at every release and compare them with the actual binary and traffic.

## Re-Review Triggers

- new sensitive data, permission, entitlement, SDK, WebView, deep-link route, or distribution channel
- major OS, MASVS, MASTG, privacy-policy, platform-security, or store-declaration change
- dependency advisory, breach, unexpected endpoint, runtime data mismatch, or security finding
- new fraud threat, regulatory scope, device-attestation requirement, or end-of-life event
