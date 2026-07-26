# OddSockets — Flutter quickstart

Cross-platform real-time messaging for Flutter (iOS, Android, web, desktop). Pub/sub, presence and history over the same channels as production.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```yaml
dependencies:
  oddsockets_flutter: ^1.0.0
```

## 60-second example

```dart
import 'package:oddsockets_flutter/oddsockets_flutter.dart';

final client = OddSocketsClient(
  config: OddSocketsConfig(apiKey: 'YOUR_API_KEY', userId: 'my-agent'),
);
await client.connect();

final channel = client.channel('my-channel');
channel.subscribe(onMessage: (msg) => print('Received: $msg'));
await channel.publish({'text': 'Hello from Flutter'});
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-flutter-sdk](https://github.com/jyswee/oddsockets-flutter-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
