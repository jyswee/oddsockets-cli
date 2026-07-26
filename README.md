# oddsockets

[![npm version](https://img.shields.io/npm/v/oddsockets.svg)](https://www.npmjs.com/package/oddsockets)
[![Real-time](https://img.shields.io/badge/pub%2Fsub-presence%20%2B%20history-f97316)](#see-it-live)
[![Zero deps](https://img.shields.io/badge/dependencies-0-3fb950)](#install)

**Real-time messaging for coding agents — pub/sub, presence and history your agent provisions itself, from the command line.**

> **Prototype in one command. Ship the same channels to production — no rewrite.**

Your agent can write the app but can't give it a real-time backbone without you stopping to wire up a messaging service. `oddsockets` is the CLI the agent runs itself: one install, and it signs up, mints its own key, and starts publishing and subscribing to live channels — the same channels that carry your production traffic. Zero dependencies.

**Works with:** Claude Code · Cursor · Cline · Windsurf · Aider · Codex · any terminal

[![oddsockets demo — signup to your first real-time message in 60 seconds](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/signup-demo.gif)](https://oddsockets.com/#demo)

*Signup to your first real-time message in 60 seconds — [watch the full demo](https://oddsockets.com/#demo).*

## See it live

Each demo below is a **real CLI session** — a throwaway account, a real key, real messages over the live cluster — stitched to the **developer dashboard** showing that same traffic. Click any tab for the full-res video.

| Signup → first message | Live pub/sub | Who's online | Agent integration |
|---|---|---|---|
| [![Signup to first real-time message](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/signup-demo.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/signup-demo.mp4) | [![Live pub/sub on one channel](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/pubsub-demo.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/pubsub-demo.mp4) | [![Presence — who is online now](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/presence-demo.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/presence-demo.mp4) | [![One-line agent integration + history](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/agent-demo.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/demo/agent-demo.mp4) |
| Fresh app, first message in seconds | One channel, two messages, instant | Live member list | `publish` + `history` in one line |

*[Watch the full set on oddsockets.com →](https://oddsockets.com/#demo)*

## Install

```bash
npm install -g oddsockets
```

## Quick Start

```bash
# 1. Sign up (instant API key, no email verification)
oddsockets signup my-app --local

# 2. Publish a message
oddsockets publish my-channel "Hello from the CLI!"

# 3. Subscribe (live tail)
oddsockets subscribe my-channel

# 4. Check who's online
oddsockets presence my-channel
```

## Pub/sub — one channel, real-time

The core primitive: publish to a channel, subscribe to tail it live. Every subscriber gets every message the instant it lands — no polling, no queue to run.

```bash
oddsockets subscribe room-42 &                     # live tail in the background
oddsockets publish room-42 "hello from the CLI"    # arrives on the tail instantly
oddsockets publish room-42 --file payload.json     # publish structured data from a file
```

## Presence — who's online, right now

Ask any channel who's connected. Presence is tracked server-side and updates in real time as clients join and leave.

```bash
oddsockets subscribe lobby &     # join the channel
oddsockets presence lobby        # live member list
```

## History — replay what you missed

Channels keep a rolling message history, so a client that connects late (or your agent after a context reset) can catch up.

```bash
oddsockets history agent-bus --limit 10
```

## Agent Integration

Add to your `CLAUDE.md`, `.cursorrules`, `.clinerules`, or `.windsurfrules`:

```markdown
## OddSockets
Use the `oddsockets` CLI for real-time messaging.
Key is in .oddsockets/config.json (auto-loaded).

oddsockets status                           # cluster health
oddsockets publish my-channel "message"     # send message
oddsockets subscribe my-channel             # live tail
oddsockets presence my-channel              # who's online
oddsockets keys                             # list API keys
```

## Commands

### Setup
| Command | Description |
|---------|-------------|
| `oddsockets signup <app> [--email x] [--local]` | Sign up, get instant API key |
| `oddsockets login --key KEY [--local]` | Save existing API key |
| `oddsockets logout [--local]` | Clear config |
| `oddsockets me` | Account info + plan |
| `oddsockets status` | Cluster health + platform stats |

### Messaging
| Command | Description |
|---------|-------------|
| `oddsockets publish <channel> "message"` | Publish message |
| `oddsockets publish <channel> --file data.json` | Publish from file |
| `oddsockets subscribe <channel>` | Live tail (Ctrl+C to stop) |
| `oddsockets history <channel> [--limit 10]` | Message history |
| `oddsockets presence <channel>` | Channel members |

### Channels
| Command | Description |
|---------|-------------|
| `oddsockets channels` | List channels |
| `oddsockets channel create <name>` | Create channel |
| `oddsockets channel delete <name>` | Delete channel |

### API Keys
| Command | Description |
|---------|-------------|
| `oddsockets keys` | List API keys |
| `oddsockets key create "name"` | Create new key |
| `oddsockets key revoke <id>` | Revoke key |

## Flags

- `--json` — Machine-readable JSON output (every command)
- `--key KEY` — Override API key for one command
- `--local` — Use project-local config (`.oddsockets/`)
- `--help` — Help

## Config Priority

1. `--key` flag
2. `ODDSOCKETS_API_KEY` environment variable
3. `.oddsockets/config.json` in project directory
4. `~/.oddsockets/config.json` in home directory

## Pricing

**7-day free trial on every plan.** Card required (secure Stripe checkout), nothing charged during the trial — cancel before it ends and you pay nothing. Agents and the CLI get a **48-hour keyless window** to prototype before a key is needed. Plans from $29/mo. [Details](https://oddsockets.com/#pricing).

## SDKs

Prefer to build it into your app? OddSockets ships a native SDK for every major language and runtime — same real-time channels, pub/sub, and presence, idiomatic to each stack.

<table>
<tr>
<td align="center" width="20%"><a href="https://github.com/jyswee/oddsockets-nodejs-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_nodejs.png" width="44" height="44" alt="Node.js"><br>Node.js</a></td>
<td align="center" width="20%"><a href="https://github.com/jyswee/oddsockets-javascript-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_javascript.png" width="44" height="44" alt="JavaScript"><br>JavaScript</a></td>
<td align="center" width="20%"><a href="https://github.com/jyswee/oddsockets-svelte-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_svelte.png" width="44" height="44" alt="Svelte"><br>Svelte</a></td>
<td align="center" width="20%"><a href="https://github.com/jyswee/oddsockets-react-native-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_react.png" width="44" height="44" alt="React Native"><br>React Native</a></td>
<td align="center" width="20%"><a href="https://github.com/jyswee/oddsockets-flutter-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_flutter.png" width="44" height="44" alt="Flutter"><br>Flutter</a></td>
</tr>
<tr>
<td align="center"><a href="https://github.com/jyswee/oddsockets-python-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_python.png" width="44" height="44" alt="Python"><br>Python</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-go-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_go.png" width="44" height="44" alt="Go"><br>Go</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-rust-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_rust.png" width="44" height="44" alt="Rust"><br>Rust</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-java-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_java.png" width="44" height="44" alt="Java"><br>Java</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-kotlin-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_kotlin.png" width="44" height="44" alt="Kotlin"><br>Kotlin</a></td>
</tr>
<tr>
<td align="center"><a href="https://github.com/jyswee/oddsockets-csharp-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_csharp.png" width="44" height="44" alt="C#"><br>C# / .NET</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-cpp-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_cpp.png" width="44" height="44" alt="C++"><br>C++</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-c-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_c.png" width="44" height="44" alt="C"><br>C</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-php-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_php.png" width="44" height="44" alt="PHP"><br>PHP</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-ruby-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_ruby.png" width="44" height="44" alt="Ruby"><br>Ruby</a></td>
</tr>
<tr>
<td align="center"><a href="https://github.com/jyswee/oddsockets-swift-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_swift.png" width="44" height="44" alt="Swift"><br>Swift</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-elixir-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_elixir.png" width="44" height="44" alt="Elixir"><br>Elixir</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-unity-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_unity.png" width="44" height="44" alt="Unity"><br>Unity</a></td>
<td align="center"><a href="https://github.com/jyswee/oddsockets-unrealengine-sdk"><img src="https://prodmedia.tyga.host/public/tyga.cloud/landing/oddsockets.com/platform_unrealengine.png" width="44" height="44" alt="Unreal Engine"><br>Unreal Engine</a></td>
<td align="center"></td>
</tr>
</table>

<details>
<summary><strong>Full SDK list with highlights</strong></summary>

| Language / Runtime | Repo | Highlights |
|--------------------|------|------------|
| Node.js | [oddsockets-nodejs-sdk](https://github.com/jyswee/oddsockets-nodejs-sdk) | Server-side, npm |
| JavaScript | [oddsockets-javascript-sdk](https://github.com/jyswee/oddsockets-javascript-sdk) | Browser + Node.js |
| TypeScript / Svelte | [oddsockets-svelte-sdk](https://github.com/jyswee/oddsockets-svelte-sdk) | Reactive stores |
| React Native | [oddsockets-react-native-sdk](https://github.com/jyswee/oddsockets-react-native-sdk) | Mobile |
| Flutter / Dart | [oddsockets-flutter-sdk](https://github.com/jyswee/oddsockets-flutter-sdk) | Cross-platform mobile |
| Python | [oddsockets-python-sdk](https://github.com/jyswee/oddsockets-python-sdk) | AsyncIO |
| Go | [oddsockets-go-sdk](https://github.com/jyswee/oddsockets-go-sdk) | Goroutine-safe |
| Rust | [oddsockets-rust-sdk](https://github.com/jyswee/oddsockets-rust-sdk) | Tokio async |
| Java | [oddsockets-java-sdk](https://github.com/jyswee/oddsockets-java-sdk) | Maven |
| Kotlin | [oddsockets-kotlin-sdk](https://github.com/jyswee/oddsockets-kotlin-sdk) | Coroutines |
| C# / .NET | [oddsockets-csharp-sdk](https://github.com/jyswee/oddsockets-csharp-sdk) | NuGet |
| C++ | [oddsockets-cpp-sdk](https://github.com/jyswee/oddsockets-cpp-sdk) | C++17 |
| C | [oddsockets-c-sdk](https://github.com/jyswee/oddsockets-c-sdk) | Embedded / IoT |
| PHP | [oddsockets-php-sdk](https://github.com/jyswee/oddsockets-php-sdk) | Composer |
| Ruby | [oddsockets-ruby-sdk](https://github.com/jyswee/oddsockets-ruby-sdk) | Gem |
| Swift | [oddsockets-swift-sdk](https://github.com/jyswee/oddsockets-swift-sdk) | SPM + Combine |
| Elixir | [oddsockets-elixir-sdk](https://github.com/jyswee/oddsockets-elixir-sdk) | GenServer / OTP |
| Unity | [oddsockets-unity-sdk](https://github.com/jyswee/oddsockets-unity-sdk) | MonoBehaviour |
| Unreal Engine | [oddsockets-unrealengine-sdk](https://github.com/jyswee/oddsockets-unrealengine-sdk) | UE5 |

</details>

## Links

- [Documentation](https://docs.oddsockets.com)
- [Dashboard](https://oddsockets.com/developer-dashboard)
- [GitHub](https://github.com/jyswee)
