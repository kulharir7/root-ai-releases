---
summary: "CLI reference for `Korvus config` (get/set/unset config values)"
read_when:
  - You want to read or edit config non-interactively
title: "config"
---

# `Korvus config`

Config helpers: get/set/unset values by path. Run without a subcommand to open
the configure wizard (same as `Korvus configure`).

## Examples

```bash
Korvus config get browser.executablePath
Korvus config set browser.executablePath "/usr/bin/google-chrome"
Korvus config set agents.defaults.heartbeat.every "2h"
Korvus config set agents.list[0].tools.exec.node "node-id-or-name"
Korvus config unset tools.web.search.apiKey
```

## Paths

Paths use dot or bracket notation:

```bash
Korvus config get agents.defaults.workspace
Korvus config get agents.list[0].id
```

Use the agent list index to target a specific agent:

```bash
Korvus config get agents.list
Korvus config set agents.list[1].tools.exec.node "node-id-or-name"
```

## Values

Values are parsed as JSON5 when possible; otherwise they are treated as strings.
Use `--json` to require JSON5 parsing.

```bash
Korvus config set agents.defaults.heartbeat.every "0m"
Korvus config set gateway.port 19001 --json
Korvus config set channels.whatsapp.groups '["*"]' --json
```

Restart the gateway after edits.
