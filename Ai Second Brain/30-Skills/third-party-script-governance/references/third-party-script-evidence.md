# Third-Party Script Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [OWASP Third Party JavaScript Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Javascript_Management_Cheat_Sheet.html) treats supplier scripts as same-page privilege and change-control risks, including arbitrary execution and sensitive-data leakage. It recommends inventory, controlled hosting or collection, sandboxing, integrity, and governance; a tag-manager data layer is not a sandbox.
- [OWASP Web Frontend Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Web_Frontend_Security_Cheat_Sheet.html) covers client-side injection, third-party origin trust, secure communication, sensitive data, and dependency controls. It is defensive guidance, not proof that a selected integration is safe.
- [HTML Standard: scripting](https://html.spec.whatwg.org/multipage/scripting.html) is the living normative definition for classic scripts, modules, import maps, integrity metadata, cross-origin behavior, and referrer policy. Browser support and exact semantics still require target testing.
- [Subresource Integrity](https://www.w3.org/TR/SRI/) defines integrity metadata for fetched resources. [SRI Level 2](https://www.w3.org/TR/sri-2/) is a Working Draft dated 2026-03-20, so draft features are not a stable production baseline.

## Decision Implications

- Prefer eliminating a third-party script over accumulating compensating controls. If code runs in the application origin, design as though it can read and change everything exposed to ordinary page script.
- Integrity metadata helps only when the expected bytes are known and the delivery path supports it; it does not constrain an approved script's behavior, downstream calls, or data access.
- Dynamic tag containers are release systems. They need exact access roles, change review, environment promotion, audit, emergency disablement, and the same privacy and security gates as application deployment.
- Sandboxed cross-origin frames can reduce DOM reach, but permissions, navigation, messaging, storage, identity, accessibility, and data transfer remain explicit contracts.
