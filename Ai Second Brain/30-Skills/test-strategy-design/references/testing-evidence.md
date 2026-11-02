# Testing Evidence

Verified: 2026-10-21

## Durable Guidance

- [MIT 6.102 Testing](https://web.mit.edu/6.102/www/sp26/classes/02-testing/) teaches specification partitions, test-first reasoning, regression tests, and test-suite quality in a current university software-construction course.
- [Google Testing Blog: How Much Testing Is Enough?](https://testing.googleblog.com/2021/06/how-much-testing-is-enough.html) recommends a base of unit tests, strong integration coverage, and end-to-end checks for critical user journeys. It is industry guidance, not a universal ratio.
- [web-platform-tests](https://github.com/web-platform-tests/wpt) is the canonical cross-browser specification test suite and useful interoperability evidence. Running its repository is R2 and requires review.
- [W3C Evaluating Web Accessibility](https://www.w3.org/WAI/test-evaluate/) states that evaluation should begin early and that no automated tool alone can establish accessibility; knowledgeable human evaluation remains necessary.
- [OWASP Web Security Testing Guide v4.2](https://owasp.org/www-project-web-security-testing-guide/v42/) is the current stable versioned web-security testing guide at verification; version 5 content was still under development.

## Tool Example

- [Playwright test isolation](https://playwright.dev/docs/browser-contexts) documents clean browser contexts and independent tests. Tool installation, browsers, and dependencies require exact-version R2 review.

## Interpretation Boundaries

- Test pyramids are cost and feedback heuristics, not quotas. Architecture and failure risk determine the useful distribution.
- Mocks verify assumptions about a substitute. Contract and integration evidence are still needed against real boundaries.
- Code coverage shows execution, not assertion quality, missing requirements, or absence of defects.
