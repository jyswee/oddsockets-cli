# OddSockets — C quickstart

Portable C real-time messaging for embedded / IoT. Small footprint, callback-based pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

Build from source with GCC or Clang — see the [SDK repo](https://github.com/jyswee/oddsockets-c-sdk) for the full build instructions.

## 60-second example

```c
#include "oddsockets.h"

void on_message(const char* channel_name, const char* message, void* user_data) {
    printf("Received: %s\n", message);
}

int main() {
    oddsockets_config_t config = {
        .api_key = "your-api-key",
        .user_id = "user123",
        .auto_connect = true
    };

    oddsockets_client_t* client = oddsockets_create(&config);
    oddsockets_channel_t* channel = oddsockets_channel_create(client, "my-channel");

    oddsockets_channel_subscribe(channel, on_message, NULL);
    oddsockets_channel_publish(channel, "Hello, World!", NULL);

    oddsockets_channel_destroy(channel);
    oddsockets_destroy(client);
    return 0;
}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-c-sdk](https://github.com/jyswee/oddsockets-c-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
