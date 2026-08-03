# Prime Genesis — Preview channel

Pre-release builds of the desktop app for early testing. **Preview builds may be unstable.** For
day-to-day use, get the Stable channel instead → [`../stable/`](../stable/).

Preview installers are published as **GitHub Pre-releases** (badged *Pre-release*, never *Latest*) and
carry the product name **`Prime-Genesis`**, so a preview install sits **side by side** with a Stable
`AgentTeam` install — they do not overwrite each other.

## Download

Go to [Releases](https://github.com/itechchoice/prime-genesis-releases/releases) and pick the release
tagged `…-preview`:

| Platform | File | Notes |
|---|---|---|
| macOS (Apple Silicon / M-series) | `Prime-Genesis-<version>-preview-arm64.dmg` | **arm64 only** — Intel Macs are not supported |
| Windows 11 (x64) | `Prime-Genesis-<version>-preview-x64-setup.exe` | NSIS installer |

> Every preview release ships a `<version>-preview.sha256`. Verify integrity after downloading.

## Install

### macOS
The installer is **unsigned / not notarized**, so Gatekeeper will block the first launch. Either:
- Right-click the app → **Open** → click **Open** again in the dialog; or
- Run in Terminal: `xattr -dr com.apple.quarantine /Applications/Prime-Genesis.app`

### Windows 11
The installer is **unsigned**, so SmartScreen will warn on first run → **More info** → **Run anyway**.

## First launch

Like the Stable build, the preview **ships with the company Nexus gateway pre-configured (gateway URL +
access key)** and works out of the box — no API key entry required. All LLM traffic is routed through
the Nexus gateway. See the security notice in the [top-level README](../README.md) — the baked key is
extractable, so this is internal distribution only.

> Modality features (image / video / voiceover / speech-to-text) call vendor REST APIs directly and do
> not go through the chat gateway; those still require the corresponding vendor key.
> The Windows build excludes the macOS-only subsystems (PDF sandbox, browser oracle) — only the
> chat / agent / LLM core is available there.

## Verify integrity

```bash
# macOS
shasum -a 256 -c checksums/v0.7.2-preview.sha256
# Windows (PowerShell)
Get-FileHash Prime-Genesis-0.7.2-preview-x64-setup.exe -Algorithm SHA256
```
