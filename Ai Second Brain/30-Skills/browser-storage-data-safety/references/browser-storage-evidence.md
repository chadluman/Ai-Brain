# Browser Storage Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [Storage Standard](https://storage.spec.whatwg.org/) is a living standard last updated 2026-10-19. It defines origin storage buckets, quota estimates, persistence, and eviction; non-persistent storage can be cleared, and persistence requests remain subject to user-agent permission.
- [HTML Standard: Web storage](https://html.spec.whatwg.org/multipage/webstorage.html) is a living standard. It defines `sessionStorage` and `localStorage` and explicitly warns authors not to assume a locking mechanism across browsing contexts.
- [Indexed Database API 3.0](https://www.w3.org/TR/IndexedDB/) is a W3C Recommendation. It defines object stores, transactions, version changes, and durability hints; `strict` and `relaxed` durability express different performance and loss tradeoffs.
- [Clear Site Data](https://www.w3.org/TR/clear-site-data/) defines a response header for requesting browser clearing of cache, cookies, DOM-accessible storage, and execution contexts. It is broad, origin-sensitive, and browser behavior must be tested before it becomes a logout or deletion control.
- [OWASP JavaScript and TypeScript Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/JavaScript_and_TypeScript_Security_Cheat_Sheet.html) recommends avoiding sensitive data and session identifiers in client storage and treating third-party scripts and unsafe DOM behavior as exposure paths.

## Decision Implications

- Persistence is a browser policy outcome, not an application durability guarantee. Design recovery and user communication for denial, eviction, clearing, quota pressure, and private-mode differences.
- `localStorage` is synchronous, string-based, and not a transactional cross-tab database. Use it only where its limited semantics are sufficient.
- IndexedDB transactions protect only their defined scope. Schema upgrades can block on other tabs and must account for long-lived clients, crash recovery, rollback, and incompatible code versions.
- Clearing browser state is not equivalent to completing backend deletion, vendor deletion, backup expiry, or legal erasure. Treat each as a separately verified surface.
