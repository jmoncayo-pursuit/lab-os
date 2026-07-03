# Network Boundaries

Applies to every fleet/suite service that opens a listening socket (HTTP, WebSocket, MCP bridge, anything). Exemplar implementation: `~/.fleet/fleet-serve`. Origin: the 2026-07-03 fleet codebase audit - three services bound all interfaces while fleet-serve already carried the correct pattern; this rule makes the right pattern the default a new service copies.

## The pattern (all four, every listener)

1. **Loopback by default.** Bind `127.0.0.1` explicitly; the host is env-overridable, never hardcoded open. A bare `listen(port)` / `serve({port})` with no host binds all interfaces and is a defect, not a default:
   - Node http/express: `server.listen(port, "127.0.0.1")`
   - Hono node-server: `serve({ fetch, port, hostname: "127.0.0.1" })`
   - Python http.server: `ThreadingHTTPServer((os.environ.get("HOST", "127.0.0.1"), port), ...)`
2. **DNS-rebinding guard.** Any endpoint a browser will call validates the `Host` header (and `Origin` on CORS requests) against a loopback allowlist (`127.0.0.1`, `localhost`, `[::1]`, env-extendable). CORS reflects loopback origins only - never wildcard `*` (a wildcard lets any open tab read the service).
3. **Side-effect endpoints require auth before any wider exposure.** An endpoint that mutates state, spawns a process, or approves an action never rides a bind widened beyond loopback without an auth layer added in the same change.
4. **Widening is a decision, not a config drift.** Exposing beyond loopback (LAN bind, tunnel, deploy) is a per-service, logged decision with the owner's explicit go - route per the approval gates, never a silent env default.

## Review check

New or changed listener in the diff? Confirm: explicit loopback bind, Host/Origin guard on browser-facing routes, no wildcard CORS, and no side-effect route left unauthenticated if the bind is ever widened. Tests binding `127.0.0.1` do not prove the service does - assert on the configured host, not the test harness default.
