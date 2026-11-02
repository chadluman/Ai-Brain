# Threat Modeling Evidence

Verified: 2026-10-21

## Security Guidance

- [OWASP Threat Modeling Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Threat_Modeling_Cheat_Sheet.html) structures the work around what is being built, what can go wrong, what to do, and whether the result is sufficient. It covers system models, trust boundaries, threat techniques, responses, and validation.
- [OWASP Business Logic Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Business_Logic_Security_Cheat_Sheet.html) extends analysis beyond technical architecture to workflow order, repetition, concurrency, automation, and value-producing invariants.
- [CISA Secure by Design](https://www.cisa.gov/securebydesign) treats threat modeling and ownership of customer security outcomes as part of product design, not a post-release add-on.

## Decision Boundaries

- There is no universal technique that guarantees coverage. Choose prompts for the system and harms, and document what the method does not address.
- The OWASP Abuse Case Cheat Sheet is explicitly marked historical; use the maintained Threat Modeling and Business Logic guidance instead of treating that archived tutorial as current authority.
- A data-flow diagram is a model, not evidence that deployed identity, network, storage, or administrative boundaries match it. Verify configuration and runtime behavior.
- Threats that cannot yet be mitigated still need an explicit owner, monitoring or containment, review date, and authorized residual-risk decision.
