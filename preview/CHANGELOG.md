# Changelog — Preview channel

Pre-release build history (newest first). Preview builds are published as GitHub Pre-releases and may
be unstable. Stable history lives in [`../stable/CHANGELOG.md`](../stable/CHANGELOG.md).

## v0.7.2-preview

**Product name**: `Prime-Genesis` (installs side by side with the Stable `AgentTeam` build)

**Platforms**: macOS arm64 (`.dmg`) · Windows 11 x64 (`.exe`, cross-compiled)

**Base**: builds on the Stable v0.7.1 Nexus gateway build — all LLM traffic routed through the company
Nexus gateway, gateway URL + access key baked in (internal distribution only; the baked key is
extractable — see the security notice in the top-level README).

**Known limitations**:
- **Preview / pre-release build — may be unstable.** Not for day-to-day use; prefer the Stable channel.
- Both installers are **unsigned** (macOS ad-hoc / Windows unsigned); the first launch must pass
  Gatekeeper / SmartScreen (see the preview README).
- macOS is arm64 only.
- The Windows build is a cross-compiled artifact, **not fully tested on real Windows 11 hardware**; the
  macOS-only subsystems (PDF sandbox-runtime, browser oracle) are excluded from the Windows package.
- Modality tools (image / video / voiceover / speech-to-text) still call vendor REST APIs directly and
  do not go through the gateway.
