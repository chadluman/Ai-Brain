---
status: reviewed
owner: vault-owner
created: 2026-10-31
last_verified: 2026-10-31
review_by: 2026-11-30
risk: R0
tags: [catalog, security-review, skills, bootstrap, frontend, prerelease]
sources:
  - https://github.com/twbs/bootstrap/tree/c2ab624f40c4dcfdbcae9747dce265834ffb4f5d/skills
  - https://github.com/twbs/bootstrap/commit/c2ab624f40c4dcfdbcae9747dce265834ffb4f5d
  - https://github.com/twbs/bootstrap/blob/c2ab624f40c4dcfdbcae9747dce265834ffb4f5d/LICENSE
  - https://getbootstrap.com/docs/6.0/getting-started/install/
  - https://getbootstrap.com/docs/6.0/guides/migration/
  - https://registry.npmjs.org/bootstrap/6.0.0-alpha.1
---

# Security Review — Bootstrap Skills

## Identity and Decision

- Name and purpose: Bootstrap's official agent skills for installing, bundling, customizing, extending, and migrating Bootstrap 6
- Source and organization: `twbs/bootstrap`, maintained by the Bootstrap Authors
- Immutable source: commit `c2ab624f40c4dcfdbcae9747dce265834ffb4f5d`, acquired 2026-10-31 from the user-provided `main/skills` reference
- Upstream package: 11 directories containing one Markdown `SKILL.md` each; the complete Git tree response was not truncated
- Assigned risk: R0 for the Markdown package and local display notes; invocations inherit R2 for installation, execution, CDN use, scaffolding, builds, or project writes and R3 for production deployment, publication, credentials, real data, paid resources, destructive work, or external-system changes
- Decision: `approved-with-conditions` for documentation and discovery at this exact commit
- Conditions: use the [Bootstrap 6 Prerelease Skill Boundary](../Bootstrap%206%20Prerelease%20Skill%20Boundary.md); do not treat this review as dependency approval; recheck the exact Bootstrap release and official docs; preserve the stable/prerelease distinction; review packages, lockfiles, install hooks, and network destinations before execution
- Reviewer: Codex for vault-owner review
- Next review: 2026-11-30 or earlier on an upstream skill or Bootstrap release change, dependency or CDN change, security advisory, browser-policy change, first production v6 use, or a failed invocation

## License and Attribution

The repository root carries the MIT License, while Bootstrap's official documentation footer labels code MIT and documentation CC BY 3.0. Because these skills are documentation-like material, the local adaptations conservatively preserve both regimes: every skill links its exact source and this review, changes are identified below, and the CC BY 3.0 license is linked at <https://creativecommons.org/licenses/by/3.0/>. Attribution: “Bootstrap agent skills” by the Bootstrap Authors, adapted by the vault owner and Codex on 2026-10-31.

MIT notice preserved for the imported source:

```text
The MIT License (MIT)

Copyright (c) 2011-2026 The Bootstrap Authors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```

## Complete Upstream Inventory

| Upstream path | Bytes | SHA-256 |
|---|---:|---|
| `skills/bootstrap-color-system/SKILL.md` | 12,515 | `8FE007942C34E097D8D309EC3F94DD6B30EBFB9D80227CB74C06A75FBE2E2213` |
| `skills/bootstrap-component-js/SKILL.md` | 16,483 | `B8FA5E78543CFD12C8A697AF788F7C876EAF38DDB437AD9C61484486695BA49D` |
| `skills/bootstrap-component/SKILL.md` | 11,786 | `01F4FF66A4FCD6EE371A7BD5DDF3908223C96358BDF5871BDE08E02C1CFF2AB6` |
| `skills/bootstrap-npm/SKILL.md` | 5,195 | `338DC770F367E144093128BE544C89EBCD44CD9C99D428D92E773252C9B2FB1A` |
| `skills/bootstrap-parcel/SKILL.md` | 4,309 | `01AEE6D5BFD17C6D168F7A2C1AA10F8D492390F97041C4D2BD62447ED3778633` |
| `skills/bootstrap-utility-api/SKILL.md` | 11,716 | `06E9A115200C3FC52B79B1F4DF0E5A48EB14F847A1715EE4E2504B34C3A008A3` |
| `skills/bootstrap-v4-v6-migration/SKILL.md` | 12,018 | `19B20D6710D952DDEC1417E75410B09B15406242C808042B14300D75B1831D97` |
| `skills/bootstrap-v5-v6-migration/SKILL.md` | 30,485 | `AEFA0132912E25E3B8FA65299F7BDCFC9B3AAE530746264581B5F719455C2F97` |
| `skills/bootstrap-v6-install/SKILL.md` | 6,033 | `DB7913CB2DD543F9EF9DE23834E702A2FF1D29C0F5DE0D31ACF8CF3D47DE1C73` |
| `skills/bootstrap-vite/SKILL.md` | 4,223 | `FCB47925BAE40F56D3D1CD5CC60AFED436B2F023C93FA5FDE2ABD7445775A9B4` |
| `skills/bootstrap-webpack/SKILL.md` | 6,669 | `6E2E44918405385C5E1C0972396D47941C61E9477F4FA9A93228D8749C9F8B0F` |

