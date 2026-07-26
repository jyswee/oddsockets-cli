# OddSockets — Unreal Engine quickstart

Real-time messaging for Unreal Engine 5. An `AOddSocketsClient` actor with Blueprint-exposed events for pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

Add the plugin to your project's `Plugins/` folder — see the [SDK repo](https://github.com/jyswee/oddsockets-unrealengine-sdk) for the full setup and module wiring.

## 60-second example

```cpp
#include "OddSocketsClient.h"

void AMyGameActor::BeginPlay()
{
    Super::BeginPlay();

    // Spawn and configure the client
    OddSocketsClient = GetWorld()->SpawnActor<AOddSocketsClient>();

    FOddSocketsConfig Config;
    Config.ApiKey = TEXT("your-api-key");
    Config.UserId = TEXT("user123");

    // Bind the message event, then connect + subscribe
    OddSocketsClient->OnChannelMessage.AddDynamic(this, &AMyGameActor::OnChannelMessage);
    OddSocketsClient->Connect(Config);
    OddSocketsClient->Subscribe(TEXT("my-channel"));
}

void AMyGameActor::OnChannelMessage(const FOddSocketsChannelMessageData& MessageData)
{
    UE_LOG(LogTemp, Log, TEXT("Received: %s"), *MessageData.Message);
}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-unrealengine-sdk](https://github.com/jyswee/oddsockets-unrealengine-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
