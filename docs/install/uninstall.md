---
summary: "Uninstall Root completely (CLI, service, state, workspace)"
read_when:
  - You want to remove Root from a machine
  - The gateway service is still running after uninstall
title: "Uninstall"
---

# Uninstall

Two paths:

- **Easy path** if `Root` is still installed.
- **Manual service removal** if the CLI is gone but the service is still running.

## Easy path (CLI still installed)

Recommended: use the built-in uninstaller:

```bash
Root uninstall
```

Non-interactive (automation / npx):

```bash
Root uninstall --all --yes --non-interactive
npx -y Root uninstall --all --yes --non-interactive
```

Manual steps (same result):

1. Stop the gateway service:

```bash
Root gateway stop
```

2. Uninstall the gateway service (launchd/systemd/schtasks):

```bash
Root gateway uninstall
```

3. Delete state + config:

```bash
rm -rf "${Root_STATE_DIR:-$HOME/.Root}"
```

If you set `Root_CONFIG_PATH` to a custom location outside the state dir, delete that file too.

4. Delete your workspace (optional, removes agent files):

```bash
rm -rf ~/.Root/workspace
```

5. Remove the CLI install (pick the one you used):

```bash
npm rm -g Root
pnpm remove -g Root
bun remove -g Root
```

6. If you installed the macOS app:

```bash
rm -rf /Applications/Root.app
```

Notes:

- If you used profiles (`--profile` / `Root_PROFILE`), repeat step 3 for each state dir (defaults are `~/.Root-<profile>`).
- In remote mode, the state dir lives on the **gateway host**, so run steps 1-4 there too.

## Manual service removal (CLI not installed)

Use this if the gateway service keeps running but `Root` is missing.

### macOS (launchd)

Default label is `bot.molt.gateway` (or `bot.molt.<profile>`; legacy `com.Root.*` may still exist):

```bash
launchctl bootout gui/$UID/bot.molt.gateway
rm -f ~/Library/LaunchAgents/bot.molt.gateway.plist
```

If you used a profile, replace the label and plist name with `bot.molt.<profile>`. Remove any legacy `com.Root.*` plists if present.

### Linux (systemd user unit)

Default unit name is `Root-gateway.service` (or `Root-gateway-<profile>.service`):

```bash
systemctl --user disable --now Root-gateway.service
rm -f ~/.config/systemd/user/Root-gateway.service
systemctl --user daemon-reload
```

### Windows (Scheduled Task)

Default task name is `Root Gateway` (or `Root Gateway (<profile>)`).
The task script lives under your state dir.

```powershell
schtasks /Delete /F /TN "Root Gateway"
Remove-Item -Force "$env:USERPROFILE\.Root\gateway.cmd"
```

If you used a profile, delete the matching task name and `~\.Root-<profile>\gateway.cmd`.

## Normal install vs source checkout

### Normal install (install.sh / npm / pnpm / bun)

If you used `https://Root.ai/install.sh` or `install.ps1`, the CLI was installed with `npm install -g Root@latest`.
Remove it with `npm rm -g Root` (or `pnpm remove -g` / `bun remove -g` if you installed that way).

### Source checkout (git clone)

If you run from a repo checkout (`git clone` + `Root ...` / `bun run Root ...`):

1. Uninstall the gateway service **before** deleting the repo (use the easy path above or manual service removal).
2. Delete the repo directory.
3. Remove state + workspace as shown above.