No hidden files, binaries, generated assets, scripts, packages, lockfiles, install hooks, CI workflows, agent configuration, or nested archives exist under the reviewed upstream `skills/` tree.

## Complete Local Adaptation Inventory

The review note excludes itself to avoid a self-referential checksum. Each human-facing note contains only an alias and an Obsidian embed of its canonical `SKILL.md`.

| Local path | Bytes | SHA-256 |
|---|---:|---|
| `20-Catalog/Bootstrap 6 Prerelease Skill Boundary.md` | 5,637 | `CFDB56EE38241518C0F9EC6A3B56C45B3065DC3B5367D3A1845F0CD9CD194838` |
| `30-Skills/bootstrap-color-system/Bootstrap Color System.md` | 59 | `8256455FDE037AD8D1B25C4C36982F8B31A5351EADC01760F9FDA46B9A19CC5B` |
| `30-Skills/bootstrap-color-system/SKILL.md` | 13,268 | `87CC54CCCBC22B0A7CBD21D73E4CAAE9E0926B8AB96111C13FFACC0C678C9002` |
| `30-Skills/bootstrap-component-js/Bootstrap Component JavaScript.md` | 59 | `72D073A94B5954E02EDC2039E2E562A57698AEB3D9100ADA614D6AA4EBC7AB60` |
| `30-Skills/bootstrap-component-js/SKILL.md` | 17,236 | `A08668F664C07BF119D04EBAC95C94641C61E8129B473CF367D8DA262664B55D` |
| `30-Skills/bootstrap-component/Bootstrap Component.md` | 56 | `B0796E114AA8829BCEE3642C7A4DF88A165A38B26D88B04B0D317EA11642D4FA` |
| `30-Skills/bootstrap-component/SKILL.md` | 12,536 | `E4DF8E1F59A7F022BC076706A9A276AE88477330D59A4F8212B7F067817A41DC` |
| `30-Skills/bootstrap-npm/Bootstrap with npm.md` | 50 | `4748B6F781C8F00BEADCC5097506AD64F3F6F74A0CCE79FDCD8404E1F7981527` |
| `30-Skills/bootstrap-npm/SKILL.md` | 6,013 | `D946D929ECAE25CC5EDEEA94E28663D47C046ABA1ABE7F895AF4F38C57AA24FE` |
| `30-Skills/bootstrap-parcel/Bootstrap with Parcel.md` | 53 | `DC45AB889DF78F20BA2F54CDA518F7E7DBE5190B8CBCB436A92DA68F6D1FDF75` |
| `30-Skills/bootstrap-parcel/SKILL.md` | 5,130 | `8A04A3846005739B53449A8B46E05943BD0A0C992C69BF639999F1EC4741B7C0` |
| `30-Skills/bootstrap-utility-api/Bootstrap Utility API.md` | 58 | `DB6F1E17BE92DB8C58AA1DC0BFF297069FB19639B2D7D3A8E885E954C264C028` |
| `30-Skills/bootstrap-utility-api/SKILL.md` | 12,508 | `9BAE1640F8568F001CC934DE43FCD88C2760433F488E0D3872CB966FA3C974DE` |
| `30-Skills/bootstrap-v4-v6-migration/Bootstrap v4 to v6 Migration.md` | 62 | `50DFF4A5C697AED114838C821B9BC519E9518025D4DB7DD526C55AA102F960C8` |
| `30-Skills/bootstrap-v4-v6-migration/SKILL.md` | 12,774 | `B2D627E5741A6D8908A5D439E788866F30582DECB7DD2269E1E1DE2F0F2147C1` |
| `30-Skills/bootstrap-v5-v6-migration/Bootstrap v5 to v6 Migration.md` | 62 | `E85D5B9B106F32583C28C54CE2D77D81C01F9EEE5F9A0A62FCE18605EA85B856` |
| `30-Skills/bootstrap-v5-v6-migration/SKILL.md` | 31,448 | `23E4A5BD7172992307E1CC8890F9F8F876A41454DFEAC01AEB6BF423A35A2F72` |
| `30-Skills/bootstrap-v6-install/Bootstrap v6 Install.md` | 57 | `C61EF8BCED5DE2B98EF788DDF26F37F53B8880936EB1BC9F1CED2A49E5E54DBF` |
| `30-Skills/bootstrap-v6-install/SKILL.md` | 6,966 | `41291B118F3AACCDC6C6A069F4F5DB9DFFA26BE946599D4A8D0581E666F1F021` |
| `30-Skills/bootstrap-vite/Bootstrap with Vite.md` | 51 | `3BF2BEE48156ACD77B7A8866C220E4AB27E0208FC28F63D16AB20CF8D7675BED` |
| `30-Skills/bootstrap-vite/SKILL.md` | 5,042 | `BF496EA65A0908C85ABBBEDB08C5934AD56FB7B544BF3A046A549C209B45816C` |
| `30-Skills/bootstrap-webpack/Bootstrap with Webpack.md` | 54 | `BB5A196439EB90E7FC1056E1107D27134FC35E0F23EEBBCAD5A129740E7BB84A` |
| `30-Skills/bootstrap-webpack/SKILL.md` | 7,491 | `555206522C7DB0C47C147DF9ED3C6D0174136691FF87673AD50F21F424F84350` |

