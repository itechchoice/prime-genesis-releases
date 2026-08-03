# Changelog

Release history for the AgentTeam installers distributed from this repository (newest first).

## v0.7.1 — Nexus gateway build (first release in this repo)

**Platforms**: macOS arm64 (`.dmg`) · Windows 11 x64 (`.exe`, cross-compiled)

**Highlights**:
- **Nexus-only gateway**: all LLM traffic is routed through the company Nexus gateway (OpenAI-compatible);
  no longer depends on individual Anthropic / OpenAI / Google keys. Auxiliary calls (judge, PDF extraction,
  plan orchestration) all go through the gateway too.
- **Works out of the box**: the gateway URL + access key are baked in, so no manual API key entry is needed
  (internal distribution only; the baked key is extractable — see the security notice in the README).
- **Structured-output gateway compatibility fix**: the gateway (proxying Anthropic) does not support
  `json_schema`, so it is downgraded to `json_object` (schema constraints are enforced via prompt injection
  + client-side validation). Judge / plan / intent-classification structured outputs work correctly.
- **Cold-start blank-screen fix**: fixed a first-render crash `Cannot read null (useMemo)` caused by a
  dangling React instance in `@heroui-pro/react` during Vite cold-start dep optimization (renderer dedupe
  React + pinned heroui optimize).

**Known limitations**:
- Both installers are **unsigned** (macOS ad-hoc / Windows unsigned); the first launch must pass
  Gatekeeper / SmartScreen (see README).
- macOS is arm64 only.
- The Windows build is a cross-compiled artifact, **not fully tested on real Windows 11 hardware**; the
  macOS-only subsystems (PDF sandbox-runtime, browser oracle) are excluded from the Windows package.
- Modality tools (image / video / voiceover / speech-to-text) still call vendor REST APIs directly and do
  not go through the gateway.
