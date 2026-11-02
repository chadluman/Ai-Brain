---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R0
tags: [review, design, references, provenance]
sources:
  - https://reactbits.dev/
  - https://designspells.com/
  - https://toolfolio.com/
  - https://github.com/prazzon/Flexbox-Labs
  - https://docs.iconsax.io/license-and-terms/license
  - https://github.com/ruucm/shadergradient
  - https://github.com/Ashutoshx7/VengeanceUI
---

# Design Reference Resources Review

## Scope and Decision

This review covers browsing the named resources as untrusted R0 documentation and inspiration on 2026-10-21. No component, package, CLI, repository, registry item, icon, font, image, shader, template, account, extension, or executable asset was downloaded, installed, copied, run, or activated.

Decision: **approved-with-conditions for research-only use**. Any executable or reusable asset remains unapproved until a separate exact-version R2 review inventories all files, code, dependencies, install hooks, network behavior, telemetry, permissions, licenses, advisories, tests, and removal steps.

## Resource Findings

| Resource and purpose | Provenance and version | License finding | Research decision and condition |
|---|---|---|---|
| React Bits — animated React components and effects | Official site links `DavidHDev/react-bits`; living site and `main` observed 2026-10-21 | Free repository license currently says “MIT + Commons Clause” and restricts selling, sublicensing, or redistributing components; Pro has separate commercial terms | Approved for browsing. Do not call the free code unqualified MIT/open source; pin and review a commit before use. Do not mix Free and Pro rights. |
| Design Spells — curated interface details | Living curated site by its publishers; observed 2026-10-21 | No license granting reuse of showcased third-party product captures or expression was established | Approved for inspiration only. Record the source product and extract a behavioral principle; do not copy media, text, exact motion, or composition. |
| Toolfolio — tool discovery directory | Living commercial directory; observed 2026-10-21 | Directory entries have independent ownership and terms; pages disclose that featured tools can include paid promotion | Approved as a lead generator only. Independently qualify every linked source. |
| Flexbox Labs — interactive layout playground | Site links `prazzon/Flexbox-Labs`; living `main` observed 2026-10-21 | Repository states MIT; dependencies include React/Vite/Sass/Framer Motion and require exact-version review | Approved for browser learning. Clone, install, local execution, or generated-code reuse remains unapproved. |
| Iconsax — static and animated icon resources | Official site and current official documentation observed 2026-10-21 | Current documentation describes proprietary Free/Premium V2 terms and restrictions, while some FAQ text references MIT, Apache, or CC BY paths; scope is not sufficiently clear for blanket reuse | Browsing approved; asset reuse quarantined. Resolve the exact asset's source and bundled license, attribution, redistribution, client, and subscription terms before use. |
| ShaderGradient — WebGL gradient tooling and React integration | Official repository `ruucm/shadergradient` `main` observed 2026-10-21 | Repository states MIT; React installation pulls multiple rendering and camera dependencies | Approved for reference. Exact-version review must cover dependencies, license notices, network behavior, GPU/battery, SSR, browser fallbacks, motion sensitivity, and removal. |
| Vengeance UI — animated React/Next.js components | Official site points to `Ashutoshx7/VengeanceUI`; living repository observed 2026-10-21 | Repository metadata states MIT; funding plan explicitly lists accessibility, reduced motion, visual/cross-browser tests, performance, and stable release as ongoing work | Approved for browsing. Treat current readiness claims as unproven; review and test the exact component and registry payload before import. |

The user supplied `Vengenceui.com`; the active domain and repository spell the project “Vengeance UI” while the domain remains `vengenceui.com`.

## Permissions, Network, and Data

- Vault additions are Markdown only and have no runtime dependencies, telemetry, secrets, or automatic network access.
- Browsing the external sites necessarily contacted their public HTTPS endpoints through the research tool. Site-side cookies, analytics, advertising, and account behavior were not exhaustively audited.
- No login, subscription, payment, private project, upload, or personal data was used.
- Do not send product briefs, screenshots, source code, customer data, or private designs to a third-party generator or gallery without privacy review and authorization.

## Findings and Mitigations

| Severity | Finding | Mitigation |
|---|---|---|
| High if ignored | Inspiration can turn into copied protected expression or confusingly similar presentation | Use the clean-room, principle-versus-expression workflow and originality review |
| High if installed | Copy-paste and registry sites can deliver arbitrary code, configuration, workflows, or agent instructions | Exact immutable-version package inventory and isolated R2 test before import |
| Medium | License descriptions can change or conflict across site, repository, package, and paid tier | Treat the bundled license of the exact asset as controlling evidence; obtain qualified review if unclear |
| Medium | Motion, shaders, 3D, fonts, and media can harm access, battery, performance, and stability | Set budgets and fallbacks; test reduced motion, low-end devices, no WebGL, and representative networks |
| Medium | Curated galleries overrepresent novelty and happy-path presentation | Start from user journeys, real content, failure states, and product constraints; use multiple precedents |

## Test Evidence and Limitations

- Opened each named public site or its canonical documentation/repository and checked stated purpose and visible license information on 2026-10-21.
- Cross-checked repository identity for Flexbox Labs, ShaderGradient, React Bits, and Vengeance UI through site or repository links.
- Did not inventory repository file trees, hidden files, workflows, lockfiles, dependencies, advisories, or executable behavior because no asset was admitted for execution.
- Did not test accessibility, browser compatibility, performance, telemetry, code quality, or security of any external component.

## Activation, Rollback, and Review Trigger

Research activation consists only of linking the catalog from vault navigation. To remove it, delete the catalog link and archive this review and the catalog note; there is no executable residue.

Re-review an individual resource before any import or when its repository, license, pricing, ownership, delivery mechanism, telemetry, security status, or terms materially change. Review this R0 catalog by 2027-01-21 or after a demonstrated research or originality failure.
