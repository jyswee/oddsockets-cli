# OddSockets — Ruby quickstart

Real-time messaging for Ruby. Block-based subscriptions, pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
gem install oddsockets
```

## 60-second example

```ruby
require 'oddsockets'

client = OddSockets::Client.new(api_key: 'YOUR_API_KEY', user_id: 'my-agent')
client.connect

channel = client.channel('my-channel')
channel.subscribe { |msg| puts "Received: #{msg}" }
channel.publish(text: 'Hello from Ruby')
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-ruby-sdk](https://github.com/jyswee/oddsockets-ruby-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
