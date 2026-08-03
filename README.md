# Prime Genesis — Distribution

Distribution repository for the AgentTeam desktop app (macOS + Windows). **Installers are not stored
in git** — they are attached to [**Releases**](https://github.com/itechchoice/prime-genesis-releases/releases).
This repository only tracks docs, changelogs, and checksums.

## Two channels

| Channel | Folder | GitHub release | App name | For |
|---|---|---|---|---|
| **Stable** | [`stable/`](./stable/) | normal release, tagged `vX.Y.Z`, marked **Latest** | `AgentTeam` | day-to-day use |
| **Preview** | [`preview/`](./preview/) | **pre-release**, tagged `vX.Y.Z-preview`, badged **Pre-release** (never *Latest*) | `Prime-Genesis` | early testing, may be unstable |

Each channel has its own `README.md`, `CHANGELOG.md`, and `checksums/`. GitHub's own **Latest vs
Pre-release** distinction is the primary separator: anyone following the normal download path always
gets Stable — the Preview build only shows up under the *Pre-release* badge.

> The two builds use **different product names** (`AgentTeam` vs `Prime-Genesis`), so they install
> **side by side** without overwriting each other.

## ⚠️ Security notice (internal distribution)

- This repository is **private**, and the installers have the **Nexus gateway key baked in** — anyone
  with access to this repo or the installers can extract that key. Keep the collaborator list minimal;
  if the key is suspected to have leaked, **rotate it on the gateway side**.
- **Do not make this repository public, and do not hand the installers to external customers.**
  External distribution requires a BYO build with no baked-in key. This applies to **both** channels.

## Versions

Published version tags are treated as immutable; any new change gets a bumped version and a fresh
release, so older versions stay available for rollback. See each channel's changelog:
[stable](./stable/CHANGELOG.md) · [preview](./preview/CHANGELOG.md).