## Dependencies, Network, Data, and Permissions

The Markdown files have no runtime dependency, secret, telemetry, analytics, tracking, persistence, or automatic network behavior. Reading them requires only local read access.

Their examples mention executable assets that remain unapproved until a project-specific review: Bootstrap, Floating UI, Vanilla Calendar Pro, Sass, Autoprefixer, PostCSS and its CLI/loader, Vite, Webpack and loaders/plugins, Parcel and its Sass transformer, Stylelint and Bootstrap's config, Nodemon, npm-run-all, sirv-cli, Playwright, Vitest, Rolldown, Terser, and an optional CSS-extraction plugin. Migration guidance also mentions jQuery, `popper.js`, and `@popperjs/core` as legacy inputs. The upstream skills do not pin most tooling versions and do not inventory transitive dependencies or install hooks.

The published `bootstrap@6.0.0-alpha.1` registry record declares `@floating-ui/dom:^1.7.6` and `vanilla-calendar-pro:^3.4.0` as peers without `peerDependenciesMeta` marking them optional. The reviewed `main` commit had already moved Floating UI to `^1.8.0`, demonstrating release-versus-main drift. Local setup examples pin the published alpha peers and the shared boundary still requires exact package review.

Potential runtime destinations are the configured package registry, `cdn.jsdelivr.net`, and localhost development servers. Documentation links point to GitHub, getbootstrap.com, floating-ui.com, parceljs.org, and the `twbs/examples` repository. CDN usage causes end-user browsers to contact the selected CDN. No account, credential, private data, telemetry, or external transmission is required by the skill files themselves.

Minimum future permissions are target-project reads for planning and narrowly scoped writes plus child-process and package-registry network access for approved R2 work. Production publication, deployment, credentials, real data, or destructive changes are R3 and are not authorized by selecting a skill.

## Findings and Mitigations

