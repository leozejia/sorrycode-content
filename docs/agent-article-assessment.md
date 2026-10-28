# Agent 旧文档评估

评估范围为 `d85e4f1^` 的 17 篇 `runtime` 文章，结论服务于当前栏目，不代表所有客户端链路已实测。

| 原文 | 处理 | 原因与保留的差异 |
| --- | --- | --- |
| Magpie | 保留 | 统一供应商与模型配置，保留截图。 |
| Codex | 合并 | 保留桌面安装、完整退出和工作目录；供应商配置不重复。 |
| Claude Code | 合并 | 保留官方按系统安装、终端 `claude`，区分 Claude Desktop。旧脚本与手改配置不作为默认。 |
| DSH | 合并 | 保留桌面安装、模型与工作区选择。旧 Web UI / Node 启动不是桌面版前置。 |
| WorkBuddy | 合并 | 保留登录、客户端版本、应用内模型选择和文件授权。旧手动字段未重新验证，不冒充 Magpie 设置。 |
| OpenCode | 合并 | 保留官网入口。旧 Desktop 手动提供商字段及能力未复测，暂不恢复成已验证流程。 |
| Pi Agent | 合并 | 保留官网入口；旧手写模型目录和硬编码能力会过期，不作为默认。 |
| Kimi Code | 合并 | 保留官方入口；旧手写 provider 路线未复测，不当成当前事实。 |
| Grok Build | 合并 | 保留官方入口；文字模型接入不等于图片和视频工具接入。 |
| Cursor | 单独保留 | Magpie 本机面板未显示 Cursor；恢复旧编辑器手动步骤供参考，明确未复测，与 CLI / Private Inference 分开。 |
| Claude Desktop | 合并入口 | 和 Claude Code 是不同客户端，本机 Magpie 显示独立入口；历史 Gateway 手动步骤及系统差异未复测，不恢复为已验证流程。 |
| Claude Fable 5 | 删除 | 型号专篇不是接入前置，型号选择以当前目录为准。 |
| Agent 能力是怎么扩展的 | 删除 | Skills 核心概念已有说明，避免重复。 |
| GPT Image 2 | 删除 | 不再维护独立模型/API 教程，图像能力不能由模型接入推断。 |
| GPT Image 2.5 | 删除 | 同上。 |
| Grok 图片 | 删除 | 不再维护独立媒体 API 教程。 |
| Grok 视频 | 删除 | 同上。 |

2026-10-28 只读检查：本机 Magpie 0.1.1793 显示 Codex、Claude Code、DeepSeek Harness、WorkBuddy、Claude Desktop 等入口，以及 OpenCode、Pi 的安装项；未在当前面板看到 Cursor。该观察不证明每个客户端或 Windows 上的实际模型调用成功，也不证明未来版本永不支持 Cursor。旧的直接接入步骤保存在 Git 历史中；未来需要恢复时，应先以目标客户端版本与 SorryCode 实测。
