# OddSockets — Rust quickstart

Tokio-async real-time messaging for Rust. Streaming subscriptions, pub/sub, presence and history with strong typing.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```toml
[dependencies]
oddsockets = "0.1.0-beta.1"
tokio = { version = "1.0", features = ["full"] }
```

## 60-second example

```rust
use oddsockets::{OddSocketsClient, OddSocketsConfig, message_types};

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let config = OddSocketsConfig::new("ak_your_api_key_here");
    let client = OddSocketsClient::new(config).await?;
    client.connect().await?;

    let channel = client.channel("my-channel");
    let mut message_stream = channel.subscribe(Default::default()).await?;

    let message = message_types::chat_message("Hello, Rust!", "user123", None);
    channel.publish(message, Default::default()).await?;

    while let Some(message) = message_stream.recv().await {
        println!("Received: {:?}", message);
    }
    Ok(())
}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-rust-sdk](https://github.com/jyswee/oddsockets-rust-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
