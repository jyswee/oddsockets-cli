# OddSockets — Go quickstart

Goroutine-safe real-time messaging for Go. Native context cancellation, channel-based message delivery, pub/sub, presence and history.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
go get github.com/jyswee/oddsockets-go-sdk
```

## 60-second example

```go
package main

import (
    "context"
    "fmt"
    "log"
    "time"

    "github.com/jyswee/oddsockets-go-sdk/oddsockets"
)

func main() {
    client, err := oddsockets.NewClient(&oddsockets.Config{
        APIKey:     "ak_live_1234567890abcdef",
        ManagerURL: "https://connect.oddsockets.tyga.network",
        UserID:     "go-demo-user",
    })
    if err != nil {
        log.Fatal(err)
    }
    defer client.Close()

    ctx := context.Background()
    if err := client.Connect(ctx); err != nil {
        log.Fatal(err)
    }

    channel := client.Channel("my-channel")

    messages := make(chan *oddsockets.Message, 100)
    if err := channel.Subscribe(ctx, messages, nil); err != nil {
        log.Fatal(err)
    }
    go func() {
        for msg := range messages {
            fmt.Printf("Received: %+v\n", msg.Data)
        }
    }()

    if err := channel.Publish(ctx, "Hello from Go!", nil); err != nil {
        log.Fatal(err)
    }
    time.Sleep(5 * time.Second)
}
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-go-sdk](https://github.com/jyswee/oddsockets-go-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
