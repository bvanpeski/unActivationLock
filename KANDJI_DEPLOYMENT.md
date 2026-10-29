# Kandji Deployment Guide — unActivationLock

Settings for deploying `unActivationLock.zsh` as a Kandji Custom Script, plus the
logo file dependency. This script prompts the Find My user to disable Find My Mac
so Kandji can collect an Activation Lock bypass code and apply the *Disallow
Activation Lock* state on already-enrolled Macs.

## Library Item: Custom Script

| Field | Value |
|---|---|
| **Type** | Custom Script |
| **Name** | `unActivationLock – Find My Prompt` |
| **Category** | Security (or your org's convention) |
| **Execution Frequency** | **Every 15 Minutes** |
| **Show in Self Service** | Off |
| **Audit Script** | *paste full `unActivationLock.zsh`* |
| **Remediation Script** | *leave empty* |

**Script field:** paste the entire contents of `unActivationLock.zsh`. Keep line 1
`#!/bin/zsh` — that is what makes Kandji run it as zsh (the #1 failure mode is it
running as bash). No remediation script is needed; the tool handles its own
prompting loop and exits cleanly.

> Kandji audit scripts act on exit codes. This script exits `0` on success/clean
> states and `1` on "needs attention" states, which Kandji surfaces as a
> non-compliant/attention status on the device — useful for spotting Macs still
> stuck in Activation Lock.

## Dependency Library Item: Logo file

Deploy the icon **before** the script so the dialog shows your branding. The
script references `/Library/Kandji/logo.png`; if the file is missing at runtime
the dialog still fires, just without the icon (handled by the `iconCMD` logic in
`UserDialog`).

| Field | Value |
|---|---|
| **Type** | Custom App → **Deploy file** (or a Script that writes it) |
| **Destination** | `/Library/Kandji/logo.png` |
| **Permissions** | `644`, owner `root:wheel` |
| **Assignment** | same Blueprint as the script |

## Blueprint / Scoping

1. Create or pick a **test Blueprint** with just 1–2 devices.
2. Add **both** Library items (logo file + script) to it.
3. Order the logo deployment ahead of the script where possible; if it lands a
   cycle late, the dialog still fires without the icon (by design).
4. After validation, add the items to your production Blueprint(s).

## Config values set in the script (top block)

- `dialogTitle="Action Required: Turn Off Find My Mac"`
- `dialogMessage=` flattened single-paragraph version (renders cleanly in
  `kandji display-alert`)
- `appIcon="/Library/Kandji/logo.png"`
- `attempts=6`, `wait_time=40` — 6 prompts, 40s apart per run
- `DisallowFindMy=false` — only prompts when user-based Activation Lock is
  actually detected. Set to `true` to always prompt any user who has Find My on,
  regardless of lock status.

## Verify after assignment

On the test Mac:

```
sudo kandji run
log show --style compact --process "logger" | grep "UnActivationLock"
```

Then check the device record in Kandji for a collected **bypass code** and the
*Disallow Activation Lock* state.

### Common test gotchas

- **"not the user associated with the Activation Lock"** in the log → you are
  signed in as the wrong account. Log in as the iCloud user that locked the device.
- **No logo in the dialog** → `logo.png` has not reached `/Library/Kandji/` yet.
- **Script appears to do nothing / runs as bash errors** → confirm the Library
  item is running the script with the `#!/bin/zsh` shebang intact.
