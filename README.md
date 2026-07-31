# Prime Genesis — AgentTeam 安装包分发

AgentTeam 桌面应用(macOS + Windows)的安装包分发仓库。**安装包不放在 git 里**,统一走
[**Releases**](https://github.com/itechchoice/prime-genesis-releases/releases) 下载——本仓库只维护
说明、更新日志与校验和。

## 下载

到 [Releases](https://github.com/itechchoice/prime-genesis-releases/releases) 选对应平台:

| 平台 | 文件 | 说明 |
|---|---|---|
| macOS（Apple Silicon / M 系列） | `AgentTeam-<版本>-arm64.dmg` | **仅 arm64**，Intel Mac 不支持 |
| Windows 11（x64） | `AgentTeam-<版本>-x64-setup.exe` | NSIS 安装向导 |

> 每个 Release 附 `<版本>.sha256`，下载后建议核验完整性（见下）。

## 安装

### macOS
安装包**未签名/未公证**，首次打开会被 Gatekeeper 拦。二选一：
- 右键 App →「打开」→ 在弹窗里再点「打开」；或
- 终端执行:`xattr -dr com.apple.quarantine /Applications/AgentTeam.app`

### Windows 11
安装包**未签名**,首次运行 SmartScreen 提示 →「更多信息」→「仍要运行」。

## 首次启动

本分发版**已内置公司 Nexus 网关配置(网关地址 + 访问 key)**,装完开箱即用、无需手填 API key。
所有 LLM 流量经 Nexus 网关转发,不依赖各厂商(Anthropic / OpenAI / Google)独立 key。

> 模态功能(图片 / 视频 / 配音 / 语音转写)走各厂商 REST,不经聊天网关;如需这些功能仍需对应厂商 key。
> Windows 版不含 macOS 专属子系统(PDF sandbox、浏览器 oracle),仅聊天 / agent / LLM 主链路可用。

## 校验完整性

```bash
# macOS
shasum -a 256 -c v0.7.1.sha256
# Windows (PowerShell)
Get-FileHash AgentTeam-0.7.1-x64-setup.exe -Algorithm SHA256
```

## ⚠️ 安全须知(内部分发)

- 本仓库**私有**,安装包内**内置了 Nexus 网关 key**——任何能访问本仓库/安装包的人都能提取该 key。
  请将协作者范围控制到最小;若 key 疑似泄露,到网关侧**轮换该 key**。
- **切勿把本仓库转为公开、或把安装包外发给外部客户**。对外分发需改用不内置 key 的 BYO 构建。

## 版本

见 [CHANGELOG.md](./CHANGELOG.md)。已发布的版本 tag 视为不可变;新改动一律递增版本号重发,便于回滚。
