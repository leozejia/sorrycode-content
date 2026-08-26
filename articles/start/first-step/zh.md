---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 先选适合的 Agent 工作台，再确认模型、协议和 API Key 分组兼容。
section: start
section_title: 开始使用
section_order: 1
---

# 第一次使用 SorryCode

第一次使用时，先选适合自己的 Agent 工作台，再按对应指南接入 SorryCode。工作台和模型是两回事，同一个工作台可以由不同模型驱动，具体取决于它使用的协议和 API Key 所属分组。

<h2 id="choose-tool">选择工作台</h2>

| 工作台 | 适合什么 | 接入指南 |
| --- | --- | --- |
| **ChatGPT / Codex** | 默认选择。适合代码、文件和本机任务，也有可视化 App | [ChatGPT / Codex](/docs/runtime/codex) |
| **Claude Code** | 适合代码、终端任务和长时间自主执行 | [Claude Code](/docs/runtime/claude-code) |
| **OpenCode** | 开源、多模型的 Agent，有桌面客户端和终端版 | [OpenCode](/docs/runtime/opencode) |
| **DSH** | DeepSeek 开源的 Web Agent，可以配置 Responses 兼容模型 | [DSH](/docs/runtime/dsh) |
| **Pi Agent** | 轻量、灵活的终端 Agent，可以自行配置 Responses 兼容模型 | [Pi Agent](/docs/runtime/pi-agent) |
| **Kimi Code** | 使用 Kimi 模型完成代码和长上下文任务 | [Kimi Code](/docs/runtime/kimi-code) |
| **WorkBuddy** | 在桌面界面处理文档、表格和本地文件 | [WorkBuddy](/docs/runtime/workbuddy) |
| **Grok Build** | 使用 Grok 模型和 xAI 生态能力 | [Grok Build](/docs/runtime/grok-build) |

不确定时先用 ChatGPT / Codex。想使用 Web UI 自行配置 Responses 模型，可以选择 DSH；想在开源工作台里使用多家模型，可以选择 OpenCode。

<h2 id="prepare-key">准备兼容的 API Key</h2>

登录 [SorryCode 控制台](https://sorrycode.com)，确认余额可用。选定模型后，检查 API Key 所属分组是否同时支持这个模型和工作台使用的协议。符合条件的 Key 可以直接复用；需要分开统计用量、设置限额或轮换凭证时，再按用途新建 Key。

创建方法和分组原则见 [创建 API Key](/docs/start/create-api-key)。仍不清楚工作台和模型的区别，可以先看 [工具不是模型](/docs/concepts/tools-models-platform)。

<h2 id="continue">进入对应指南</h2>

每个工作台页面都会给出安装方式、配置入口和首次验证方法。已经安装过时，只需完成 SorryCode 接入部分。

需要手动验证 API 时，看 [首条请求](/docs/start/first-request)。遇到共性错误时，看 [常见错误](/docs/troubleshoot/common-errors)。
