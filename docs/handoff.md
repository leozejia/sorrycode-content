# SorryCode Content Handoff

更新时间：2026-08-27

## Agent Runtime 收录

### Google

- Google 已将普通用户的主要终端入口迁移到 Antigravity CLI。Gemini CLI 继续面向企业许可证和付费 API Key 场景。
- 截至 `sub2api v0.1.183`，上游“接入工具”仍然生成 Gemini CLI 配置。上游的 `antigravity` 指服务端 provider 路由，不是 Antigravity CLI。
- Antigravity CLI 官方已经支持 Gemini API Key 和自定义 Gemini Base URL，但 SorryCode 尚未完成实际调用验证。

当前不改公开文档、导航和接入工具，也不新增 Gemini CLI 或 Antigravity CLI 页面。

下次推进 Google runtime 时，先询问是否要把 Antigravity CLI 作为主入口，再重新核对上游实现、Google 官方迁移状态和自定义端点支持。只有用 SorryCode Gemini 分组 Key 跑通模型请求和工具调用后，才进入公开文档。

### 国内办公 Agent

- Qwen Code 暂不进入内容队列。
- Qwen Work 值得持续关注，但官方帮助中心当前只提供内置模型和 Credits 体系，系统设置没有自定义模型、API Key 或 Base URL。现在不写 SorryCode 接入文档。
- Cline 和 Roo Code 不进入当前内容范围。

下次调整办公 Agent 或模型与工作台栏目时，主动询问是否重新检查 Qwen Work。若官方仍未开放自定义模型入口，继续只观察，不新增页面。
