# OddSockets — Java quickstart

Real-time messaging for the JVM. Futures-based API, pub/sub, presence and history — the SDK handles manager discovery and reconnection.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```groovy
// build.gradle
implementation 'com.oddsockets:oddsockets-java-sdk:0.1.0-beta.1'
```

## 60-second example

```java
import com.oddsockets.OddSockets;
import com.oddsockets.Channel;
import com.oddsockets.config.OddSocketsConfig;

public class BasicExample {
    public static void main(String[] args) throws Exception {
        OddSocketsConfig config = OddSocketsConfig.builder()
            .apiKey("ak_live_1234567890abcdef")
            .managerUrl("https://connect.oddsockets.tyga.network")
            .userId("java-demo-user")
            .build();

        OddSockets client = new OddSockets(config);
        client.connect().get();

        Channel channel = client.channel("my-channel");
        channel.subscribe(message -> {
            System.out.println("Received: " + message.getData());
        }).get();

        channel.publish("Hello from Java!").get();
        Thread.sleep(5000);
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

**→ [oddsockets-java-sdk](https://github.com/jyswee/oddsockets-java-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
