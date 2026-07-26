# OddSockets — Swift quickstart

Real-time messaging for iOS / macOS with Combine + async/await. Pub/sub, presence and history, ready for SwiftUI.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```swift
// Package.swift
dependencies: [
    .package(url: "https://github.com/jyswee/oddsockets-swift-sdk.git", from: "0.1.0")
]
```

## 60-second example

```swift
import OddSockets

let config = try OddSocketsConfigBuilder()
    .apiKey("ak_your_api_key_here")
    .userId("user123")
    .build()

let client = try OddSocketsClient(config: config)
try await client.connect()

let channel = try client.channel("my-channel")
try await channel.subscribe { message in
    print("Received: \(message)")
}
_ = try await channel.publish("Hello from Swift!")
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-swift-sdk](https://github.com/jyswee/oddsockets-swift-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
