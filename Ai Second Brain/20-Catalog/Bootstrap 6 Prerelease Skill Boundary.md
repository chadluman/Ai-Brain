---
status: reviewed
owner: vault-owner
created: 2026-10-31
last_verified: 2026-10-31
review_by: 2026-11-30
risk: R0
tags: [bootstrap, frontend, prerelease, skills, safety]
sources:
  - https://github.com/twbs/bootstrap/tree/c2ab624f40c4dcfdbcae9747dce265834ffb4f5d/skills
  - https://getbootstrap.com/docs/6.0/getting-started/install/
  - https://getbootstrap.com/docs/6.0/guides/migration/
  - https://getbootstrap.com/docs/6.0/getting-started/browsers-devices/
  - https://getbootstrap.com/docs/6.0/getting-started/accessibility/
---

# Bootstrap 6 Prerelease Skill Boundary

This is the single local safety and execution boundary for the Bootstrap skills pinned to `twbs/bootstrap` commit `c2ab624f40c4dcfdbcae9747dce265834ffb4f5d`. The instructions describe Bootstrap `6.0.0-alpha.1`; Bootstrap's official documentation identified 6.0.x as Alpha and 5.3.x as the latest stable line when verified on 2026-10-31.

The reviewed Markdown is approved as documentation. It does not approve Bootstrap, a bundler, a compiler, a loader, an optional peer, a CDN, or any other executable dependency for a project.

## Select the Correct Lane

Before using a skill, establish the target's current Bootstrap major and exact version, product stage, supported browsers, accessibility obligations, package manager and lockfile, build system, customization depth, JavaScript components, Content Security Policy, and rollback path.

- Do not use the v6 instructions as a production default merely because they are newer. If the project requires a stable release, use current official stable-line guidance or record an evidence-backed prerelease decision in an ADR.
- Use `bootstrap-v4-v6-migration` only for a v4 starting point, and preserve its v4-to-v5 checkpoint before starting the v5-to-v6 skill.
- Use one setup lane that fits the existing project. Do not add Vite, Webpack, Parcel, or npm-only scaffolding when the current toolchain already has an appropriate integration path.
- Treat the examples as patterns, not permission to replace existing manifests, configs, HTML, Sass, or application code.

## R2 Dependency and Execution Gate

Installation, scaffolding, package-manager operations, builds, tests, browser downloads, migration rewrites, and CDN integration are R2. Before any such action:

1. Review the exact selected versions, package contents, maintainers, license, dependencies, install scripts, advisories, supported runtimes, and required network destinations. Pin versions and preserve the lockfile; the documentation review alone is insufficient.
2. State the files and commands that will change, preserve a clean rollback point, and run in the user-requested project with least privilege and no real credentials or private data.
3. Adapt POSIX examples such as brace expansion and `touch` to the actual shell. Never paste a command whose targets or effects have not been resolved.
4. Parcel's documented transformer auto-install is still an install. Prefer a separately reviewed and pinned transformer rather than allowing an unexpected dynamic install.
5. For CDN use, copy versioned URLs and SRI hashes from the matching official release documentation, retain `crossorigin="anonymous"`, review CSP and availability implications, and disclose that browsers will contact jsDelivr. Never guess or reuse an SRI hash across versions.

Do not publish, deploy, migrate real data, create paid resources or accounts, modify a production system, or perform destructive cleanup without the immediate R3 authorization required by the root contract.

## Change and Migration Controls

- Inventory Bootstrap imports, Sass overrides, data attributes, JavaScript APIs, custom CSS, templates, component states, browser coverage, and accessibility-critical journeys before editing.
- Separate mechanical renames from structural component rewrites. Use reviewable increments and keep the last working version recoverable.
- For v4 to v6, make Bootstrap 5 build and behave correctly before beginning the v6 stage. Do not mix the two rename waves.
- Do not silently remove jQuery when the application uses it outside Bootstrap, or replace an established build system solely to follow an example.
- Stop when the target version, expected markup, dependency approval, browser policy, or rollback path is unresolved and the answer would materially change the work.

## Completion Evidence

Report the exact Bootstrap and tooling versions selected, changed files, dependency-review decision, network destinations, commands run, and rollback path. In proportion to the change, verify:

- a clean install and reproducible build from the lockfile
- expected generated CSS and JavaScript without unintended global or bundle changes
- representative interactive components, keyboard use, visible focus, reduced motion, zoom, RTL, color modes, validation, and assistive-technology behavior
- the project's supported browsers and CSP
- migration searches for legacy patterns plus targeted regression tests
- accessibility, performance, and security outcomes separately from mere compilation success

If a required check was not run, label it pending rather than calling the integration or migration complete.

## Rollback and Re-Review

Rollback means restoring the reviewed manifest, lockfile, source, and configuration state from version control or a verified backup, then rebuilding and retesting. Do not use broad recursive deletion as a convenience. Re-review on any Bootstrap release change, upstream skill change, new dependency or CDN, security advisory, browser-floor change, failed migration, or first production use of the v6 prerelease line.
