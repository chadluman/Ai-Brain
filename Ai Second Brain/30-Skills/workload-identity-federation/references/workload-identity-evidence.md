# Workload Identity Federation Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [NIST SP 800-207](https://csrc.nist.gov/pubs/sp/800/207/final) defines zero trust around resources rather than network segments and rejects implicit trust based solely on location or ownership. Subject and device authentication and authorization are discrete decisions before resource access.
- [NIST SP 800-207A](https://csrc.nist.gov/pubs/sp/800/207/A/final) applies identity-tier access control to cloud-native, multi-cloud applications and explicitly describes application and service identities, gateways, proxies, and SPIFFE-style infrastructure. It does not make a service mesh or sidecar mandatory.
- [SPIFFE specifications](https://spiffe.io/docs/latest/spiffe-specs/) define a vendor-neutral workload identity document family. SPIFFE IDs, workload APIs, SVIDs, trust bundles, and federation provide an architecture vocabulary; a specific SPIRE or platform deployment is still an unreviewed executable system until version and configuration review.
- [RFC 8693](https://www.rfc-editor.org/rfc/rfc8693.html) defines OAuth token exchange and its subject and actor semantics. It deliberately leaves the deployment trust model and token policy to the implementation, so unrestricted exchange or impersonation is unsafe.
- [RFC 8705](https://www.rfc-editor.org/rfc/rfc8705.html) defines certificate-based OAuth client authentication and certificate-bound access tokens. It is useful only when certificate issuance, termination, forwarding, validation, renewal, revocation, and resource-server binding work end to end.
- [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html) defines DPoP proof-of-possession and token binding at the application layer. DPoP is not authorization or client authentication and requires per-request proof validation and replay handling.

## Decision Implications

- A workload identity is a verified claim about a running principal; a service account label or static API key is only one input and may be copied or reused.
- Short credential lifetime reduces exposure but increases dependence on issuance, clock, network, cache, and control-plane availability. Test degraded behavior and avoid fail-open renewal.
- Federation exchanges one trust dependency for another. Exact issuer, subject, actor, audience, environment, tenant, and resource conditions are the security boundary.
- mTLS and DPoP solve different sender-constraining problems and can fail at proxy boundaries. Verify what the resource server actually receives and checks.
- Portability requires stable application identity and authorization semantics above provider-specific subjects, plus documented export, dual-trust migration, and rollback.
