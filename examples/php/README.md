# OddSockets — PHP quickstart

Real-time messaging for PHP. Pub/sub, presence and history — the SDK handles manager discovery and worker assignment.

> Prefer the terminal? The [`oddsockets` CLI](../../README.md) does the same over any channel — no code.

## Install

```bash
composer require jyswee/oddsockets-php-sdk
```

## 60-second example

```php
use OddSockets\OddSocketsClient;
use OddSockets\Config\OddSocketsConfig;

$config = new OddSocketsConfig(['apiKey' => 'YOUR_API_KEY', 'userId' => 'my-agent']);
$client = new OddSocketsClient($config);
$client->connect();

$channel = $client->channel('my-channel');
$channel->subscribe(function($msg) { echo "Received: " . json_encode($msg); });
$channel->publish(['text' => 'Hello from PHP']);
```

## What you get

- **Pub/sub** — publish to a channel, every subscriber gets it instantly.
- **Presence** — see who's connected in real time.
- **History** — replay recent messages a late-joining client missed.
- **Auto-reconnect** — session-sticky worker assignment, exponential backoff.

## Full SDK, docs & examples

The complete SDK — every method, types, and runnable examples — lives in its own repo:

**→ [oddsockets-php-sdk](https://github.com/jyswee/oddsockets-php-sdk)**

- [Documentation](https://docs.oddsockets.com)
- [Get an API key](https://oddsockets.com/developer-dashboard)
- [All 19 SDKs](../../README.md#sdks)
