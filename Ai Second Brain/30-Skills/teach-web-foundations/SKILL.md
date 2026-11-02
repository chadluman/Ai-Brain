---
name: teach-web-foundations
description: Teach browser, HTML, CSS, JavaScript, TypeScript, HTTP, and web toolchain foundations through runnable exercises. Use for foundational web instruction or for repairing gaps that block more advanced frontend or full-stack work.
---

# Teach Web Foundations

## Outcome

Build an accurate browser-and-network mental model so the learner can explain, implement, inspect, and debug a small web page without treating a framework as the platform.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

Read only what the lesson needs:

- [Teach COITB HTML and CSS](../teach-coitb-html-css/SKILL.md) for certification-focused HTML/CSS diagnostics, weighted objectives, curriculum, capstone, and original practice assessments.
- [TypeScript Project Foundation](../typescript-project-foundation/SKILL.md) for static typing, configuration, runtime-validation boundaries, or JavaScript migration.
- [Build and Package Toolchain](../build-package-toolchain/SKILL.md) for runtimes, package managers, lockfiles, scripts, builds, and caches.
- [Web Platform Compatibility](../web-platform-compatibility/SKILL.md) for browser targets, feature support, fallbacks, and compatibility testing.
- [Web Accessibility Review](../web-accessibility-review/SKILL.md) for semantic structure, keyboard and assistive-technology behavior, and accessible verification.
- [Web Form Design](../web-form-design/SKILL.md) when inputs, validation, submission, errors, or recovery are central.

For current platform behavior, use current web standards and authoritative browser documentation; do not rely on remembered compatibility claims.

## Teaching Priorities

Teach the platform in dependency order: document semantics and accessibility; cascade, layout, and responsive behavior; JavaScript values, control flow, functions, modules, and asynchronous work; DOM events and rendering; HTTP requests and responses; browser storage and security boundaries; then TypeScript and build tooling when they solve a demonstrated problem.

Require the learner to use browser developer tools to inspect the DOM, styles, network traffic, runtime errors, and accessibility information. Make debugging part of the lesson rather than a rescue step.

Prefer exercises that render or exchange real data locally. Useful checks include valid document structure, keyboard operation, responsive behavior, event order, network requests, error states, and testable pure logic.

## Boundaries

- Do not teach framework conventions as browser guarantees.
- Do not introduce a bundler, package, type system, or CSS abstraction before its benefit is observable in the exercise.
- Treat storage, cookies, cross-origin behavior, DOM injection, and untrusted input as security boundaries even in beginner material.
- Label compatibility, performance, and accessibility statements as verified or unverified for the chosen browsers and devices.

## Completion

The learner can explain the relevant browser or HTTP mechanism, build the focused artifact, diagnose at least one failure with development tools, verify the named behavior, and state which production concerns remain outside the exercise.
