---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 选择要用的 Agent 工具，确认 API Key 和分组兼容，再进入该工具的接入指南。
section: start
section_title: 开始使用
section_order: 1
---

# 第一次使用 SorryCode

SorryCode 为 Codex、Claude Code、WorkBuddy 等 Agent 工具提供模型 API。第一次使用时，先选工具，再按对应指南完成安装和配置。

<h2 id="choose-tool">选择 Agent 工具</h2>

| 工具 | 适合什么 | 接入指南 |
| --- | --- | --- |
| **Codex** | 默认选择。适合代码、文件和本机任务，也有可视化 App | [Codex](/docs/runtime/codex) |
| **Claude Code** | 使用 Claude 模型完成代码和终端任务 | [Claude Code](/docs/runtime/claude-code) |
| **WorkBuddy** | 在桌面界面处理文档、表格和本地文件 | [WorkBuddy](/docs/runtime/workbuddy) |
| **Grok CLI** | 使用 Grok 模型和 xAI 生态能力 | [Grok CLI](/docs/runtime/grok-cli) |
| **Kimi Code** | 使用 Kimi 模型完成代码和长上下文任务 | [Kimi Code](/docs/runtime/kimi-code) |

不确定选哪个时，先用 Codex。

<h2 id="prepare-key">准备兼容的 API Key</h2>

登录 [SorryCode 控制台](https://sorrycode.com)，确认余额可用，并检查现有 API Key 所属分组是否支持目标模型和工具使用的协议。符合条件的 Key 可以直接复用，不必为每个工具单独创建；需要分开统计用量、设置限额或轮换凭证时，再按用途新建 Key。

创建方法和分组原则见 [创建 API Key](/docs/start/create-api-key)。不要把 Key 填入不兼容的协议，或填入所属分组未开放的模型。

<h2 id="continue">进入对应指南</h2>

每个工具页面会给出当前安装方式、配置入口和首次验证方法。已经安装过工具时，也从对应页面开始，只完成 SorryCode 接入部分即可。

需要手动验证 API 时，看 [首条请求](/docs/start/first-request)。遇到共性错误时，看 [常见错误](/docs/troubleshoot/common-errors)。
