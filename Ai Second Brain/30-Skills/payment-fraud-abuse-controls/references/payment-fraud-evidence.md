# Payment Fraud and Abuse Evidence

Verified: 2026-10-22

## Standards and Regulatory Evidence

- [PCI SSC Document Library](https://www.pcisecuritystandards.org/document_library/) records PCI DSS v4.0.1 as the current PCI DSS baseline at verification. Scope and validation remain questions for the acquiring or qualified compliance parties.
- [PCI SSC FAQ 1588](https://www.pcisecuritystandards.org/faqs/1588/) explains the PCI DSS v4.0.1 SAQ A eligibility boundary for scripts affecting embedded payment pages and directs merchants to confirm applicability with the entity accepting their compliance evidence.
- [PCI SSC payment-page and e-skimming guidance](https://blog.pcisecuritystandards.org/new-information-supplement-payment-page-security-and-preventing-e-skimming) focuses on authorized scripts, integrity, and change detection for payment pages. It supplements rather than replaces PCI DSS requirements.
- [EMVCo 3-D Secure](https://www.emvco.com/emv-technologies/3-d-secure/) describes issuer-merchant data exchange and risk-based step-up authentication for card-not-present payments. At verification, the page listed published 2.3.1 materials and a 2.4 draft; implementation must confirm the versions supported by the selected providers and region.
- [NIST SP 800-63-4](https://www.nist.gov/publications/nist-sp-800-63-4-digital-identity-guidelines), published August 2025, supersedes SP 800-63-3 and covers identity proofing, authentication, federation, security, privacy, fraud, and customer-experience considerations. It is not a card-network rule or a complete payment-fraud standard.
- [European Banking Authority SCA Q&A](https://www.eba.europa.eu/single-rule-book-qa/qna/view/publicId/2018_4031) illustrates that strong-customer-authentication applicability depends on how a transaction is initiated and the applicable PSD2 rules. Recheck the current legal framework and obtain qualified advice for the target payment flow.

## Decision Implications

- Outsourced or embedded payment collection can reduce scope, but the merchant page, scripts, accounts, integrations, and operational processes can still affect payment security and validation duties.
- Authentication and authorization answer different questions. A transaction can be authenticated and still be abusive, coerced, misclassified, or fulfilled to the wrong party.
- Risk data is personal or sensitive when it can identify, profile, locate, or disadvantage a person. Use data minimization and purpose limits as design constraints, not after-the-fact documentation.
- Fraud labels arrive late and can be wrong. Keep provenance and confidence, prevent feedback loops, and evaluate both prevented loss and harm to legitimate customers.
- Standards and provider controls are inputs to a project policy. They do not approve a provider, guarantee fraud prevention, transfer every liability, or replace qualified compliance and legal review.
