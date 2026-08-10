# Changelog — Preview channel

Pre-release build history (newest first). Preview builds are published as GitHub Pre-releases and may
be unstable. Stable history lives in [`../stable/CHANGELOG.md`](../stable/CHANGELOG.md).

## v0.7.2-preview.3

**Product name**: `Prime-Genesis` (installs side by side with the Stable `AgentTeam` build)

**Platforms**: macOS arm64 (`.dmg`) · Windows 11 x64 (`.exe` installer + portable `.zip`, cross-compiled)

**Base**: `develop` @ `92eea03` — 37 commits on top of the v0.7.2-preview.2 base (`573a3b6`). All LLM
traffic routed through the company Nexus gateway, gateway URL + access key baked in (internal
distribution only; the baked key is extractable — see the security notice in the top-level README).

**What changed since v0.7.2-preview.2**:
- **Tool-capability boundary + data provenance** — an agent's resolved tool surface is stated to it as an
  explicit capability boundary, and figures in a finished chat answer are checked against the turn's
  actual tool results, with untraceable ones disclosed.
- **Executor self-verification + engine-enforced repair round** — the protocol executor can run the
  project's own acceptance commands before handing in, and when platform verification fails the engine
  feeds the real failure output back for exactly one repair attempt before the judge sees it. The repair
  round is recorded on the signed ledger as `EXECUTOR_REPAIRED`; it never loops.
- **Built-in cases no longer declare the `claude-code` engine** — the product does not push users at an
  external CLI. The option stays selectable and honestly labelled (see Known limitations).
- **Windows-path fixes** — browser oracle usable on Windows dev, process tree fully reaped on smoke
  teardown (previously leaked a tree per server smoke), Windows SIGTERM semantics passed to the executor,
  and `claude.exe` resolution corrected.
- **Executor step timeout 120s → 600s** — the real cause of the "Aborted" family; multi-step tool loops
  were being starved. Transient stream drops are retried once and are distinguishable from a real timeout.
- **Stale-install self-heal** — built-in capability rows and agent default grants are reconciled against
  the code on every start, so upgrading an existing install no longer produces spurious capability-drift
  hard blocks or `NO_GRANT` denials.

**Known limitations**:
- **Preview / pre-release build — may be unstable.** Not for day-to-day use; prefer the Stable channel.
- Both installers are **unsigned** (macOS ad-hoc / Windows unsigned); the first launch must pass
  Gatekeeper / SmartScreen (see the preview README).
- macOS is arm64 only.
- The Windows build is a cross-compiled artifact and was **not tested on real Windows 11 hardware for
  this version**; the macOS-only subsystems (PDF sandbox-runtime, browser oracle) are excluded from the
  Windows package, so cases whose acceptance needs a browser judge cannot reach full green there.
- The `claude-code` execution engine stays selectable, but packaged builds do **not** ship the native
  `claude` binary and its traffic would not route through the Nexus gateway. Selecting it requires
  bringing your own `claude` CLI; the run form labels this.
- Modality tools (image / video / voiceover / speech-to-text) still call vendor REST APIs directly and
  do not go through the gateway.

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
