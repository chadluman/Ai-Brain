# Frontend Runtime Resilience Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [Fetch Standard](https://fetch.spec.whatwg.org/) is the living normative model for requests, responses, network errors, CORS failures, cancellation, and abort behavior. HTTP error status is still an HTTP response; application code must classify it rather than equate promise fulfillment with success.
- [DOM Standard](https://dom.spec.whatwg.org/) defines `AbortSignal`, abort reasons, timeout signals, and combined signals. Platform support and framework cleanup behavior still require target testing.
- [WAI Forms Tutorial: User Notification](https://www.w3.org/WAI/tutorials/forms/notifications/) recommends clear, concise success and error feedback, inline association, and overall form results.
- [WCAG 2.2 Understanding 4.1.3: Status Messages](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html) explains when changing status information must be programmatically determinable without taking focus. It does not prescribe one live-region pattern for every message.
- [OWASP Web Frontend Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Web_Frontend_Security_Cheat_Sheet.html) provides defensive context for client-side data, injection, logging, third-party code, and browser controls.

## Decision Implications

- Separate user cancellation, deadline expiry, transport failure, HTTP status, schema failure, business rejection, and unknown defect. They require different retry, message, logging, and support behavior.
- Cancellation is cooperative. A browser abort does not establish that a server did not receive or commit a mutation; idempotency and reconciliation still protect consequential work.
- Accessible status is part of the operation contract. Visual spinners and generic toast messages are not enough when users need a field relationship, task result, focus path, or persistent recovery instruction.
- Error isolation should match ownership. A global handler is a last-resort signal, not a substitute for explicit states and recovery at request, feature, route, worker, and application boundaries.
