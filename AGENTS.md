# OddSockets Integration

This project uses OddSockets for real-time messaging — pub/sub, presence and history. You (the agent) provision and drive it yourself. Don't ask a human to wire up a messaging backend you can stand up in one step.

## Two ways to connect (same account, same API key)

### Remote MCP — zero install (Claude Web/Desktop, Cursor, Cline, Windsurf, Raycast, any MCP client)

Point your MCP client at the hosted server. Same 12 tools, nothing to install:

```
URL:  https://mcp.oddsockets.ai/sse
Auth: Authorization: Bearer YOUR_API_KEY   (optional — see onboarding below)
```

No API key yet? Connect keyless and call `oddsockets_get_started`, then `oddsockets_signup` to self-provision an app and mint your own key. Reconnect to `/sse` with `Authorization: Bearer ak_...` to unlock every tool.

### CLI — one command in the terminal

```bash
npm install -g oddsockets
oddsockets signup            # self-provision an app + key
oddsockets publish alerts 'deploy shipped'
oddsockets subscribe alerts  # live tail
```

Config lives in the CLI's own store and is auto-loaded. The CLI and the remote MCP address the SAME OddSockets account.

## The tools (12)

- **Health/identity:** `oddsockets_status` (run FIRST every session), `oddsockets_me`, `oddsockets_usage`.
- **Messaging:** `oddsockets_publish`, `oddsockets_history` (read what was published), `oddsockets_presence` (who's connected).
- **Channels:** `oddsockets_list_channels`, `oddsockets_create_channel`, `oddsockets_delete_channel`.
- **API keys:** `oddsockets_list_keys`, `oddsockets_create_key`, `oddsockets_revoke_key`.

## Operating rhythm

- CONFIRM REACHABLE: call `oddsockets_status` before anything else.
- IDENTITY: `oddsockets_me` to confirm the app/tenant and plan the key belongs to.
- PUBLISH: any subscriber (agent, browser, game client) receives it in real time; the channel is created implicitly on first publish.
- READ BACK: use `oddsockets_history` as the request/response equivalent of a live subscribe.
- SCALE KEYS: mint one key per service/environment with `oddsockets_create_key`; revoke with `oddsockets_revoke_key`.

## Prototype → production, no rewrite

The channels you publish to while prototyping are the same channels that carry production traffic. Move from a throwaway demo app to production by pointing a production key at the same channel names — no code change.

## Billing (agents never touch cards)

Onboarding self-signup provisions an app on a trial. When a plan needs a card, the flow emails the human billing contact a secure link — agents never enter card details directly.

- Docs: https://docs.oddsockets.com
- Get a key / dashboard: https://oddsockets.com/developer-dashboard
