# Web Platform Compatibility Evidence

Verified 2026-10-21. Recheck feature status when making a project decision.

## Baseline

- [Web Platform Baseline](https://web.dev/baseline) is defined by the W3C WebDX Community Group. It labels a feature **newly available** after support reaches the core browser set and **widely available** after 30 months.
- [MDN's Baseline definition](https://developer.mozilla.org/en-US/docs/Glossary/Baseline/Compatibility) covers desktop and mobile Chrome, Edge, Firefox, and Safari. MDN explicitly notes that Baseline does not replace testing for older releases, browsers outside that set, operating-system webviews, assistive technology, accessibility, usability, performance, or security.
- [web-features](https://github.com/web-platform-dx/web-features) is the canonical data project behind Baseline. It is an external code and data package; using it in tooling requires version-specific R2 review.

## Normative and Test Sources

- The [WHATWG HTML Living Standard](https://html.spec.whatwg.org/) defines HTML and related browser behavior. Use focused sections of the standard for normative claims rather than copying the full document into context.
- [ECMAScript](https://tc39.es/ecma262/) is the normative JavaScript language specification.
- [web-platform-tests](https://github.com/web-platform-tests/wpt) provides cross-browser specification tests. Its results can reveal interoperability but do not prove an application's critical journeys work.
- [MDN browser-compat-data](https://github.com/mdn/browser-compat-data) supplies structured compatibility evidence used by MDN. Treat individual claims as evidence to verify against project targets, not as a blanket guarantee.

## Decision Rule

Baseline Widely available is a useful default for broad public experiences. A project may use a newer feature only when target environments and fallback behavior make the risk acceptable. A project may need older support when its real users, contractual obligations, accessibility needs, or embedded environments require it.
