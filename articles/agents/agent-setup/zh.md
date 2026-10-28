---
title: 安装和使用 Agent
slug: agent-setup
order: 2
summary: 选择并安装 Agent，通过 Magpie 接入，打开工作目录开始第一个任务。
section: agents
section_title: AGENTS
section_order: 10
---

# 安装和使用 Agent

先选一个工具，不确定时推荐 Codex。下表保留各工具不同的安装和启动步骤，模型配置统一在 [Magpie](/docs/agents/magpie) 完成。

## 1. 安装要用的工具

| Agent | 安装和启动 | 适合什么场景 |
| --- | --- | --- |
| Codex | 下载 [Codex 桌面端](https://learn.chatgpt.com/docs/app)，在应用内进入 Codex | 文件、代码和项目任务 |
| Claude Code | 按[官方说明](https://code.claude.com/docs/en/overview)安装；在工作文件夹打开终端，运行 `claude` | 终端任务，注意它不是 Claude Desktop |
| DeepSeek Harness | 从[官网](https://www.deepseek.com/harness/)下载桌面版并安装 | 桌面文件和项目任务 |
| WorkBuddy | 从[官网](https://www.workbuddy.cn/)下载安装，按提示登录 | 文档、表格和本地文件 |
| OpenCode、Pi、Kimi Code、Grok Build 等 | 从各自的官方来源安装，按实际版本启动 | 已经熟悉这些工具的用户 |

其他官方入口：[OpenCode](https://opencode.ai/download)、[Pi](https://pi.dev/)、[Kimi Code](https://www.kimi.com/code/docs/kimi-code-cli/guides/getting-started.html)、[Grok Build](https://x.ai/cli/install.sh)。终端打不开时看 [Windows PowerShell](/docs/start/common-errors#windows-powershell)。

## 2. 在 Magpie 中启用

1. 按 [Magpie 教程](/docs/agents/magpie)添加 SorryCode 供应商并获取模型。
2. 在 Magpie 的 Agent 面板找到已安装的工具，打开「接入」，选择供应商和模型。
3. 重新打开该工具，并保持 Magpie 运行。如果没有显示，先检查是否安装了对应客户端，再用面板中的重新检测；以当前版本的实际支持为准。

Codex 桌面端要完整退出后重新打开。WorkBuddy 和 WorkBuddy AI 是不同客户端，选择与你安装的版本相符的入口；在 WorkBuddy 的模型选择器中选择刚配置的模型。DSH 如输入框不可用，先选择模型和工作区。Claude Code 在终端执行 `claude`；Windows 请按官方说明选择对应的安装命令。

Claude Desktop 与 Claude Code 是不同客户端，按 Magpie 面板中对应入口操作，不要混用配置。Cursor 编辑器不在这条默认路径中，请看 [Cursor 手动配置](/docs/agents/cursor)。

## 3. 开始第一个任务

选择一个测试文件夹并按提示授权，然后发送：

```text
先看看这个文件夹里有什么，告诉我主要文件的用途。不要修改或删除文件。
```

确认回复与文件夹内容一致后，再开始自己的任务。能对话不代表写文件、联网或图片工具都已验证；这些能力需要单独授权和测试。遇到问题看[常见问题](/docs/start/common-errors)。
