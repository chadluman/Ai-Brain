# Account Management Experience Evidence

Verified 2026-10-25. These sources constrain design decisions; they do not certify an implementation or replace product-specific threat, privacy, accessibility, and legal review.

## Source Roles

- [NIST SP 800-63A-4 subscriber accounts](https://pages.nist.gov/800-63-4/sp800-63a/accounts/) distinguishes subscriber-account maintenance, suspension, termination, notifications, and retention-aware disposal in its government digital-identity scope.
- [NIST SP 800-63B-4](https://csrc.nist.gov/pubs/sp/800/63/B/4/final) provides current authenticator, session, recovery, phishing-resistance, and assurance evidence; the product must still choose an appropriate assurance context.
- [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) covers reauthentication after risk events and protection for sensitive account changes.
- [OWASP Transaction Authorization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transaction_Authorization_Cheat_Sheet.html) supports binding authorization to the exact operation and presenting significant transaction data before approval.
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) is the normative accessibility baseline, including error prevention for data changes and accessible authentication.
- [WAI Forms Tutorial: User Notification](https://www.w3.org/WAI/tutorials/forms/notifications/) explains accessible inline and overall success or error feedback; it does not prescribe product policy or server validation.

## Decision-Relevant Constraints

- Model the stable product account separately from mutable contact, display, authentication, recovery, federation, and membership attributes.
- Reauthentication and transaction confirmation should preserve the operation the user intended, bind approval to its current target and consequences, expire safely, and fail without partially applying hidden effects.
- A successful form submission is not necessarily a completed provider or lifecycle transition. Show pending, delayed, failed, reversed, and reconciled states using authoritative status.
- Support password managers and copy and paste. Do not make recall, transcription, visual puzzles, or secret questions the only route through authentication or recovery.
- Announce validation, progress, success, and failure without unexpectedly moving focus. Give the user a clear route to the affected field, retry, cancel, dispute, or support path.
- Error prevention is strongest when risky changes are reversible or reviewed before commit. Confirmation text must describe the actual target, scope, timing, and retained effects rather than rely on a generic warning.

## Boundaries

NIST requirements apply within defined United States government digital-identity contexts and need tailoring elsewhere. OWASP guidance is defensive practitioner guidance, not a product certification. WCAG conformance depends on the complete implementation and representative testing, not on copying an example pattern.
