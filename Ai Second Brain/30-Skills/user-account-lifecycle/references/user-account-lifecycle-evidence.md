# User Account Lifecycle Evidence

Verified: 2026-10-25

## Current Standards and Guidance

- [NIST SP 800-63A-4 subscriber accounts](https://pages.nist.gov/800-63-4/sp800-63a/accounts/) requires a unique subscriber account from enrollment through closure, a unique identifier, validated changes to core attributes, notices for updates and suspension or termination, and disposal after termination according to documented retention requirements. This is final United States government digital-identity guidance, not a universal product, legal, or assurance mandate.
- [NIST SP 800-63C-4 federation requirements](https://pages.nist.gov/800-63-4/sp800-63c/Federation/) distinguishes the relying party's local account lifecycle from the identity provider's account, requires an authenticated existing account for federated-identity linking, and addresses unlinking, disabling, termination, deprovisioning, notices, and attribute minimization. Its normative requirements apply within its stated assurance and government scope.
- [OpenID Connect Core 1.0 with errata set 2](https://openid.net/specs/openid-connect-core-1_0.html) makes the `iss` plus `sub` pair the stable federated identifier. It explicitly warns that email, phone number, preferred username, and name can change or be reused and must not identify the user uniquely.
- [RFC 7643](https://www.rfc-editor.org/rfc/rfc7643.html) defines a stable, non-reassignable SCIM resource `id`, a provisioning-domain-scoped `externalId`, and a provider-defined `active` administrative state. These fields model directory resources; they do not define a product account, tenant, entitlement, billing, retention, or deletion policy.
- [RFC 7644](https://www.rfc-editor.org/rfc/rfc7644.html) defines SCIM create, read, replace, patch, delete, filtering, versioning, bulk, and security behavior. A successful provisioning operation is not proof that every application dependency converged or that retained personal data was erased.
- The [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) recommends reauthentication after recovery, suspicious activity, and sensitive account changes, followed by appropriate session rotation or invalidation. It is maintained practitioner guidance, not a protocol specification or compliance certificate.

## Decision Implications

- Keep the product account identifier independent from usernames, addresses, authenticators, and provider subjects. This permits those bindings to change without changing ownership.
- Treat account linking as an authenticated security transition. Attribute similarity alone is insufficient and can convert a sign-in convenience into account takeover.
- Model disabled access, terminated identity bindings, product closure, anonymization, and verified deletion as different outcomes with different evidence.
- Treat enterprise provisioning as scoped desired-state input. Preserve local product invariants, continuously enforce authorization, reconcile missed or reordered events, define what happens when upstream and local lifecycle policy disagree, and do not let one organization's deprovisioning signal disable unrelated access.
- Reusing an address or username must never revive the prior account's sessions, privileges, content, billing state, or private data unless an explicitly verified restoration policy permits it.
