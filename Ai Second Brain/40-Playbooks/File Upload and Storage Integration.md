---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, backend, storage, uploads, media, security]
sources: []
---

# File Upload and Storage Integration

## Scope and Fit

This playbook covers two complementary choices for files in a Next.js and Vercel app: UploadThing for direct, type-safe browser uploads with auth, and Cloudflare R2 for S3-compatible object storage with zero egress for public assets. It also covers when to use Cloudinary instead for transforms and video.

Use UploadThing when the app needs user uploads (avatars, clips, overlays) without proxying through Vercel functions, which have size and time limits. Use R2 when the app needs public assets, clips, or overlays served at scale without egress bills. Use Cloudinary only when image and video transforms, transcoding, or adaptive streaming are the actual need.

Do not proxy uploads through Server Actions, and do not use R2 as a transform service or Cloudinary as a plain file store.

## Trust Boundary

```text
browser -> UploadThing (File Router, auth middleware) -> storage -> onUploadComplete -> Neon metadata
browser -> R2 (presigned URL, scoped) -> public asset via custom domain
untrusted client -> application authentication + authorization -> server only
```

Upload authorization happens in the File Router's middleware, not in the browser. A public R2 asset is public: anything served from a public custom domain must be safe to share with anyone who has the link.

## Prerequisites and Approval Boundaries

- Apply the vault's file-media-ingestion skill for media handling, and its privacy-data-governance skill for what may be uploaded and retained.
- Accept an ADR covering the upload choice per file type (user uploads versus public assets versus transformed media), retention and deletion policy, and cost (see below).
- Security-review the exact File Router rules, presigned-URL scope and expiry, and deletion flow before use.
- Enabling production uploads, changing file-type or size limits, and changing public-asset policy are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `UPLOADTHING_TOKEN` / `UPLOADTHING_SECRET` | Server secret | UploadThing authentication |
| `UPLOADTHING_APP_ID` | Server config | UploadThing application identification |
| `R2_ACCOUNT_ID` | Server config | R2 account endpoint |
| `R2_ACCESS_KEY_ID` / `R2_SECRET_ACCESS_KEY` | Server secret | R2 S3-compatible authentication |
| `R2_BUCKET` | Server config | R2 bucket for public assets |
| `R2_PUBLIC_DOMAIN` | Public config | Custom domain serving public assets |

For UploadThing: define a File Router with type, size, and count limits plus auth middleware (for example Clerk), an API route, an upload button or dropzone, and an `onUploadComplete` handler that saves metadata to Neon. For R2: use the S3-compatible SDK with the account endpoint, presigned URLs for uploads, a Workers binding where applicable, and a public custom domain for delivery.

## Integration Rules

- Authorize every upload server-side, in middleware, before any bytes are stored. A client-side file-type check is a user-experience feature, not a security control.
- Validate type, size, and count in the File Router or presigned-URL policy, and re-validate on completion. Do not trust the browser's file extension.
- Delete from the storage provider when the app record is deleted. An orphaned file in UploadThing or R2 is a retention and privacy leak.
- Serve public assets from R2's custom domain, not through the app, so delivery does not consume Vercel function invocations or egress.
- Use Cloudinary only for transforms: upload, transformation URL parameters, SDK, and eager variants, with a paid plan and a cache strategy before production video. The free plan has no paid overage path in secondary accounts — an account suspends when credits run out — so do not use Cloudinary as the sole origin for high-traffic video on free.
- Do not assume every S3 feature works on R2. Object Lock, Intelligent-Tiering, and replication gaps are reported in secondary accounts; check the feature the app actually needs.
- Watch operations billing on R2: operations are billed, so chatty small-file workloads can dominate cost even with zero egress.

## Cost Shape

UploadThing: Secondary, not vendor-verified in the research run — Free 2GB; $10 per month for 100GB, $25 per month for 250GB, $0.08 per GB over. Check uploadthing.com/pricing. R2: Secondary, corroborated — $0.015 per GB-month Standard, $0.01 infrequent access, Class A $4.50 per million, Class B $0.36 per million, free 10GB and 1M Class A and 10M Class B operations, zero egress. Check Cloudflare R2 pricing. Cloudinary: Verified (vendor pricing page) — Free 25 credits per month; Plus $99 per month ($89 annual) for 225 credits; 1 credit = 1,000 transforms, or 1GB storage, or 1GB image bandwidth (2GB video bandwidth on paid).

## Verification

Before production use, verify in an isolated project: an authorized upload succeeds and its metadata lands in Neon; an unauthorized upload is rejected; an oversized or wrong-type file is rejected server-side; deleting an app record deletes the stored file; a public R2 asset serves from the custom domain with zero app involvement; and a Cloudinary transform renders and is cached.

## Rollback and Recovery

If uploads break, disable the upload button with a clear message rather than accepting files that go nowhere. If a storage credential is exposed, rotate it, re-scope presigned URLs, and audit which files were uploaded or served under the exposed credential.
