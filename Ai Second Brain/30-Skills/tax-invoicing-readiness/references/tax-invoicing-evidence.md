# Tax and Invoicing Evidence

Verified: 2026-10-22

## Primary and Provider Sources

- [OECD VAT policy and administration](https://www.oecd.org/en/topics/sub-issues/vat-policy-and-administration.html) routes to the International VAT/GST Guidelines and digital toolkits for cross-border services and intangibles. It is a global policy framework, not the operative law or rate for a particular transaction.
- [European Commission VAT guidelines](https://taxation-customs.ec.europa.eu/taxation/vat/commission-guidelines-vat_en) describes EU e-commerce guidance and the One Stop Shop. The Commission labels this material practical and informal; it does not replace legislation, implementing rules, or jurisdiction-specific advice.
- [European Commission VAT invoicing](https://taxation-customs.ec.europa.eu/taxation/vat/vat-businesses/invoicing_en) summarizes when EU VAT invoices are required and the information they contain. Member-state rules and the exact transaction still control.
- [IRS Publication 583](https://www.irs.gov/publications/p583) identifies invoices, receipts, statements, journals, and ledgers as supporting records and requires computerized records to remain legible and reconcilable to books and returns. It is introductory United States federal guidance, not a complete sales-tax or international rulebook.
- [Stripe tax IDs with invoicing](https://docs.stripe.com/tax/invoicing/tax-ids) documents provider behavior for displaying and asynchronously validating supported tax identifiers. Stripe states that the business remains responsible for customer-data accuracy and that some tax treatment can depend on identifier format rather than completed validation; this is a provider contract to test, not a legal conclusion or provider approval.

## Decision Implications

- Start with legal and economic roles, not with a tax API. A calculator can implement a supported rule only after the seller, product, customer, location, registration, and effective date are known.
- Model registration, calculation, invoice issuance, return filing, payment or remittance, and accounting as separate responsibilities. A provider may cover only some of them and may rely on facts supplied by the application.
- Version product classifications, rates, evidence, invoice rules, and corrections by effective date. Historical reproduction is required when rules or providers change.
- Treat invoices and tax identifiers as sensitive business records. Access, retention, correction, export, and deletion must follow the applicable legal and accounting boundary rather than a generic privacy default.
- This evidence does not determine nexus, establishment, place of supply, taxability, rate, exemption, marketplace-facilitator status, invoice validity, or filing treatment for a project. Escalate those conclusions to a qualified adviser in the relevant jurisdiction.
