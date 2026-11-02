# Browser State Evidence

Verified 2026-10-21.

- The [WHATWG URL Standard](https://url.spec.whatwg.org/) defines URL parsing, serialization, origins, and `URLSearchParams`. URLs are interoperable application state only when their security, length, encoding, and product semantics are appropriate.
- [MDN History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API) documents session-history navigation and state manipulation. Use the underlying HTML specification for normative behavior and test back, forward, reload, and restoration in supported browsers.
- The [WHATWG Storage Standard](https://storage.spec.whatwg.org/) defines origin storage, persistence, estimates, quota, and pressure. It notes that non-persistent data may be lost under device storage pressure.
- [IndexedDB 3.0](https://www.w3.org/TR/IndexedDB-3/) defines records, indexes, transactions, upgrades, privacy, and security considerations. Its 2025 publication was a Working Draft, so verify compatibility and actual implementation behavior.

## Placement Test

Before adding a store, ask:

- Is this already authoritative on the server or derivable from another value?
- Must it survive component disposal, route navigation, reload, browser restart, logout, or device change?
- Should a copied URL reproduce it, and is it safe to expose in history, logs, referrers, screenshots, and analytics?
- What invalidates it, migrates it, clears it, and resolves concurrent changes?
- What does the user see when it is missing, stale, rejected, conflicted, or corrupted?

Use the narrowest lifetime and ownership boundary that satisfies those answers.
