# Realtime Transport Evidence

Verified: 2026-10-21

## Standards

- [WHATWG Server-Sent Events](https://html.spec.whatwg.org/multipage/server-sent-events.html) defines `EventSource`, `text/event-stream`, reconnection, event IDs, and server-to-client event delivery in the HTML Living Standard.
- [RFC 6455: WebSocket Protocol](https://www.rfc-editor.org/rfc/rfc6455.html) defines the WebSocket handshake, origin-based browser security model, framing, and full-duplex protocol. Application semantics remain the implementer's responsibility.
- [WebRTC Recommendation](https://www.w3.org/TR/webrtc/) dated 2025-03-13 defines browser APIs for real-time media and data. Signaling, identity, TURN operation, privacy, and application protocol remain architectural concerns.
- [WebTransport](https://www.w3.org/TR/webtransport/) was a W3C Candidate Recommendation Snapshot dated 2026-07-30 at verification, not a final Recommendation. Verify browser, network, and server support before adoption.
- [HTTP Semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html) remains the basis for polling, streaming HTTP responses, authentication, intermediaries, and status behavior.

## Interpretation Boundaries

- “Realtime” does not imply exactly once, globally ordered, or durable. Those are application and infrastructure properties.
- WebSocket supplies framing, not message schema, replay, authorization, backpressure policy, or recovery.
- Mobile push and background delivery are controlled by operating systems and may be delayed or omitted; use them as notifications with reconciliation.
- Protocol and browser support change. Test actual clients, proxies, mobile networks, corporate networks, and deployment platforms.
