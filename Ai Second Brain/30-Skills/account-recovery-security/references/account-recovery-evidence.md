# Account Recovery Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [NIST SP 800-63B-4](https://pages.nist.gov/800-63-4/sp800-63b.html) defines account recovery as regaining control after loss of authenticators and recognizes saved recovery codes, issued recovery codes, recovery contacts, repeated identity proofing, and risk-analysed application-specific methods. It requires recovery notification and distinguishes replacement after authentication with another factor from account recovery.
- [NIST SP 800-63-4 publication record](https://www.nist.gov/publications/nist-sp-800-63-4-digital-identity-guidelines) confirms the final 2025 revision family and supersession of SP 800-63-3. Apply its assurance language according to the product and jurisdiction rather than claiming universal certification.
- [WebAuthn Level 3](https://www.w3.org/TR/webauthn-3/) became a W3C Recommendation on 2026-08-25. Origin-bound public-key credentials improve phishing resistance, but applications still own enrollment, credential inventory, sync assumptions, lost-device recovery, account linking, and removal.
- [OWASP Forgot Password Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) calls for consistent existence-neutral responses and timing, cryptographically random single-use expiring tokens, secure storage, normal post-reset login, and session invalidation. Its suspected-compromise guidance also calls for independent established evidence and review of unauthorized account changes.
- [CISA phishing-resistant MFA guidance](https://www.cisa.gov/sites/default/files/2023-01/fact-sheet-implementing-phishing-resistant-mfa-508c.pdf) ranks FIDO/WebAuthn and PKI above phishable methods and identifies SMS and voice exposure to phishing, SS7, and SIM-swap attacks. Weaker fallback can erase the benefit of stronger primary authentication.
- [CISA mobile communications guidance](https://www.cisa.gov/sites/default/files/2024-12/guidance-mobile-communications-best-practices.pdf) warns that some services default to SMS in recovery and recommends disabling weak methods where feasible and protecting carrier accounts against SIM swap.

## Decision Implications

- Measure the account's practical assurance by its weakest successful recovery route, including customer support and channel changes.
- Recovery proof should come from evidence established before the incident. Recently added phone numbers, addresses, sessions, and authenticators may be attacker-controlled.
- Recovery is a state transition, not one token check. Successful restoration includes compromise review, revocation, new authenticator binding, notifications, delayed high-risk actions where warranted, and user appeal.
- Strong proof can still exclude legitimate users. Test accessibility, device loss, travel, disability, name and address changes, and unavailable channels without substituting public biographical questions.
- Notifications must not contain secrets and should go to safe established channels, including for failed or reversed recovery when that helps the user detect abuse.
