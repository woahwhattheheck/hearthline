# Native MCP App action controls

The `ui://hearthline/mission-dashboard.html` resource exposes a mission's local actions inside a compatible MCP Apps host. It uses the existing orchestrator, approval records, operation IDs, receipts, and persistent store.

## Use

Open a mission through `hearthline_prepare_storm` or `hearthline_get_mission` in a host that renders the resource. The host must negotiate MCP Apps `2026-01-26` and advertise `hostCapabilities.serverTools`. Without that capability the resource remains readable, with its controls disabled.

Each local shopping handoff or reminder exposes separate steps:

1. **Approve local handoff / reminder** binds the displayed action and current plan hash to one durable operation. This does not execute it.
2. **Execute approved local action** uses the operation ID returned by the server. Shopping produces `prepared_not_purchased`; reminders remain in the local outbox.
3. **Replay original receipt** repeats the same operation, not a new action. The displayed receipt includes the server's digest and replay flag.

**Refresh mission** explicitly reads current durable state. A refusal, invalid response, or timeout never appears as success. After an uncertain outcome, mutation controls stay disabled until a successful refresh reconciles the server state. If an approval committed but its response was lost, refresh recovers its existing operation ID rather than creating a second approval. A repeated approval for the same displayed action and plan uses a deterministic operation ID. The server still validates every operation, action and plan hash.

There are no direct network requests from the resource, automatic approvals, background polling, or embedded credentials. All calls use host-mediated `tools/call`; responses are correlated to one pending request with a 30-second timeout. Parent-frame identity and the negotiated parent origin are checked. User and server strings are rendered as text, not HTML.

The standalone source bundle includes the resource implementation. Test files are not included in this source subset.

Protocol references:
- https://github.com/modelcontextprotocol/ext-apps/blob/main/specification/2026-01-26/apps.mdx
- https://apps.extensions.modelcontextprotocol.io/api/documents/overview.html