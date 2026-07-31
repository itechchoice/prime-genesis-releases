# Changelog

本仓库分发的 AgentTeam 安装包版本记录(最新在上)。

## v0.7.1 — Nexus 网关版（本仓库首个发布）

**平台**:macOS arm64（`.dmg`）· Windows 11 x64（`.exe`,交叉编译)

**要点**:
- **Nexus-only 网关**:全部 LLM 流量经公司 Nexus 网关(OpenAI 兼容)转发,不再依赖
  Anthropic / OpenAI / Google 独立 key;judge / PDF 抽取 / 计划编排等辅助调用统一走网关。
- **开箱即用**:内置 Nexus 网关地址 + 访问 key,装完无需手填(内部分发用;含可提取 key,见 README 安全须知)。
- **网关结构化输出兼容修复**:网关代理 Anthropic 时不支持 `json_schema`,已降级为 `json_object`
  (schema 约束改由 prompt 注入 + 客户端校验保证),judge / plan / 意图分类等结构化输出正常。
- **冷启动白屏修复**:修 Vite 冷启动时 `@heroui-pro/react` React 实例悬空导致的
  `Cannot read null (useMemo)` 首渲染崩溃(renderer dedupe React + 钉住 heroui optimize)。

**已知边界**:
- 两个包均**未签名**(macOS ad-hoc / Windows 未签),首次打开需过 Gatekeeper / SmartScreen(见 README)。
- macOS 仅 arm64。
- Windows 为交叉编译产物,**未在真机 Windows 11 上完整实测**;macOS 专属子系统
  (PDF sandbox-runtime、浏览器 oracle)在 Windows 包中已排除。
- 模态工具(图片 / 视频 / 配音 / 语音转写)仍走各厂商 REST,不经网关。
