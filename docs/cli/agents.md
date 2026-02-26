---
summary: "CLI reference for `Root agents` (list/add/delete/set identity)"
read_when:
  - You want multiple isolated agents (workspaces + routing + auth)
title: "agents"
---

# `Root agents`

Manage isolated agents (workspaces + auth + routing).

Related:

- Multi-agent routing: [Multi-Agent Routing](/concepts/multi-agent)
- Agent workspace: [Agent workspace](/concepts/agent-workspace)

## Examples

```bash
Root agents list
Root agents add work --workspace ~/.Root/workspace-work
Root agents set-identity --workspace ~/.Root/workspace --from-identity
Root agents set-identity --agent main --avatar avatars/Root.png
Root agents delete work
```

## Identity files

Each agent workspace can include an `IDENTITY.md` at the workspace root:

- Example path: `~/.Root/workspace/IDENTITY.md`
- `set-identity --from-identity` reads from the workspace root (or an explicit `--identity-file`)

Avatar paths resolve relative to the workspace root.

## Set identity

`set-identity` writes fields into `agents.list[].identity`:

- `name`
- `theme`
- `emoji`
- `avatar` (workspace-relative path, http(s) URL, or data URI)

Load from `IDENTITY.md`:

```bash
Root agents set-identity --workspace ~/.Root/workspace --from-identity
```

Override fields explicitly:

```bash
Root agents set-identity --agent main --name "Root" --emoji "🦞" --avatar avatars/Root.png
```

Config sample:

```json5
{
  agents: {
    list: [
      {
        id: "main",
        identity: {
          name: "Root",
          theme: "space lobster",
          emoji: "🦞",
          avatar: "avatars/Root.png",
        },
      },
    ],
  },
}
```
