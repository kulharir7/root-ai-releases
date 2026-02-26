---
summary: "CLI reference for `Korvus channels` (accounts, status, login/logout, logs)"
read_when:
  - You want to add/remove channel accounts (WhatsApp/Telegram/Discord/Google Chat/Slack/Mattermost (plugin)/Signal/iMessage)
  - You want to check channel status or tail channel logs
title: "channels"
---

# `Korvus channels`

Manage chat channel accounts and their runtime status on the Gateway.

Related docs:

- Channel guides: [Channels](/channels/index)
- Gateway configuration: [Configuration](/gateway/configuration)

## Common commands

```bash
Korvus channels list
Korvus channels status
Korvus channels capabilities
Korvus channels capabilities --channel discord --target channel:123
Korvus channels resolve --channel slack "#general" "@jane"
Korvus channels logs --channel all
```

## Add / remove accounts

```bash
Korvus channels add --channel telegram --token <bot-token>
Korvus channels remove --channel telegram --delete
```

Tip: `Korvus channels add --help` shows per-channel flags (token, app token, signal-cli paths, etc).

## Login / logout (interactive)

```bash
Korvus channels login --channel whatsapp
Korvus channels logout --channel whatsapp
```

## Troubleshooting

- Run `Korvus status --deep` for a broad probe.
- Use `Korvus doctor` for guided fixes.
- `Korvus channels list` prints `Claude: HTTP 403 ... user:profile` → usage snapshot needs the `user:profile` scope. Use `--no-usage`, or provide a claude.ai session key (`CLAUDE_WEB_SESSION_KEY` / `CLAUDE_WEB_COOKIE`), or re-auth via Claude Code CLI.

## Capabilities probe

Fetch provider capability hints (intents/scopes where available) plus static feature support:

```bash
Korvus channels capabilities
Korvus channels capabilities --channel discord --target channel:123
```

Notes:

- `--channel` is optional; omit it to list every channel (including extensions).
- `--target` accepts `channel:<id>` or a raw numeric channel id and only applies to Discord.
- Probes are provider-specific: Discord intents + optional channel permissions; Slack bot + user scopes; Telegram bot flags + webhook; Signal daemon version; MS Teams app token + Graph roles/scopes (annotated where known). Channels without probes report `Probe: unavailable`.

## Resolve names to IDs

Resolve channel/user names to IDs using the provider directory:

```bash
Korvus channels resolve --channel slack "#general" "@jane"
Korvus channels resolve --channel discord "My Server/#support" "@someone"
Korvus channels resolve --channel matrix "Project Room"
```

Notes:

- Use `--kind user|group|auto` to force the target type.
- Resolution prefers active matches when multiple entries share the same name.
