# OddSockets — C# / .NET quickstart

Real-time messaging for .NET. async/await API, pub/sub, presence and history — with first-class ASP.NET Core integration.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
dotnet add package OddSockets.DotNet.SDK
```

## 60-second example

```csharp
using OddSockets;
using OddSockets.Models;

var config = new OddSocketsConfigBuilder()
    .WithApiKey("ak_live_your_api_key_here")
    .WithUserId("user123")
    .Build();

using var client = new OddSocketsClient(config);
await client.ConnectAsync();

var channel = client.Channel("my-channel");
await channel.SubscribeAsync(message =>
{
    Console.WriteLine($"Received: {message.Data}");
});

await channel.PublishAsync("Hello, OddSockets!");
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-csharp-sdk](https://github.com/jyswee/oddsockets-csharp-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
