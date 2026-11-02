# Release Evidence

Verified 2026-10-21. Provider controls are examples to evaluate after a platform is selected, not universal defaults.

- [SLSA 1.2](https://slsa.dev/spec/v1.2/about) defines supply-chain tracks, levels, and verifiable build and source evidence. Select a target from the project's threat model and verify artifact provenance at consumption.
- [Google SRE: Canarying Releases](https://sre.google/workbook/canarying-releases/) defines a canary as a partial, time-limited deployment evaluated against a control. It emphasizes smaller releases, observable comparison, and pause or rollback when the candidate degrades the system.
- [GitHub Actions secure use](https://docs.github.com/en/actions/reference/security/secure-use) documents platform-specific workflow threats, permissions, dependency updates, and short-lived cloud authentication. Apply only when GitHub Actions is a selected candidate.
- [GitHub deployment environments](https://docs.github.com/en/actions/concepts/workflows-and-actions/deployment-environments) documents environment approvals, branch restrictions, protection rules, deployment history, and delayed secret access.
- [GitHub Actions OIDC](https://docs.github.com/en/actions/concepts/security/openid-connect) describes exchanging workflow identity for short-lived provider tokens rather than storing long-lived provider credentials. The provider trust policy remains a critical configuration boundary.

## Release Proof

For a release, retain the source revision, reviewed change, dependency lock, builder identity, artifact digest, provenance or attestation, tests and scanners actually run, approver where required, deployment target, configuration version, start and finish, verification signals, result, and rollback or incident link.

Do not retain secret values or unnecessary personal data in that evidence.
