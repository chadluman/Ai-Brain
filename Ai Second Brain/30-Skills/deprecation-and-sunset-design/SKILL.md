---
name: deprecation-and-sunset-design
description: Design API deprecation and product sunsetting with two published dates, standard deprecation and sunset headers, a 410 Gone successor response, and a responsible shutdown sequence with a working export. Use when retiring an API, a feature, or a product.
---

# Deprecation and Sunset Design

## Outcome

Produce a retirement plan that treats the people who depend on the thing being retired as the first priority: two published dates, a migration path, a working export where user data is involved, and a shutdown sequence that does what it promised — including deleting data when it said it would.

Use [API Contract Design](../api-contract-design/SKILL.md) for the contract and compatibility policy being retired, [User Data Export Design](../user-data-export-design/SKILL.md) for the export itself, and [Dependency Upgrade Operations](../dependency-upgrade-operations/Dependency%20Upgrade%20Operations.md) for tracking the lifecycle dates that force retirements.

## Snapshot and re-check

Research for this skill was checked 2026-11-09. Treat deprecation practice as durable, but re-check version numbers, platform notice periods, and policy dates before citing them — they are a 2026-11-09 snapshot and may have moved on. Provider notice calendars in particular change: verify each provider's current period against its own documentation rather than copying a figure from this skill.

## Deprecating an API: two dates

Retiring an endpoint takes two dates, and they must not be confused:

- **Deprecation date** — stop recommending the endpoint. Its behaviour does not change; it keeps answering exactly as before. This is the date clients should start migrating away.
- **Sunset date** — the endpoint stops answering. The sunset date must not precede the deprecation date.

Publish both dates in the documentation and send both on every response from the deprecated endpoint: the `Deprecation` header (RFC 9745) and the `Sunset` header (RFC 8594). A deprecation that lives only in a changelog nobody reads is not a deprecation; the headers put the notice where the client actually looks.

Published notice periods vary widely by provider. As a snapshot from research checked 2026-11-09: one large API provider gives roughly 24 months after a newer version ships, another commits to at least 24 months before retiring, another gives each stable version at least 12 months with at least 9 months of overlap, and one model provider gives at least 60 days. These are illustrations of the range, not promises — verify the current period for each provider you depend on. Security issues are the usual exception to notice periods: a vulnerable endpoint can be shut down faster, and clients should expect that.

A reasonable calendar for a small API is 12 months: announce with a migration guide and a dual-run period where old and new both work, warn in responses via the headers, then retire. On sunset, return `410 Gone` with a problem document naming the successor. Do not silently redirect to a differently-shaped payload — a redirect that changes the shape is a breaking change wearing a polite status code.

## Sunsetting a product responsibly

A fair shutdown has a fixed shape. A good default is 90 days' notice for a paid product people depend on, and around 30 days for a free side project. The sequence:

1. **Decide and prepare 1–2 weeks before announcing.** Build the export first, confirm the billing and refund mechanics, and write the alternatives list. Announcing before the export works is announcing a promise you cannot yet keep.
2. **Announce with a fixed date**, a one-sentence reason, alternatives, and a working export. Stop new signups the same day.
3. **Stop billing and refund prepaid time** beyond the end date. Charging people for a product you have announced you are closing is the fastest way to lose whatever trust remains.
4. **Final warning at 14 days** before the end date.
5. **Read-only for the last 1–2 weeks**, with export still working. Users can get their data out; they cannot create new work they will then lose.
6. **Delete data as promised**, commonly around 30 days after close, and confirm the deletion. A deletion promise that is never carried out is a lie told to people who trusted the shutdown notice.

**Export is non-negotiable.** Build it before announcing, in a format people can open (CSV or JSON), including everything the user created. Pointing people at an API does not count as an export — the API goes away with the product. In the EU, data-portability rules give users a right to their data in a structured, commonly used, machine-readable format; get legal advice rather than self-certifying from a checklist.

API and integration consumers deserve the longest notice of anyone, because their product breaks when yours does. Give them the full calendar, the migration guide, and a direct contact — they cannot fix a breaking change they were not told about.

## Failure modes

- One date instead of two: an endpoint disappears with no deprecation period, or a deprecation is announced and never followed through, so clients stop trusting the next one.
- A sunset that silently redirects to a differently-shaped successor.
- Announcing a shutdown before the export works, then shipping the export late or incomplete.
- Billing continuing past the announced end date, or prepaid time never refunded.
- Data kept after the promised deletion date with no explanation.

## Supporting skills

- [API Contract Design](../api-contract-design/SKILL.md) — the contract and compatibility policy being retired.
- [User Data Export Design](../user-data-export-design/SKILL.md) — building the export the shutdown depends on.
- [Dependency Upgrade Operations](../dependency-upgrade-operations/Dependency%20Upgrade%20Operations.md) — tracking runtime and dependency end-of-life dates that force retirements.
- [Data Retention and Deletion Operations](../data-retention-deletion-operations/Data%20Retention%20and%20Deletion%20Operations.md) — retention, holds, and deletion evidence for the shutdown tail.
- [Privacy and Data Governance](../privacy-data-governance/Privacy%20and%20Data%20Governance.md) — data-subject rights and portability obligations.

## State

Risk: R0 (draft).
Draft pending representative validation.
