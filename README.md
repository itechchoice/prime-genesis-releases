# Prime Genesis — Distribution

Distribution repository for the **Prime Genesis** desktop app (macOS + Windows). **Installers are not
stored in git** — they are attached to [**Releases**](https://github.com/itechchoice/prime-genesis-releases/releases).
This repository only tracks docs, changelogs, and checksums.

> ### Naming
> The app was previously distributed as **AgentTeam**. That name is being **retired in favor of
> Prime Genesis** — it is **one app, not two**. The only build that still carries the old `AgentTeam`
> name is the current stable release (**v0.7.1**). Every preview build, and every future release, uses
> **Prime Genesis**.

## Two channels (same app)

| Channel | Folder | GitHub release | Installer name today | For |
|---|---|---|---|---|
| **Stable** | [`stable/`](./stable/) | normal release, tagged `vX.Y.Z`, marked **Latest** | `AgentTeam-*` *(legacy name — v0.7.1)* | day-to-day use |
| **Preview** | [`preview/`](./preview/) | **pre-release**, tagged `vX.Y.Z-preview`, badged **Pre-release** (never *Latest*) | `Prime-Genesis-*` | early testing, may be unstable |

The two channels are the **same product** — they differ in **stability, not identity**. GitHub's own
**Latest vs Pre-release** distinction is the primary separator: anyone following the normal download
path always gets Stable; the Preview build only appears under the *Pre-release* badge.

> **Side-by-side install:** because the legacy `AgentTeam` build and the `Prime-Genesis` build use
> different bundle names, a Prime Genesis (preview) install sits **next to** an existing AgentTeam
> install without overwriting it. Once the stable channel also moves to Prime Genesis, a new release
> replaces the previous one in place (same name).

## Security notice

- This repository is **public**. Current preview installers contain service addresses but **no shared
  API keys**; users sign in for per-user gateway credentials and supply their own vendor keys where a
  modality tool requires one.
- Legacy artifacts may have embedded shared credentials. Treat any such credential as exposed and
  rotate it at the service. Never publish a new installer until its packaged resources have been
  checked for local or shared keys.

## Versions

Published version tags are treated as immutable; any new change gets a bumped version and a fresh
release, so older versions stay available for rollback. See each channel's changelog:
[stable](./stable/CHANGELOG.md) · [preview](./preview/CHANGELOG.md).
