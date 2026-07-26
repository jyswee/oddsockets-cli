# OddSockets — Svelte quickstart

Reactive real-time stores for Svelte — messages and presence update your UI automatically. Pub/sub, presence and history over the same channels as production.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
npm install oddsockets-svelte-sdk
```

## 60-second example

```svelte
<script>
  import { createChannelStore } from 'oddsockets-svelte-sdk/stores';
  import { onMount } from 'svelte';

  const { messages, presence, publish, subscribe, unsubscribe } = createChannelStore('chat', {
    apiKey: 'ak_your_api_key_here',
    userId: 'user123'
  });

  onMount(() => {
    subscribe();
    return unsubscribe; // cleanup on destroy
  });
</script>

<!-- Reactive UI updates automatically -->
{#each $messages as message}
  <div>{message.data.text}</div>
{/each}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-svelte-sdk](https://github.com/jyswee/oddsockets-svelte-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
