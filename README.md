# oddsockets

Agent-first CLI for [OddSockets](https://oddsockets.com) real-time messaging.

Signup, publish, subscribe, presence, API key management — all from the command line. Zero dependencies.

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

## Free Tier

- 100 MAU, 50 concurrent connections
- 10,000 messages/day, 10 channels
- 24h message history

## Links

- [Documentation](https://docs.oddsockets.com)
- [Dashboard](https://oddsockets.com/developer-dashboard)
- [GitHub](https://github.com/jyswee)
