# User Administration Console Evidence

Verified 2026-10-25. These sources support the interaction and security constraints below; they do not approve a component library, administrative product, or implementation.

## Source Roles

- [OWASP Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) supports deny-by-default, per-request authorization, protected-resource scoping, and tests against horizontal and vertical privilege escalation.
- [OWASP Mass Assignment Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html) supports dedicated input objects and field allow-lists so administrative endpoints do not accidentally accept sensitive attributes.
- [OWASP Transaction Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html) supports presenting and binding approval to the exact significant action data.
- [CISA and NSA IAM Best Practices for Administrators](https://www.cisa.gov/sites/default/files/2023-12/ESF%20IDENTITY%20AND%20ACCESS%20MANAGEMENT%20RECOMMENDED%20BEST%20PRACTICES%20FOR%20ADMINISTRATORS%20PP-23-0248_508C.pdf) provides defensive evidence for separate administration, phishing-resistant authentication, least privilege, and audited privileged access.
- [W3C WAI Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/) explains semantic relationships among captions, headers, rows, and data cells.
- [WAI-ARIA APG Grid Pattern](https://www.w3.org/WAI/ARIA/apg/patterns/grid/) defines the substantial keyboard interaction contract introduced by an interactive grid; APG examples are not normative conformance guarantees.
- [WAI-ARIA APG Dialog Pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/) covers dialog labeling, contained focus, close controls, focus return, and cautious initial focus for hard-to-reverse actions.
- [USWDS Table](https://designsystem.digital.gov/components/table/) and [Pagination](https://designsystem.digital.gov/components/pagination/) provide maintained public guidance for readable columns, sort announcements, responsive table variants, current-page meaning, and bounded or unbounded result sets.

## Decision-Relevant Constraints

- A table row or disabled control is presentation, not enforcement. Recompute field and command authorization from trusted state at execution and again for every item in bulk work.
- Prefer a semantic table for tabular reading. An ARIA grid changes focus and keyboard behavior; use it only when the richer interaction is essential and can be tested across supported assistive technologies.
- Sorting, filtering, pagination, virtualization, and live updates must preserve the user's understanding of result scope. A bulk action must name whether it targets selected rows, a frozen result set, or a re-evaluated query.
- Risky confirmations should state actor context, target, scope, consequences, timing, notifications, reversibility, and blocked or excluded items. Generic “Are you sure?” dialogs do not provide transaction meaning.
- For a hard-to-reverse dialog, placing initial focus on a non-destructive action can reduce accidental confirmation. Focus placement still depends on content order and must not hide the explanation.
- Administrative create and update endpoints should accept command-specific fields. Field allow-lists do not replace resource, tenant, state, and operation authorization.
- Privileged access must be attributable and time-bounded where appropriate. The console should visibly distinguish routine use, elevation, impersonation, emergency access, and approval state.

## Boundaries

USWDS and APG provide patterns, not a mandatory visual system or proof of accessibility. CISA guidance targets defensive administrative practice and must be adapted to the product. OWASP guidance is not a penetration-test result or certification.
