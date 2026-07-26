# OddSockets — Node.js quickstart

Real-time pub/sub, presence and history for Node.js. Connect, subscribe, and publish in a few lines — the SDK handles manager discovery, worker load-balancing and reconnection for you.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
npm install @oddsocketsai/nodejs-sdk
```

## 60-second example

```javascript
const OddSockets = require('@oddsocketsai/nodejs-sdk');

const client = new OddSockets({
  apiKey: 'your-api-key-here',   // from `oddsockets signup` or the dashboard
  userId: 'user-123'
});

client.on('connected', () => console.log('Connected to OddSockets'));

const channel = client.channel('my-channel');

// Subscribe — every message arrives the instant it's published
await channel.subscribe((message) => {
  console.log('Received:', message);
});

// Publish
await channel.publish({ text: 'Hello World!', timestamp: new Date().toISOString() });
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — exponential backoff, session-sticky worker assignment.

## Full SDK, docs & examples

The complete SDK — every method, TypeScript types, and runnable examples — lives in its own repo:

**→ [oddsockets-nodejs-sdk](https://github.com/jyswee/oddsockets-nodejs-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
