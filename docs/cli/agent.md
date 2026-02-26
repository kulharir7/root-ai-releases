---
summary: "CLI reference for `Korvus agent` (send one agent turn via the Gateway)"
read_when:
  - You want to run one agent turn from scripts (optionally deliver reply)
title: "agent"
---

# `Korvus agent`

Run an agent turn via the Gateway (use `--local` for embedded).
Use `--agent <id>` to target a configured agent directly.

Related:

- Agent send tool: [Agent send](/tools/agent-send)

## Examples

```bash
Korvus agent --to +15555550123 --message "status update" --deliver
Korvus agent --agent ops --message "Summarize logs"
Korvus agent --session-id 1234 --message "Summarize inbox" --thinking medium
Korvus agent --agent ops --message "Generate report" --deliver --reply-channel slack --reply-to "#reports"
```
