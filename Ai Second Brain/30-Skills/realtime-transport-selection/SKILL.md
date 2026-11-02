---
name: realtime-transport-selection
description: Select or review polling, long polling, server-sent events, WebSocket, WebTransport, WebRTC, webhook, or push-notification communication for live web and mobile features. Use when update direction, latency, ordering, reliability, media, scale, or reconnect behavior matters; do not choose a persistent connection by fashion alone.
---

# Realtime Transport Selection

## Outcome

Choose the simplest communication mode that meets the actual update direction and latency need, with explicit authorization, backpressure, ordering, reconnection, recovery, and scale behavior.

## Required Inputs

- producers, consumers, message direction, payload, frequency, burst, and size
- latency, reliability, order, duplication, presence, fan-out, and offline requirements
- browser, mobile, network, proxy, firewall, and background constraints
- authentication, authorization, tenant, privacy, retention, and abuse risks
- connection count, geographic scale, operating model, cost, and fallback

## Safety and Permission Constraints

- Authenticate the connection and authorize each subscription, channel, message, and state-changing action. A connected client does not gain blanket access.
- Do not put long-lived credentials in URLs. Define credential refresh, revocation, logout, and connection termination.
- Bound message size, rate, queue depth, fan-out, connection duration, retries, and server work. Apply backpressure or disconnect slow consumers.
- Treat messages as untrusted, versioned input. Validate origin, schema, tenant, sequence, and authorization at the trusted boundary.
- Encrypt transport and minimize message data. Do not leak protected state through channel names, presence, error details, counts, or resume cursors.
- Enabling production broadcast or media infrastructure is R3 and requires immediate authorization, capacity limits, and rollback.

## Workflow

1. Define what "realtime" means numerically and what happens if an update is late, duplicated, reordered, or lost.
2. Choose the least complex fitting mode:
   - ordinary polling for tolerant, low-frequency refresh;
   - server-sent events for server-to-browser text event streams with HTTP reconnection semantics;
   - WebSocket for full-duplex application messages;
   - WebRTC for peer-oriented real-time media or data with its signaling and network complexity;
   - WebTransport only for requirements benefiting from its stream or datagram model and supported environments;
   - webhook or mobile push for server-to-server or background notification rather than an open foreground connection.
3. Specify the application protocol independently of transport: envelope, version, identity, sequence, acknowledgement, errors, limits, and compatibility.
4. Define authorization at subscribe and delivery time, including policy change and revocation while connected.
5. Define delivery semantics, per-key ordering, idempotency, resume cursors, snapshots, gap detection, reconciliation, and resynchronization.
6. Design heartbeats, idle timeout, exponential reconnect with jitter, connection migration, offline queueing, and duplicate suppression.
7. Model fan-out, slow consumers, hot keys, broker partitions, load balancing, connection draining, deploys, and regional failure.
8. Provide fallback or degraded behavior for unsupported browsers, constrained networks, disabled background delivery, and service outage.
9. Test proxy interruption, mobile network changes, sleep and resume, token expiry, revoked access, duplicate and out-of-order messages, overload, deploy, and regional recovery.

## Required Output

- communication requirements and transport comparison
- selected transport plus fallback and protocol contract
- authentication, authorization, privacy, and abuse controls
- delivery, ordering, resume, reconciliation, and backpressure behavior
- connection, fan-out, capacity, observability, cost, and deployment plan
- failure-test evidence and rollback path

## Completion Gate

Do not call the design ready until reconnect and gap recovery preserve state, revoked clients stop receiving protected data, slow consumers cannot exhaust the service, and the chosen transport works through representative networks and supported clients.

## Conditional Reference

Read [Realtime Transport Evidence](references/realtime-evidence.md) when comparing browser transport capabilities or maturity.
