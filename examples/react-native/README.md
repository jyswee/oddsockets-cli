# OddSockets — React Native quickstart

Real-time pub/sub, presence and history for React Native / Expo apps. One client, live channels on mobile — the SDK handles reconnection and worker assignment.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
npm install @oddsocketsai/react-native-sdk
```

## 60-second example

```typescript
import OddSockets from '@oddsocketsai/react-native-sdk';

// Initialize the client
const client = new OddSockets({
  apiKey: 'your-api-key-here',
  userId: 'user-123'
});

// Get a channel
const channel = client.channel('my-channel');

// Subscribe to messages
await channel.subscribe((message) => {
  console.log('Received message:', message);
});

// Publish a message
await channel.publish('Hello, World!');
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-react-native-sdk](https://github.com/jyswee/oddsockets-react-native-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
