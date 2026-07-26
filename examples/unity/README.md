# OddSockets — Unity quickstart

Real-time messaging for Unity games. MonoBehaviour-friendly client with coroutine-based connect and pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

Add the package via the Unity Package Manager (Git URL) — see the [SDK repo](https://github.com/jyswee/oddsockets-unity-sdk) for the exact UPM install steps.

## 60-second example

```csharp
using UnityEngine;
using OddSockets.Unity;

public class ChatManager : MonoBehaviour
{
    private OddSocketsUnityClient client;

    void Start()
    {
        var config = new OddSocketsUnityConfig
        {
            ApiKey = "your-api-key-here",
            UserId = "user123",
            AutoConnect = true
        };

        client = new OddSocketsUnityClient(config);
        client.OnConnected += OnConnected;
        StartCoroutine(client.ConnectAsync());
    }

    private void OnConnected()
    {
        Debug.Log("Connected to OddSockets!");
        var channel = client.Channel("chat-room");
        StartCoroutine(channel.SubscribeAsync(msg => Debug.Log("Received: " + msg)));
    }
}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-unity-sdk](https://github.com/jyswee/oddsockets-unity-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
