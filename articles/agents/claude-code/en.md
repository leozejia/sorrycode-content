---
title: Claude Code
slug: claude-code
order: 3
summary: Install Claude Code, enable it in Magpie, and start a task from your working folder.
section: agents
section_title: AGENTS
section_order: 10
---

# Claude Code

Claude Code handles code, files, and project tasks in the terminal. This is Claude Code, not the Claude Desktop chat window.

## 1. Install Claude Code

Open the [official Claude Code installation guide](https://code.claude.com/docs/en/overview) and follow the instructions for your system. On Windows, use its PowerShell commands rather than the macOS commands.

For help opening a terminal on Windows, see [Windows PowerShell](/docs/start/common-errors#windows-powershell).

## 2. Enable it in Magpie

Complete [Configure SorryCode in Magpie](/docs/agents/magpie). In the Agent panel, find Claude Code, turn on **Connect**, and choose a model. Exit any running Claude Code process, then start it again.

You do not need to set authentication environment variables manually or run another connector.

## 3. Start a task in your working folder

Open a terminal in the folder you want to work with and run:

```bash
claude
```

Send your first message:

```text
Explain what this folder is for and which files matter most. Do not modify anything.
```

For reusable working methods, read about [Skills](/docs/concepts/skills) and choose when needed. For connection errors, see [Common Questions](/docs/start/common-errors).
