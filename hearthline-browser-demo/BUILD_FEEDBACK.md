# Hearthline browser-workboard observations

The recorded local workflow used the browser as an MCP client of the same Hearthline service. It completed four tasks across two saved missions, rejected a stale second-client edit, retained the mission and stock through a full host restart, and replayed a receipt without adding a duplicate local effect. The video uses a labeled sample-weather fixture, a local shopping handoff and a local reminder outbox.

## What worked well

- The browser completed MCP initialization, tool discovery and calls to the 12 registered tools.
- The local workspace retained mission, task and stock state after restart.
- Revision checks rejected an outdated edit while preserving the newer value.
- Replaying a completed operation returned its original receipt without adding another receipt or outbox item.
- The Node.js runtime path has no npm runtime dependencies.

## Areas to improve

- Keep the human approval step visually separate from execution so users can tell that approval alone does not buy, send or book anything.
- Show a clear reconnect or restart status alongside saved-state and receipt indicators.
- MCP documentation should clearly distinguish package generations and the separate versions used for MCP HTTP and MCP Apps.
- Clients should distinguish a tool-level error from an HTTP transport error.

This is product feedback from the documented local engineering run, not Alexa-device or AWS service testing.