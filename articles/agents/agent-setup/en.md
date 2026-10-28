---
title: Install and Use an Agent
slug: agent-setup
order: 2
summary: Choose and install an agent, connect it through Magpie, and try a first task in a working folder.
section: agents
section_title: AGENTS
section_order: 10
---

# Install and Use an Agent

Choose one tool. If you are unsure, start with Codex. The table keeps the installation and startup steps that differ; configure models once in [Magpie](/docs/agents/magpie).

## 1. Install Your Tool

| Agent | Install and start | When to use it |
| --- | --- | --- |
| Codex | Download the [Codex desktop app](https://learn.chatgpt.com/docs/app) and open Codex in the app | Files, code, and project tasks |
| Claude Code | Download the [Claude desktop app](https://claude.com/download) and open Code, or follow the [official instructions](https://code.claude.com/docs/en/overview) to install the terminal version | Files, code, and project tasks |
| DeepSeek Harness | Download and install the desktop app from the [official site](https://www.deepseek.com/harness/) | Desktop file and project tasks |
| WorkBuddy | Download and install it from the [official site](https://www.workbuddy.ai/), then sign in as prompted | Documents, spreadsheets, and local files |
| OpenCode, Pi, Kimi Code, Grok Build, and others | Install from their official sources and start the version you installed | Users already familiar with these tools |

Other official sources: [OpenCode](https://opencode.ai/download), [Pi](https://pi.dev/), [Kimi Code](https://www.kimi.com/code/docs/kimi-code-cli/guides/getting-started.html), and [Grok Build](https://x.ai/cli/install.sh). If you cannot open a terminal, see [Windows PowerShell](/docs/start/common-errors#windows-powershell).

## 2. Enable It in Magpie

1. Follow the [Magpie guide](/docs/agents/magpie) to add a SorryCode provider and fetch models.
2. Find the installed tool in Magpie's Agent panel, turn on **Connect**, and choose a provider and model.
3. Reopen the tool and keep Magpie running. If it does not appear, check that the matching client is installed and use the panel's detection button. Support depends on the current version.

Quit Codex desktop completely before reopening it. In WorkBuddy, select the configured model in the app's model picker. If DSH's input is unavailable, select a model and workspace first. For the terminal version of Claude Code, run `claude` from your working folder.

The Cursor editor is not part of this default path; see [manual Cursor setup](/docs/agents/cursor).

## 3. Try Your First Task

Choose a test folder, grant access when prompted, and send:

```text
Look at this folder and explain what the main files are for. Do not modify or delete anything.
```

Check that the reply matches the folder before starting your own task. A successful chat does not verify file writing, network access, or image tools; authorize and test those separately. For problems, see the [FAQ](/docs/start/common-errors).
