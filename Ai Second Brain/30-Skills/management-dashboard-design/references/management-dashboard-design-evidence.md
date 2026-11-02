# Management Dashboard Design Evidence

Verified 2026-10-25. These sources support dashboard and visualization decisions; they do not validate a product's metrics, data, charting dependency, or management policy.

## Source Roles

- [GOV.UK: How to set performance metrics for your service](https://www.gov.uk/service-manual/measuring-success/how-to-set-performance-metrics-for-your-service) supports starting from service purpose and hypotheses, finding suitable sources, adding context, and distinguishing objective-focused dashboards from scheduled reports and event-driven alerts.
- [USWDS Data Visualizations](https://designsystem.digital.gov/components/data-visualizations/) provides maintained public guidance on common chart forms, lossless representation, plain-language intent, reduced interaction, underlying data, accessible equivalents, and manual testing.
- [USWDS Table](https://designsystem.digital.gov/components/table/) covers readable tabular comparison, concise columns, units, captions, source or last-updated context, sorting announcements, and responsive variants.
- [W3C WAI Complex Images](https://www.w3.org/WAI/tutorials/images/complex/) explains short descriptions plus complete text equivalents for charts, diagrams, and other information-dense images.
- [W3C WAI Tables Tutorial](https://www.w3.org/WAI/tutorials/tables/) explains captions and programmatic header-to-cell relationships for exact data.
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) supplies the normative accessibility baseline for perceivable, operable, understandable, and robust content.

## Decision-Relevant Constraints

- Dashboard composition starts with a decision and intended audience, not with available widgets. A metric without a decision, owner, or interpretation contract belongs in exploration or reporting until its use is defined.
- A chart should communicate one central relationship with a visible text interpretation. Provide exact values or underlying data and do not require hover, color perception, or fine pointer control to obtain essential meaning.
- Use semantic tables when exact lookup and comparison are primary. Keep units consistent within columns, provide captions and source or freshness context, and announce sort changes when sorting is interactive.
- Data freshness, completeness, sample size, filters, and revisions can change the meaning of a value as much as the value itself. Present these as part of the metric, not as hidden metadata.
- A text alternative must explain the essential information and relationships, not merely identify that an image is a chart. Complex data may need a concise insight, a structured table, and access to a fuller description or source.
- Dashboards support recurring inspection and decisions; reports support context-rich snapshots; alerts interrupt when a bounded condition needs attention. Using one artifact for all three purposes usually obscures cadence, ownership, and action.

## Boundaries

GOV.UK guidance is written for public services and its required KPIs are not universal product requirements. USWDS examples are guidance-only and do not approve a charting library. WCAG conformance requires review of the complete interface and content with representative users and assistive technologies.
