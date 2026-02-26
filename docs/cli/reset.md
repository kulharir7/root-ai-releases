---
summary: "CLI reference for `Root reset` (reset local state/config)"
read_when:
  - You want to wipe local state while keeping the CLI installed
  - You want a dry-run of what would be removed
title: "reset"
---

# `Root reset`

Reset local config/state (keeps the CLI installed).

```bash
Root reset
Root reset --dry-run
Root reset --scope config+creds+sessions --yes --non-interactive
```
