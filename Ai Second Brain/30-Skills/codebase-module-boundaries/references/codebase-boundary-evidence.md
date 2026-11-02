# Codebase Boundary Evidence

Verified: 2026-10-22

## Current and Durable Sources

- [CMU SEI Maintainability](https://sei.cmu.edu/library/maintainability/) provides a scenario-based method for assessing whether architectural decisions satisfy maintainability requirements. It treats maintainability as a quality attribute with concrete stimuli and responses rather than a style label.
- [CMU SEI ATAM collection](https://www.sei.cmu.edu/library/architecture-tradeoff-analysis-method-collection/) evaluates architecture against prioritized quality-attribute scenarios and exposes risks, sensitivity points, and tradeoffs. A full ATAM is heavyweight; smaller projects can still use its scenario and tradeoff discipline.
- [MIT 6.102 Abstract Data Types](https://web.mit.edu/6.102/www/sp26/classes/06-abstract-data-types/) explains abstraction, modularity, encapsulation, information hiding, separation of concerns, and representation independence. Its key boundary test is whether clients depend only on specified operations rather than internal representation.
- [MIT 6.102 Designing Specifications](https://web.mit.edu/6.102/www/sp26/classes/05-designing-specs/) distinguishes stronger and weaker contracts and the freedom they leave implementers. Module contracts should state behavior precisely without exposing unnecessary implementation choices.
- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) defines a product-quality model that includes maintainability characteristics. The public scope is useful for vocabulary; clause-level conformity requires access to and interpretation of the licensed standard.

## Decision Implications

- Start with scenarios such as adding a payment method, changing a datastore, enforcing a new tenant rule, or replacing a provider. “Use clean architecture” is not a measurable requirement.
- A useful module owns coherent behavior and hides a volatile decision. A folder, package, class, service, or layer is not a boundary if callers still reach through it.
- Independence is multidimensional: change, test, data, runtime, deployment, scaling, security, and team ownership can point to different boundaries. Do not assume they must coincide.
- Public contracts should be simple, coherent, adequate, and representation-independent. Generic shared modules often create the opposite result by coupling unrelated domains.
- Architecture evaluation identifies risk; only representative change, failure, performance, and security tests demonstrate the chosen boundary in this system.
