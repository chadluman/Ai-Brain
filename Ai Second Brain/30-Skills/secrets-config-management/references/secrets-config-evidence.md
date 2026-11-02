# Secrets and Configuration Evidence

Verified: 2026-10-21

## Primary Guidance

- [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html) covers centralized and standardized management, least privilege, automation, lifecycle, metadata, CI/CD, injection, detection, logging, and cloud-provider considerations.
- [OWASP Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html) distinguishes key storage from ordinary configuration and warns against keys in source, version control, and weakly protected configuration.
- [SPIFFE standard](https://spiffe.io/docs/latest/spiffe-specs/) defines a vendor-neutral workload-identity framework for heterogeneous systems.
- [SPIFFE Workload API](https://spiffe.io/docs/latest/spiffe-specs/spiffe_workload_api/) defines stable profiles for workloads to obtain and receive updated verifiable identity documents. It is a complex infrastructure choice, not a default requirement for small applications.
- [GitHub Actions OIDC guidance](https://docs.github.com/en/actions/concepts/security/openid-connect) documents a provider-specific way for workflows to exchange short-lived identity tokens for cloud access instead of storing long-lived cloud credentials.

## Interpretation Boundaries

- Environment variables are a transport mechanism, not a secret store, and may be visible to processes, diagnostics, or dumps depending on the platform.
- A managed secret store centralizes controls but becomes an availability and trust dependency. Define cache, startup, outage, and recovery behavior.
- Rotation frequency should follow secret type, threat, issuer capability, and recovery risk. Forced user-password rotation is a separate identity-policy question.
- Secret scanners have false positives and false negatives. Use multiple preventive controls and an incident process rather than treating scanning as proof.