| Severity | Finding | Mitigation | Status |
|---|---|---|---|
| High if executed blindly | The skills contain installation, build, browser-download, scaffold, and migration commands but do not review every package or install hook | Shared R2 gate requires exact-version package review, lockfile, network scope, rollback, and user-requested project scope before execution | Mitigated by condition |
| High for production selection | All 11 skills target Bootstrap `6.0.0-alpha.1`; official docs still label 6.0.x Alpha and 5.3.x latest stable | Descriptions and callouts name the snapshot; stable versus prerelease is an explicit project decision and ADR trigger | Mitigated by condition |
| Medium | Upstream `main` is mutable and package metadata already differs from the published alpha peer range | Pinned immutable commit, upstream hashes, local hashes, and re-review on any source or release change | Mitigated |
| Medium | “Optional peer” wording did not match the published package's lack of optional peer metadata | Local setup skills now state the metadata boundary and pin the published alpha peer versions pending full dependency review | Mitigated |
| Medium | POSIX shell examples use brace expansion and `touch`, which fail in PowerShell | Shared boundary requires shell-specific adaptation and resolved targets | Mitigated |
| Medium | Parcel may auto-install its Sass transformer | Shared boundary treats auto-install as an install and prefers explicit reviewed pinning | Mitigated |
| Medium | CDN examples introduce a third-party availability, privacy, CSP, and supply-chain boundary | Versioned URLs, matching SRI, `crossorigin`, CSP review, destination disclosure, and release-doc verification are required | Mitigated by condition |
| Medium | Migration renames and structural rewrites can silently break semantics, JavaScript, accessibility, or custom CSS | Inventory, staged v4-to-v5-to-v6 checkpoints, representative interaction/accessibility tests, legacy-pattern searches, and rollback are required | Mitigated by condition |
| Low | One upstream v5-to-v6 verification list had a merged bullet | Corrected locally without changing the technical meaning | Resolved |

No obfuscation, encoded payload, dynamic downloader, `eval`-style behavior, shell construction, privilege escalation, persistence, credential access, destructive command, telemetry, or instruction attempting to override the root contract was found in the upstream skill package. The repository's public security-advisories endpoint returned no published repository advisories on 2026-10-31; this does not cover future issues or the unreviewed transitive dependencies named by examples.

## Adaptation and Test Evidence

Local changes preserve the upstream procedures while removing the unsupported `guide` frontmatter, adding exact source/review routing, making the prerelease scope discoverable, correcting the merged verification bullet, and tightening peer-dependency language and versions against the published alpha registry record. No upstream command, package, build, browser, CDN asset, script, or example repository was installed, executed, imported, or activated.

- Enumerated the complete recursive Git tree at the pinned commit: 23 tree/blob entries under `skills/`, 11 Markdown blobs, `truncated: false`.
- Read every upstream file completely and calculated the source SHA-256 inventory above.
- Scanned all upstream text: 20 npm install invocations and one Playwright browser-install command; no downloader command, encoded payload, `eval`/`exec`, destructive command, or telemetry instruction.
- Inspected Bootstrap's pinned license and security policy, the current official v6 install, migration, browser, and accessibility pages, the published npm metadata, and the repository advisory endpoint.
- Inspected the bundled skill validator before execution, then ran it in explicit UTF-8 mode across all 138 skill folders: zero failures, 138 unique names, and zero duplicates.
- Parsed 434 Markdown notes and resolved 1,025 relative Markdown links, Wikilinks, and embeds: zero missing or ambiguous internal targets.
- Confirmed 517 source-registry body URL occurrences are all unique.
- Static behavioral traces confirm that a production request encounters the alpha/stable decision, an install request encounters the R2 dependency gate, a Parcel request cannot silently approve auto-install, and a v4 migration preserves the Bootstrap 5 checkpoint.

No live Bootstrap project, clean install, compilation, browser interaction, accessibility test, migration, or rollback was performed, so the skills are not evidence that Bootstrap 6 or any integration works in a specific project.

## Activation, Rollback, and Removal

- Activation: select the relevant canonical `30-Skills/bootstrap-*/SKILL.md` through the Skills Map; read the shared boundary before any command or edit.
- Safe first use: inspect a synthetic or disposable project and produce a change/dependency plan without installing or rewriting.
- Disablement: remove or mark the corresponding Skills Map entries unavailable and stop selecting the skills.
- Rollback/removal: restore the prior Skills Map, Source Registry, Maintenance Log, Vault Map, and any Research Queue entry; remove the 11 `bootstrap-*` skill folders, the shared boundary, and this review note. The imported Markdown created no other residue.
- Re-review: repeat the complete inventory and exact-version review when upstream content, Bootstrap release state, peer metadata, browser support, licensing, security guidance, or a named dependency changes.
