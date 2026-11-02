# SMS Messaging Evidence

Verified: 2026-10-22

## Regulatory, Industry, Security, and Provider Sources

- [FCC consent order, FCC 24-24](https://docs.fcc.gov/public/attachments/FCC-24-24A1.pdf) codifies United States revocation methods, timely honoring of opt-outs, standardized reply words, and limits on confirmation messages for covered robocalls and robotexts. Applicability depends on the facts and law.
- [FCC January 2026 waiver order, DA 26-12](https://docs.fcc.gov/public/attachments/DA-26-12A1.pdf) extends until January 31, 2027 a waiver for the specific requirement to treat revocation in response to one informational message as revocation across unrelated matters. It does not suspend all consent or revocation duties; recheck status before implementation.
- [CTIA Messaging Principles and Best Practices](https://api.ctia.org/wp-content/uploads/2023/05/230523-CTIA-Messaging-Principles-and-Best-Practices-FINAL.pdf) describes industry expectations for clear calls to action, sender identity, opt-in, opt-out, support, and wanted messaging. Carrier and provider requirements can be stricter or newer.
- [Twilio A2P 10DLC](https://www.twilio.com/docs/messaging/compliance/a2p-10dlc) documents one provider's implementation of United States carrier registration, brands, campaigns, consent, sender routes, throughput, and fees. It is provider evidence only and does not approve Twilio or establish global rules.
- [NIST SP 800-63B-4 authenticators](https://pages.nist.gov/800-63-4/sp800-63b/authenticators/) classifies PSTN out-of-band authentication as restricted, requires an alternative authenticator, and calls for risk indicators such as SIM change, number porting, and abnormal behavior.

## Decision Implications

- Treat consent as sender-, purpose-, channel-, and jurisdiction-specific evidence. A telephone number on an account is not automatically permission for every message stream.
- Revocation rules can change through orders, waivers, litigation, carrier policy, and provider enforcement. Store evidence dates and recheck immediately before launch.
- Registration can require business, tax, campaign, and consent-flow data and can add recurring fees or throughput limits. Review privacy, authority, cost, and exit before submitting it.
- Provider status callbacks and carrier delivery receipts are not proof that the intended person read a message. Preserve in-product state and recovery paths.
- SMS is useful for reach but has confidentiality, reassignment, accessibility, delivery, fraud, and cost limitations. It should not be the only path for critical product access.
