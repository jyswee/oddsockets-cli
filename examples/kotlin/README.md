# OddSockets — Kotlin quickstart

Coroutine-first real-time messaging for Kotlin / Android. Suspend functions, pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```kotlin
// build.gradle.kts
dependencies {
    implementation("com.oddsockets:oddsockets-kotlin-sdk:1.0.0")
}
```

## 60-second example

```kotlin
val client = OddSocketsClient(OddSocketsConfig(apiKey = "YOUR_API_KEY", userId = "my-agent"))
client.connect()

val channel = client.channel("my-channel")
channel.subscribe { msg -> println("Received: $msg") }
channel.publish(mapOf("text" to "Hello from Kotlin"))
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-kotlin-sdk](https://github.com/jyswee/oddsockets-kotlin-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
