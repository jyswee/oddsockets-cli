# OddSockets — JavaScript quickstart

Real-time pub/sub, presence and history for the browser and Node.js. The SDK handles manager discovery, worker load-balancing and reconnection — you just publish and subscribe.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
npm install @oddsocketsai/javascript-sdk
```

## 60-second example

```javascript
import OddSockets from '@oddsocketsai/javascript-sdk';

// Create client (auto-connects by default)
const client = new OddSockets({
  apiKey: 'your-api-key-here'
});

// Get a channel
const channel = client.channel('my-channel');

// Subscribe to messages
channel.subscribe((message) => {
  console.log('Received:', message);
});

// Publish a message
channel.publish('Hello, World!');
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-javascript-sdk](https://github.com/jyswee/oddsockets-javascript-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
