# Agent and Tool Safety Evidence

Verified: 2026-10-22

## Current Standards and Threat Guidance

- [MCP 2026-07-28 security best practices](https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices) covers confused-deputy flows, token passthrough, SSRF, state-handle hijacking, local-server compromise, redirect validation, mix-up attacks, credential binding, and scope minimization. It must be read with the exact protocol revision and OAuth guidance.
- [MCP 2026-07-28 authorization](https://modelcontextprotocol.io/specification/2026-07-28/basic/authorization) defines HTTP transport authorization, protected-resource metadata, discovery, issuer validation, registration choices, and incremental scope selection. Authorization is optional in the protocol; an implementation still needs application-level identity and resource policy.
- [MCP 2026-07-28 tools](https://modelcontextprotocol.io/specification/2026-07-28/server/tools) says tools are model-controlled but recommends visible exposure, invocation indicators, confirmation, and a human ability to deny calls. Tool annotations are explicitly untrusted unless their server is trusted.
- [OWASP Top 10 for Agentic Applications](https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/) summarizes goal hijack, tool misuse, identity and privilege abuse, supply-chain compromise, unexpected execution, memory and communication risks, cascading failure, trust exploitation, and rogue agents. It is a threat prompt, not complete assurance.
- [OWASP Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/) provides a threat-model-based taxonomy and layered mitigations for agentic systems. Recheck revisions because this area is evolving quickly.
- [OWASP LLM06:2025 Excessive Agency](https://genai.owasp.org/llmrisk/llm062025-excessive-agency/) emphasizes minimizing tools, functions, permissions, and autonomy and independently approving high-impact actions.

## Decision Implications

- MCP interoperability does not approve a server, SDK, tool, or permission. Review the complete exact-version asset before connection or execution.
- Protocol authentication and OAuth scopes do not replace tenant and object authorization at tool execution.
- Tool descriptions and annotations can be poisoned. Treat them as code-adjacent supply-chain inputs and do not let metadata grant trust.
- Human-in-the-loop is effective only when the confirmation is comprehensible, specific, timely, and enforced by deterministic execution code.
- Current MCP changed materially in July 2026, including stateless requests, authorization hardening, caching, headers, and deprecated older mechanisms. Pin the revision and recheck SDK conformance rather than assuming compatibility.
