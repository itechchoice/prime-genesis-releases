# Prime Genesis — AgentTeam Installers

Distribution repository for the AgentTeam desktop app (macOS + Windows). **Installers are not stored
in git** — download them from
[**Releases**](https://github.com/itechchoice/prime-genesis-releases/releases). This repository only
tracks the docs, changelog, and checksums.

## Download

Go to [Releases](https://github.com/itechchoice/prime-genesis-releases/releases) and pick your platform:

| Platform | File | Notes |
|---|---|---|
| macOS (Apple Silicon / M-series) | `AgentTeam-<version>-arm64.dmg` | **arm64 only** — Intel Macs are not supported |
| Windows 11 (x64) | `AgentTeam-<version>-x64-setup.exe` | NSIS installer |

> Every release ships a `<version>.sha256`. Verify integrity after downloading (see below).

## Install

### macOS
The installer is **unsigned / not notarized**, so Gatekeeper will block the first launch. Either:
- Right-click the app → **Open** → click **Open** again in the dialog; or
- Run in Terminal: `xattr -dr com.apple.quarantine /Applications/AgentTeam.app`

### Windows 11
The installer is **unsigned**, so SmartScreen will warn on first run → **More info** → **Run anyway**.

## First launch

This distribution build **ships with the company Nexus gateway pre-configured (gateway URL + access key)**,
so it works out of the box — no API key entry required. All LLM traffic is routed through the Nexus
gateway; it does not rely on individual vendor keys (Anthropic / OpenAI / Google).

> Modality features (image / video / voiceover / speech-to-text) call vendor REST APIs directly and do
> not go through the chat gateway; those still require the corresponding vendor key.
> The Windows build excludes the macOS-only subsystems (PDF sandbox, browser oracle) — only the
> chat / agent / LLM core is available there.

## Verify integrity

```bash
# macOS
shasum -a 256 -c v0.7.1.sha256
# Windows (PowerShell)
Get-FileHash AgentTeam-0.7.1-x64-setup.exe -Algorithm SHA256
```

## ⚠️ Security notice (internal distribution)

- This repository is **private**, and the installers have the **Nexus gateway key baked in** — anyone
  with access to this repo or the installers can extract that key. Keep the collaborator list minimal;
  if the key is suspected to have leaked, **rotate it on the gateway side**.
- **Do not make this repository public, and do not hand the installers to external customers.**
  External distribution requires a BYO build with no baked-in key.

## Versions

See [CHANGELOG.md](./CHANGELOG.md). Published version tags are treated as immutable; any new change gets
a bumped version and a fresh release, so older versions stay available for rollback.
