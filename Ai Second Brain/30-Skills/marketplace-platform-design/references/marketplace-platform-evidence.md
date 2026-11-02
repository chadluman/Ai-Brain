# Marketplace Platform Evidence

Verified: 2026-10-22

## Government and Provider Evidence

- [FinCEN payment-processor administrative ruling](https://www.fincen.gov/resources/statutes-regulations/administrative-rulings/application-money-services-business) states that United States money-transmitter analysis depends on the facts and circumstances and that a payment-processor exemption has specific conditions. The ruling addresses one described business pattern and is not blanket marketplace approval.
- [FinCEN: Am I an MSB?](https://www.fincen.gov/am-i-msb) summarizes categories of money services businesses and associated Bank Secrecy Act obligations. It is a routing resource, not a substitute for counsel or current federal and state analysis.
- [FTC INFORM Consumers Act](https://www.ftc.gov/legal-library/browse/statutes/inform-consumers-act) identifies United States duties for covered online marketplaces concerning information collection and verification, seller disclosure, data protection, suspension, and consumer reporting mechanisms. Coverage depends on the statutory definitions and facts.
- [European Commission Digital Services Act](https://digital-strategy.ec.europa.eu/en/policies/digital-services-act) describes duties for covered online intermediaries and marketplaces, including seller transparency and product-traceability measures. Exact duties, exemptions, category rules, and enforcement require current EU and member-state review.
- [Stripe Connect separate charges and transfers](https://docs.stripe.com/connect/separate-charges-and-transfers) documents one provider-specific model that decouples a platform charge from transfers to one or more connected accounts. In that model, the platform balance bears specified fees, refunds, and chargebacks; this is implementation evidence, not an approval or universal marketplace architecture.

## Decision Implications

- Product labels such as platform, marketplace, processor, agent, or facilitator do not decide legal status. Contracts, control, possession of funds, transaction sequence, geography, and actual operations do.
- A managed payment product can implement onboarding and fund movement while leaving the platform with material verification, disclosure, data, seller, moderation, tax, support, and consumer duties.
- Identity and bank evidence collected for marketplace compliance creates a high-impact data boundary. Prefer direct provider collection when suitable, restrict platform access, and document how users correct or remove data.
- Marketplace topology is an architecture decision. Directory, direct-seller, platform-collection, and merchant-of-record models create different control, cost, liability, user experience, reconciliation, and exit profiles.
- This evidence does not determine money-transmitter, merchant-of-record, marketplace-facilitator, employment, agency, product-safety, tax, sanctions, or content status for a specific project. Obtain qualified review before commitment.
