# Discoverability Evidence

Verified 2026-10-22. Search interfaces, policies, ranking systems, APIs, and result features change; recheck the exact provider and market before a material decision.

## Ranking and Content

- [Google's ranking systems guide](https://developers.google.com/search/docs/appearance/ranking-systems-guide) describes multiple page-level systems plus site-wide signals. It supports planning around relevance, usefulness, originality, and reliability, not a deterministic factor checklist or guaranteed position.
- [Creating helpful, reliable, people-first content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) asks whether a page contributes original information, research, analysis, experience, or substantial value. Its E-E-A-T discussion is explanatory guidance; E-E-A-T is not itself one numeric ranking factor.
- [Google Search spam policies](https://developers.google.com/search/docs/essentials/spam-policies) prohibit practices including link spam, keyword stuffing, doorway abuse, scaled low-value content, abusive scraping, and unauthorized machine-generated Search queries. Apply these as Google-specific eligibility and enforcement evidence, not universal law.
- [Google SEO Starter Guide](https://developers.google.com/search/docs/fundamentals/seo-starter-guide) frames SEO as helping search systems understand content and users find it. Exact-match repetition is not a substitute for useful coverage.

## Research and Measurement

- The [Search Console API overview](https://developers.google.com/webmaster-tools/about) provides authorized programmatic access to Search data for properties the caller is permitted to access. Account connection and production-data transfer remain R3 actions.
- [Search Console performance tasks](https://support.google.com/webmasters/answer/17010961?hl=en) explain query and page analysis and recommend focusing more on impression and click trends than average position alone. They also note that outside events and competitor changes can confound before-and-after conclusions.
- The [Bing Webmaster API](https://learn.microsoft.com/en-us/bingwebmaster/) provides registered-site rank, traffic, keyword, link, and crawl data through provider interfaces. Microsoft lists 2026-08-31 as the retirement date for legacy SOAP and POX APIs; treat them as retired and verify the current supported REST interface and terms before implementation.
- Follow the vault [Research Standard](../../../00-System/Research%20Standard.md) for collection. Search-result pages, publicly visible competitor pages, missing `robots.txt` rules, cached copies, and third-party summaries do not grant permission to automate collection or republish content. Use owned data, official APIs and exports, licensed datasets, small permitted manual samples, or source-owner authorization.

## Crawl and Presentation

- [Robots Exclusion Protocol, RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html) standardizes `robots.txt` parsing, matching, errors, and caching. It requires matching crawlers to follow applicable rules and explicitly states that the protocol is not access authorization.
- [Google Search: How Search Works](https://developers.google.com/search/docs/fundamentals/how-search-works) describes Google's crawl, render, index, and serving stages and states that indexing is not guaranteed.
- [Google crawling and indexing](https://developers.google.com/search/docs/crawling-indexing) documents Google-specific sitemaps, canonicalization, robots meta directives, JavaScript, status handling, and site moves.
- Use the [WHATWG HTML Living Standard](https://html.spec.whatwg.org/) for normative HTML semantics and metadata behavior. Search-provider interpretation is a separate, changing layer.

## Evidence Boundary

Provider documentation is primary evidence for that provider, not a universal web standard. Record the provider, locale, device, date, personalization state, data ownership, access route, and sampling limits for ranking research. Distinguish observed Search Console trends from external rank estimates and manual result samples. Validate production-equivalent output, status, headers, canonical and alternate links, structured data, internal navigation, and privacy behavior with no privileged session.
