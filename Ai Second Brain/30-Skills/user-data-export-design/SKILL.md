---
name: user-data-export-design
description: Let a user obtain their own data in a structured, commonly used, machine-readable form, without leaking other people's data, so portability and exit are real and not a support ticket. Use when a product stores user-provided personal data; do not use for deletion, which is covered by Data Retention and Deletion Operations, or for a general backup, which is covered by Backup and Disaster Recovery.
---

# User Data Export Design

## Outcome

Produce a self-serve export that returns a user's own provided data in a documented, machine-readable form, through a verified, expiring delivery, so a user can leave with their data without a support ticket and without receiving anyone else's.

Use [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for the overall privacy model. Use this skill for the export mechanism itself: scope, format, delivery, and verification.

## Required Inputs

- The data inventory: every entity that holds user-provided personal data, and for each, whether it is in export scope.
- The legal and policy scope for the jurisdictions served: which data the right to portability covers, and which data it does not. This skill is design guidance, not legal advice; confirm scope with counsel for each jurisdiction.
- The identity verification method for an export request, proportionate to the sensitivity of the data.
- The format and schema: file formats, field names, timestamps, and identifiers, documented so another system can use the export without manual conversion.
- The delivery model for small and large exports, including expiry, encryption, and notification.

If there is no data inventory, build one before building the export. An export built from guesswork will miss entities, include other people's data, or both.

## Workflow

1. Scope the export to the user's own provided data. Under the portability model this skill follows, that means data the user provided, processed under consent or contract by automated means, in a structured, commonly used, machine-readable form. Derived or inferred data, other users' data, and secrets are not automatically in scope, and each exclusion should be stated in the export documentation, not hidden.
2. Verify identity before generating anything. An export is a high-value target: it bundles a user's data into one downloadable file. Require re-authentication proportionate to sensitivity, and never deliver an export to an unverified address or session.
3. Use documented, open formats. JSON and CSV cover most exports; use a stable schema with field names, types, timestamps in a stated timezone or UTC, and identifiers that remain consistent across files in the same export, so relationships between entities survive. Include a readme in the export that states what is included, what is excluded, and the export's generation date.
4. Separate other people's data at the source. Shared workspaces, messages, comments, and collaborative objects must be filtered to the requester's own contributions, or redacted, before export. A filter applied at download time, after the file is built, is too late to be the only control; filter at collection time and verify with tests.
5. Build large exports asynchronously. A request that times out in a browser is not an export feature. Use a background job, notify the user when the export is ready, deliver through an expiring, single-use or short-lived link, and delete the generated file after expiry. See [Background Job and Queue Design](../background-job-queue-design/SKILL.md).
6. Respect the response window the applicable rules set: for the portability guidance this skill follows, respond without undue delay and within one month, with an extension only for complex or numerous requests, communicated to the requester. Track requests, their status, and their delivery in an [Audit Log](../audit-log-design/SKILL.md), without logging the exported data itself.
7. Support direct transmission where technically feasible, as a separate path from download, and state honestly when it is not feasible for a given destination. Direct transmission must not become a reason to delay or block the download path.
8. Test with a synthetic account that mirrors a real user's shape: multiple entities, shared objects with other users, deleted items, and large volumes. Verify that the export contains exactly the requester's provided data, in the documented schema, and nothing else.

## Safety and Permission Boundaries

- Never include secrets, tokens, passwords, other users' personal data, or internal identifiers that would expose other accounts in an export.
- Never make export a paywalled or hindered feature for a user's own data. Charging for, delaying, or degrading an export to discourage exit is a hindrance, not a business model.
- Export delivery links must expire, must be encrypted in transit, and must not be logged in full. A permanent, public export URL is a breach, not a feature.
- A new export, storage, or delivery tool still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Sunsetting the Export

When the product itself is being retired, the export must be built and working before the shutdown is announced — users need a working exit while the service still runs, not a promise after it stops. Provide the export in CSV or JSON under the portability model this skill follows (GDPR Article 20 for data provided under consent or contract by automated means), keep the export available through the announced notice period, and stop billing before the service stops serving. See [Deprecation and Sunset Design](../deprecation-and-sunset-design/SKILL.md) for the full shutdown sequence, notice, and deletion duties.

## Outputs and Evidence

- A data inventory with export scope per entity, and stated exclusions.
- An export schema and readme, with formats, field definitions, and timestamps.
- An identity-verification, asynchronous-generation, expiring-delivery, and audit design.
- Tests or a test report covering a synthetic account with shared objects, deleted items, and large volumes, verifying exactly the requester's data is included.
