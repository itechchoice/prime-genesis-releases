# Prime Genesis — Preview channel

Pre-release builds of the **Prime Genesis** desktop app for early testing. **Preview builds may be
unstable.** For day-to-day use, get the Stable channel instead → [`../stable/`](../stable/).

Preview installers are published as **GitHub Pre-releases** (badged *Pre-release*, never *Latest*)
under the app's going-forward name, **`Prime-Genesis`**. (The current stable build still uses the app's
former name, `AgentTeam` — see the [top-level README](../README.md); it's the same app, mid-rename.)
Because the two use different bundle names, a preview install sits **side by side** with an existing
`AgentTeam` install without overwriting it.

## Download

Go to [Releases](https://github.com/itechchoice/prime-genesis-releases/releases) and pick a release
tagged `vX.Y.Z-preview.N`:

| Platform | File | Notes |
|---|---|---|
| macOS (Apple Silicon / M-series) | `Prime-Genesis-<version>-arm64.dmg` | **arm64 only** — Intel Macs are not supported |
| Windows 11 (x64) | `Prime-Genesis-<version>-x64-setup.exe` | NSIS installer |
| Windows 11 (x64) | `Prime-Genesis-<version>-win.zip` | Portable archive |

> Every preview release ships a `v<version>.sha256`. Verify integrity after downloading.

## Install

### macOS
The installer is **unsigned / not notarized**, so Gatekeeper will block the first launch. Either:
- Right-click the app → **Open** → click **Open** again in the dialog; or
- Run in Terminal: `xattr -dr com.apple.quarantine /Applications/Prime-Genesis.app`

### Windows 11
The installer is **unsigned**, so SmartScreen will warn on first run → **More info** → **Run anyway**.

## First launch

The preview ships with staging service addresses configured, but **does not contain shared API keys**.
Sign in so the gateway can issue your own credential. If an upgrade stops authenticating, sign out and
back in.

> Modality features (image / video / voiceover / speech-to-text) call vendor REST APIs directly and do
> not go through the chat gateway; those still require the corresponding vendor key.
> The Windows build excludes the macOS-only subsystems (PDF sandbox, browser oracle) — only the
> chat / agent / LLM core is available there.

## Verify integrity

```bash
# macOS
shasum -a 256 -c checksums/v0.8.0-preview.1.sha256
# Windows (PowerShell)
Get-FileHash Prime-Genesis-0.8.0-preview.1-x64-setup.exe -Algorithm SHA256
```
