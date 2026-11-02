---
name: desktop-web-shell-design
description: Wrap a web app in a desktop shell with a narrow native bridge, so desktop features such as tray, file access, and local services work without giving the web page unrestricted access to the machine. Use when a web product needs a desktop companion; do not use for mobile WebView work, which is covered by the separate WebView Hybrid Integration skill, or for distribution, which is covered by Desktop App Distribution Design.
---

# Desktop Web Shell Design

## Outcome

Produce a desktop shell whose web page can do exactly the native things it needs, through a small, typed, allowlisted bridge, and nothing else, so a compromised or malicious page cannot become a compromised machine.

The mobile analogue is the separate WebView Hybrid Integration skill, which is not on main yet; link it here after that skill merges. Use this skill for desktop shells, where the native surface is larger: files, processes, system tray, global shortcuts, and local services.

## Required Inputs

- The desktop-only features actually needed: tray or menu bar, file picking or watching, local service control, global shortcuts, notifications, or deep links, with each feature justified.
- The shell shape: a bundled browser engine or the operating system's own WebView, and the tradeoff that choice makes for size, API surface, and update burden.
- The bridge surface: the exact native functions the page may call, their arguments, and their return shapes, before any code is written.
- The local-service model, if any: what runs on the user's machine, which port or socket it uses, and how the page proves it is the app's page.
- The data boundary: what lives on the machine, what lives in the cloud, and what must never be copied between them without the user's action.

If the feature list is "everything the web app does, plus desktop," narrow it first. A shell that mirrors the whole web app with a generic native bridge is not a design.

## Workflow

1. Choose the shell shape explicitly. A bundled engine gives a consistent browser and Node-like APIs at the cost of size and a larger update surface. An OS WebView gives a small binary and OS updates at the cost of engine differences across machines. Record the choice and its update owner; do not let the choice drift by framework default.
2. Define the bridge as a small, typed API, and enforce it in the native layer, not in JavaScript. Each function takes validated arguments, returns only what the page needs, and is allowlisted by name. There is no generic "run command," "read file," or "evaluate code" function, and the page never receives a direct handle to a native module.
3. Isolate the renderer. Enable context isolation and sandboxing where the shell supports them, keep Node and native access out of the renderer, and put all privileged work behind the bridge in the main process. A page that can require a native module has no bridge, whatever the documentation calls it.
4. Treat local services as a trust boundary. A local HTTP or socket service must authenticate the caller (for example, a per-install token the shell holds, not a fixed port with no auth), bind to localhost only, and reject requests from any other origin. A local service with no authentication is a local privilege escalation waiting for a browser tab.
5. Handle desktop lifecycle explicitly: single instance or multi-instance, deep-link routing to the running instance, window state and restore, tray behavior on close, and clean shutdown of local services. Test each on a clean machine, not only on a developer machine where services are already running.
6. Keep file access user-initiated where it matters. Prefer system file dialogs for picking files and folders; for watched folders or background access, require an explicit grant the user can see and revoke, and record what was granted.
7. Separate shell code from web code in review and testing. Shell changes, bridge changes, and local-service changes are security-relevant even when they look like UI work, and they are reviewed at the boundary that applies.

## Safety and Permission Boundaries

- Treat web content as untrusted, even when it is your own app's page. A cross-site scripting flaw in the page must not become code execution on the machine, because the bridge is the only path to native capability and it is allowlisted.
- Never expose secrets, tokens, or other users' data through the bridge, and never log bridge arguments that contain credentials or file paths the user has not chosen to share.
- Never auto-run, auto-install, or auto-update a local service without the user's consent and a verified, signed update. Distribution and update integrity are covered by [Desktop App Distribution Design](../desktop-app-distribution-design/SKILL.md).
- A new shell framework, native module, or bridge library still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Outputs and Evidence

- A shell-shape decision with its size, engine, and update tradeoffs.
- A bridge specification: function list, argument validation, and return shapes, with everything not listed explicitly denied.
- A local-service authentication and localhost-binding design, with the lifecycle and shutdown behavior.
- Tests or a test report covering renderer isolation, bridge allowlisting, local-service authentication, and clean-machine lifecycle.
