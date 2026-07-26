# OddSockets — Elixir quickstart

Real-time messaging for Elixir / OTP. GenServer-backed client, pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```elixir
# mix.exs
def deps do
  [
    {:oddsockets, "~> 1.0.0"}
  ]
end
```

## 60-second example

```elixir
# Start a client
{:ok, client} = OddSockets.start_link(api_key: "your-api-key")

# Get a channel
channel = OddSockets.channel(client, "my-channel")

# Subscribe to messages
:ok = OddSockets.Channel.subscribe(channel, fn message ->
  IO.inspect(message, label: "Received")
end)

# Publish a message
{:ok, result} = OddSockets.Channel.publish(channel, %{text: "Hello World!"})
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-elixir-sdk](https://github.com/jyswee/oddsockets-elixir-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
