---
summary: "CLI reference for `Root voicecall` (voice-call plugin command surface)"
read_when:
  - You use the voice-call plugin and want the CLI entry points
  - You want quick examples for `voicecall call|continue|status|tail|expose`
title: "voicecall"
---

# `Root voicecall`

`voicecall` is a plugin-provided command. It only appears if the voice-call plugin is installed and enabled.

Primary doc:

- Voice-call plugin: [Voice Call](/plugins/voice-call)

## Common commands

```bash
Root voicecall status --call-id <id>
Root voicecall call --to "+15555550123" --message "Hello" --mode notify
Root voicecall continue --call-id <id> --message "Any questions?"
Root voicecall end --call-id <id>
```

## Exposing webhooks (Tailscale)

```bash
Root voicecall expose --mode serve
Root voicecall expose --mode funnel
Root voicecall unexpose
```

Security note: only expose the webhook endpoint to networks you trust. Prefer Tailscale Serve over Funnel when possible.
