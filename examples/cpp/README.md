# OddSockets — C++ quickstart

C++17 real-time messaging for native and embedded apps. Pub/sub, presence and history with an event-driven client loop.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

Build from source with CMake — see the [SDK repo](https://github.com/jyswee/oddsockets-cpp-sdk) for the full build instructions and dependencies.

## 60-second example

```cpp
#include "oddsockets/OddSockets.hpp"

int main() {
    oddsockets::Config config;
    config.apiKey = "your-api-key";
    config.userId = "user123";

    auto client = std::make_unique<oddsockets::OddSockets>(config);

    client->connect().then([&](bool success) {
        if (success) {
            auto channel = client->channel("my-channel");
            channel->subscribe([](const std::string& message) {
                std::cout << "Received: " << message << std::endl;
            });
            channel->publish("Hello, World!");
        }
    });

    while (client->isConnected()) {
        client->processEvents();
        std::this_thread::sleep_for(std::chrono::milliseconds(10));
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

**→ [oddsockets-cpp-sdk](https://github.com/jyswee/oddsockets-cpp-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
