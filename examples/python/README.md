# OddSockets — Python quickstart

AsyncIO-native real-time messaging for Python. Pub/sub, presence and history with full async/await — the SDK handles manager discovery and reconnection.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
pip install oddsocketsai-python-sdk
```

## 60-second example

```python
import asyncio
from oddsockets import OddSockets

async def main():
    client = OddSockets(
        api_key='ak_live_1234567890abcdef',
        manager_url='https://connect.oddsockets.tyga.network'
    )

    channel = client.channel('my-channel')

    # Subscribe to messages
    async def on_message(message):
        print(f'Received: {message}')

    await channel.subscribe(on_message)

    # Publish a message
    await channel.publish('Hello from Python!')

    # Keep the connection alive
    await asyncio.sleep(10)

if __name__ == '__main__':
    asyncio.run(main())
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-python-sdk](https://github.com/jyswee/oddsockets-python-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
