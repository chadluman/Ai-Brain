# File and Media Evidence

Verified: 2026-10-21

## Primary Sources

- [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html) recommends defense in depth: allow-list necessary extensions, distrust the client media type, generate filenames, constrain size, authorize uploaders, isolate storage, and consider scanning or content reconstruction. Scanners and rewriters remain parsers of hostile input and need isolation and resource bounds.
- [OWASP SSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html) treats application-controlled remote fetching as a route to internal services and non-HTTP schemes. Apply it to URL imports, link previews, avatar fetches, and media proxying.
- [WHATWG MIME Sniffing](https://mimesniff.spec.whatwg.org/) defines browser media-type interpretation. It explains delivery behavior; it does not establish that uploaded content is safe.

## Decision Boundaries

- A file extension, `Content-Type` value, magic-byte match, antivirus result, or successful decode is one signal, not proof of harmlessness.
- Sending private content to a public reputation or scanning service is a disclosure. Use an approved private service or isolated local scanner when data policy forbids that transfer.
- Public object URLs simplify delivery but weaken revocation and authorization. Prefer application-mediated access or short-lived capability URLs for protected content.
- Object storage durability does not prove backup, deletion, or recovery. Test lifecycle behavior, versioning, replication, restore, and provider export separately.
- Active formats such as HTML, SVG, office documents, and PDFs require content-specific handling. Forced download, sandboxed rendering, or format conversion can reduce risk but does not eliminate it.
