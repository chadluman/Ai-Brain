# Software Quality Evidence

Verified 2026-10-21.

## Academic Foundation

MIT EECS [6.102 Software Construction, Spring 2026](https://web.mit.edu/6.102/www/sp26/) organizes software quality around being safe from bugs, easy to understand, and ready for change. Its curriculum covers static checking, testing, code review, specifications, abstraction, concurrency, and networking.

- [Testing](https://web.mit.edu/6.102/www/sp26/classes/02-testing/) covers test-first work, input-space partitioning, black-box and glass-box testing, unit and integration tests, regression testing, and coverage as part of validation.
- [Code Reviewing](https://web.mit.edu/6.102/www/sp26/general/code-review.html) describes review as complementary to static checking, testing, assertions, and reasoning, and emphasizes defects, specification mismatch, test partitions, clarity, safety, and maintenance.
- [Designing Specifications](https://web.mit.edu/6.102/www/sp26/classes/05-designing-specs/) explains how coherent declarative contracts support correctness, understanding, and implementation change.

Use these as durable engineering principles. Course exercises and workflows are educational examples, not mandatory production process.

## Web Interoperability Evidence

The canonical [web-platform-tests repository](https://github.com/web-platform-tests/wpt) is a cross-browser test suite for web-platform specifications and publishes results through [wpt.fyi](https://wpt.fyi/). Use its tests and results as interoperability evidence when a decision depends on browser behavior.

Do not assume a passing browser-engine test proves an application's user journey, accessibility, performance, or security. Do not clone or execute the repository until its exact revision and setup pass R2 review.

