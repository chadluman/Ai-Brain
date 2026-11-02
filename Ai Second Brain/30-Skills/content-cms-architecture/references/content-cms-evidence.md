# Content and CMS Evidence

Verified: 2026-10-21

## Standards and Public Guidance

- [W3C Authoring Tool Accessibility Guidelines overview](https://www.w3.org/WAI/standards-guidelines/atag/) explains two distinct requirements: the authoring interface is accessible, and the tool enables, supports, and promotes accessible output. It explicitly covers CMSs, editors, site builders, forums, and other authoring systems.
- [ATAG 2.0](https://www.w3.org/TR/ATAG20/) is a W3C Recommendation. It predates WCAG 2.2, so use the current WCAG version when testing generated content while retaining ATAG's authoring-tool principles.
- [GOV.UK: Getting the scope of your transaction right](https://www.gov.uk/service-manual/design/scoping-your-service) distinguishes task-critical guidance from separately discoverable content and centers the wider user journey.
- [GOV.UK: Making your service accessible](https://www.gov.uk/service-manual/helping-people-to-use-your-service/making-your-service-accessible-an-introduction) makes accessibility a whole-team concern and includes disabled people in discovery and testing.

## Decision Boundaries

- A CMS feature list does not prove editor usability, API stability, accessible output, localization quality, total cost, or export fidelity. Test representative content and roles.
- Headless delivery improves channel separation but moves preview, composition, validation, accessibility, caching, and failure handling into the product team.
- Visual page builders maximize local layout choice while often weakening structure, consistency, portability, and accessible output. Use bounded components and validation when selected.
- Content migrations fail through semantics and relationships as often as through bytes. Preserve stable identifiers, redirects, ownership, provenance, publication state, language, and history where required.
