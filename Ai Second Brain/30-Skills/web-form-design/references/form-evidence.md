# Web Form Evidence

Verified 2026-10-21.

- The [WHATWG forms standard](https://html.spec.whatwg.org/multipage/forms.html) defines native forms, labels, controls, submission, client validation, autofill, input modes, and server communication. It notes that many forms need no client scripting and that scripts can progressively augment behavior.
- The [W3C WAI Forms Tutorial](https://www.w3.org/WAI/tutorials/forms/) covers labels, groups, instructions, validation, notifications, multi-page flows, custom controls, and time limits. It recommends short forms that request only what the process requires.
- [MDN client-side form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation) explains the user-experience benefit of immediate feedback and explicitly warns that client checks are easy to bypass and are not an exhaustive security measure.
- The [OWASP Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html) routes server-side parsing, allowlist validation, structured and Unicode data, rich content, files, and common pitfalls.
- The [OWASP CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) documents framework protections, token patterns, Fetch Metadata, origin checks, SameSite limits, and interaction defenses. Select controls from the actual authentication and request model; do not copy one pattern universally.

## Review Questions

- Can the user understand and complete the form without placeholder-only instructions, pointer-only input, or client JavaScript?
- Does the server parse, normalize where appropriate, validate, authorize, and constrain every submitted value before side effects?
- Can retries, double clicks, reordered requests, expired sessions, or network recovery create duplicate or contradictory state?
- Are errors announced, associated, specific, non-destructive, and safe to display?
- Are sensitive values excluded from URLs, logs, analytics, crash reports, and unnecessary storage?
