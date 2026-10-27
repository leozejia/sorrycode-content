---
title: Claude Code
slug: claude-code
order: 3
summary: 安装 Claude Code，在 Magpie 中启用，然后进入工作目录开始任务。
section: agents
section_title: AGENTS
section_order: 10
---

# Claude Code

Claude Code 适合在终端里处理代码、文件和项目任务。这里说的是 Claude Code，不是 Claude Desktop 聊天窗口。

## 1. 安装 Claude Code

打开 [Claude Code 官方安装说明](https://code.claude.com/docs/en/overview)，按你的系统完成安装。Windows 用户使用说明中的 PowerShell 命令，不要复制 macOS 命令。

不知道怎么打开终端时，看 [Windows PowerShell](/docs/start/common-errors#windows-powershell)。

## 2. 在 Magpie 中启用

先完成[用 Magpie 配置 SorryCode](/docs/agents/magpie)，在 Agent 面板找到 Claude Code，启用「接入」并选择模型。已有 Claude Code 进程需要退出后重新启动。

不用再手动填写认证环境变量或运行另一套接入器。

## 3. 在工作目录开始任务

在要处理的文件夹中打开终端，运行：

```bash
claude
```

发送第一句话：

```text
先解释这个文件夹的用途和主要文件，不要修改任何内容。
```

需要扩展任务能力时看 [Skills](/docs/skills/featured-skills)；接入报错看[常见问题](/docs/start/common-errors)。
