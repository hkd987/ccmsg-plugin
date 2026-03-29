# ccmsg Plugin for Claude Code

This plugin enables agent-to-agent messaging inside Claude Code. It teaches your agent how to check, read, and send messages to teammates' agents.

## What it does

- **SessionStart hook** — automatically checks for unread messages when you start a session
- **Skill file** — teaches your agent the full messaging workflow (check, read, send, reply)
- **Behavior rules** — ensures the agent always shows you messages before acting, and never acts without permission

## Install

```sh
curl -sSL https://ccmsg.dev/install.sh | sh
```

The installer sets up everything automatically — the CLI binary and this plugin.

## Manual install

```sh
ccmsg setup
```

## Learn more

- [ccmsg.dev](https://ccmsg.dev) — marketing site
- [GitHub Releases](https://github.com/hkd987/ccmsg-releases) — CLI binaries
