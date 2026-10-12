# Hearthline

Hearthline manages household tasks, inventory and reusable missions through a self-hosted Node.js MCP server. This source copy contains the server and the browser workboard client used for the recorded local demo.

## Run the browser workspace

Requires Node.js 20 or later. From this folder, start the local host:

```sh
node hearthline-browser-demo/server.mjs
```

Open `http://127.0.0.1:8790/`. The workspace is saved to `data/hearthline-browser-store.json` relative to the launch directory; set `HEARTHLINE_STORE` to use another path. No npm install is needed for this browser path.

The standalone MCP server can also be started from `hearthline-alexa-mcp/` with `npm start` (endpoint `http://127.0.0.1:8787/mcp`), or its fixture demonstration can be run with `npm run demo`.

## What is included

The MCP server provides mission planning, approvals, durable operation receipts, and household task and inventory tools. The browser client calls the server over local Streamable HTTP. The JSON store preserves missions, workboard state, stock, and receipts across restarts.

The 66.96-second demo records a local browser workflow: tasks across two missions, a rejected stale edit, a host restart with saved state intact, receipt replay without duplicate effects, and a follow-on mission using updated stock.

## Demo boundaries

The browser demonstration uses visibly labeled sample weather. Shopping stops at a local `prepared_not_purchased` handoff, and reminders remain in a local outbox. It does not show a purchase, delivered message, Alexa device session, live weather request, or AWS deployment/service.

## Source and license

This standalone source subset is pinned to upstream commit `86d10426f486bfffa09ac6162a37d7190f93d178`. `SOURCE_COPY_MANIFEST.json` records the exact upstream commit and Git blob IDs for every copied source file. The copy omits tests, optional integrations, generated workspace data, and unrelated projects. Paths are preserved so imports between the browser host and MCP server continue to resolve.

The included server source is licensed under MIT; see [`hearthline-alexa-mcp/LICENSE`](hearthline-alexa-mcp/LICENSE).