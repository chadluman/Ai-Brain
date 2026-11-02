# Information Architecture Evidence

Verified: 2026-10-21

## Standards and Public Guidance

- [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110.html) defines resource identification, safe and idempotent methods, `Location`, and redirect semantics, including special care when redirecting unsafe methods.
- [WHATWG URL Standard](https://url.spec.whatwg.org/) defines interoperable URL parsing, serialization, origins, hosts, paths, queries, and fragments. It does not choose a product's route vocabulary.
- [W3C WAI: Navigating and finding](https://www.w3.org/WAI/people-use-web/tools-techniques/navigation/) describes varied navigation strategies and the value of consistent labels, descriptive headings, multiple mechanisms, skip links, and orientation cues.
- [W3C WAI Page Structure Tutorial](https://www.w3.org/WAI/tutorials/page-structure/) connects semantic regions and headings to screen-reader, keyboard, cognitive, low-vision, mobile, and search use.
- [GOV.UK: Writing for user interfaces](https://www.gov.uk/service-manual/design/writing-for-user-interfaces) recommends clear, readable URLs and warns against exposing personal information through URLs and page metadata.

## Decision Boundaries

- URL syntax standards establish interoperability, not a good taxonomy. Validate names and grouping with domain users.
- A permanent redirect can be cached and indexed for a long time. Prove the mapping and downstream behavior before broad release.
- Single-page routing must preserve document semantics, focus, titles, history, and direct loading; visual screen replacement alone is insufficient.
- Localization strategy changes URL identity, caching, analytics, sharing, and indexing. Choose it with the internationalization and discoverability skills.
