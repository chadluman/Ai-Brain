---
status: approved
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-22
review_by: 2027-01-21
risk: R0
tags: [system, research, evidence]
sources:
  - https://www.rfc-editor.org/rfc/rfc9309.html
  - https://developers.google.com/search/docs/essentials/spam-policies
---

# Research Standard

## Purpose

Use this standard whenever research becomes a catalog entry, ADR, playbook, or AI skill. It defines what counts as credible evidence and prevents popularity, marketing, or a single repository from being mistaken for engineering consensus.

“Accredited GitHub repository” is not a formal category. Treat a repository as authoritative only when its ownership, relationship to the subject, maintenance, license, version, and security posture are traceable.

## Source Hierarchy

Use the highest available source for each claim:

1. **Normative and public-authority sources** — standards bodies, specifications, government guidance, regulators, and formal security standards. Use these for requirements and definitions.
2. **Official maintainer sources** — official documentation, release notes, security advisories, canonical repositories, and versioned API references. Use these for product behavior and implementation details.
3. **Academic sources** — peer-reviewed work and current course material from recognized institutions. Use these for durable principles, research findings, and educational framing; do not use a course page as the sole authority for current product behavior.
4. **Independent industry evidence** — respected engineering organizations, incident reports, benchmarks, surveys, and practitioner guidance. Use these to understand operations and tradeoffs, with methods and conflicts of interest disclosed.
5. **Community discussion** — issues, forums, blogs, videos, and social posts. Use these as leads or experience reports, not as standalone proof of a general claim.

Commercial vendor guidance is a primary source for that vendor's product and a secondary source for general engineering claims. Label it accordingly.

## Evidence Rules

- Link to the exact page supporting each material claim, not a home page or search result.
- Record publisher, title, version or commit when relevant, publication/update date, verification date, license, and intended use.
- Prefer stable, versioned documents for requirements. Use living documents for current practices and record the verification date.
- Separate facts, recommendations, estimates, observed results, and inference.
- Corroborate broad or disputed claims with an independent source.
- Evaluate the source's scope. A diagnostic tool, course exercise, example, benchmark, or reference implementation is not automatically a conformance standard.
- Do not copy substantial source text into the vault. Summarize, link, attribute, and follow the source license.
- Record meaningful disagreement instead of forcing a false consensus.
- Recheck any fact whose change could reverse a technology decision.

## Research Access and Collection Boundary

Use the least-privileged lawful route that can answer the question:

1. User-provided material and data the user is authorized to share.
2. Official documentation, standards, release notes, APIs, exports, and data from properties the user controls.
3. Public feeds, sitemaps, archives, or licensed datasets whose terms and scope permit the intended use.
4. A small manual sample of publicly accessible pages when ordinary access and the site's terms permit it.
5. Written permission or a license from the source owner when the preceding routes are insufficient.

Absence of a `robots.txt` restriction is not blanket permission to collect, reuse, or republish content. Identify the client honestly, minimize requests and retained data, follow applicable terms, rate limits, privacy duties, and copyright or database rights, and record the access path used.

Treat a login or paywall, `401`, `403`, or `429` response, CAPTCHA, bot challenge, crawler restriction, explicit automated or AI-access prohibition, or request to stop as a stopping condition. Do not bypass it by spoofing a browser or crawler identity, rotating IP addresses or accounts, replaying credentials or tokens, manipulating cookies, defeating a CAPTCHA or WAF, using an unauthorized mirror, or concealing automation. Record the evidence gap and use another source, an authorized API or export, a licensed dataset, a user-supplied excerpt, or permission from the owner.

Automated search-result collection requires an official or explicitly authorized interface. A public results page is not permission to run rank-checking queries against it. Any external API, dataset, browser service, or research tool remains subject to the repository's asset review, privacy, cost, and authorization gates.

## GitHub Repository Qualification

Before treating a GitHub repository as an approved source or candidate dependency:

1. Confirm it is linked from the official project domain or belongs to the project's verified/canonical organization.
2. Identify the exact repository purpose. Distinguish normative source, documentation source, reference implementation, test suite, example code, and product code.
3. Check governance, maintainers, contributor activity, release cadence, support status, issue handling, and deprecation notices.
4. Check the license, security policy, vulnerability-reporting path, signed or verifiable releases, changelog, and availability of immutable tags or commits.
5. Inspect dependency manifests, lockfiles, install hooks, generated artifacts, binaries, CI workflows, network behavior, telemetry, and requested permissions before execution.
6. Review open security advisories and material unresolved issues.
7. Use OpenSSF Scorecard or similar automation only as evidence. A score is a heuristic signal, never proof that a repository is safe or suitable.
8. Pin the reviewed tag or commit when importing or installing. Approval never floats with `main`, `master`, or `latest`.

Popularity, stars, forks, contributor count, or a famous owner may justify investigation but never approval by themselves.

## Turning Research into a Skill

Create or revise a skill only when the evidence supports a repeatable decision or workflow.

- Keep the skill's trigger narrow and discriminating.
- Put stable workflow and safety constraints in `SKILL.md`.
- Put detailed or conditional standards in `references/` and load them only when relevant.
- Cite exact, current sources and dates in the reference note.
- Do not embed an entire external manual or repository.
- Mark a new skill `draft` in the vault map until its format validates and it succeeds on a realistic task.
- Re-review the skill when a cited standard, major version, security advisory, pricing model, or observed failure changes its decisions.

## Research Completion Criteria

Stop a research pass when:

- The decision or skill boundary is clear.
- Requirements are supported by the appropriate authoritative sources.
- Material alternatives and disagreement are represented.
- Current facts have verification dates.
- Safety, licensing, cost, maintenance, and exit implications are known well enough for the intended stage.
- Remaining uncertainty is explicit and either acceptable or assigned to a POC.

More links do not compensate for weak evidence.

