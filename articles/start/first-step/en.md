---
title: First Time Using SorryCode
slug: first-step
order: 1
summary: Choose an agent workspace, then confirm model, protocol, and API key group compatibility.
section: start
section_title: Getting Started
section_order: 1
---

# First Time Using SorryCode

Start by choosing the agent workspace that fits how you work, then follow its guide to connect it to SorryCode. A workspace is not a model. The same workspace can use different models when its protocol and API key group support them.

<h2 id="choose-tool">Choose a Workspace</h2>

| Workspace | Good for | Setup guide |
| --- | --- | --- |
| **ChatGPT / Codex** | The default choice for code, files, and local tasks, with a visual app | [ChatGPT / Codex](/docs/runtime/codex) |
| **Claude Code** | Code, terminal tasks, and long-running autonomous work | [Claude Code](/docs/runtime/claude-code) |
| **OpenCode** | An open-source, multi-model agent with both desktop and terminal apps | [OpenCode](/docs/runtime/opencode) |
| **DSH** | DeepSeek's open-source Web agent with configurable Responses models | [DSH](/docs/runtime/dsh) |
| **Pi Agent** | A lightweight, flexible terminal agent with configurable Responses-compatible models | [Pi Agent](/docs/runtime/pi-agent) |
| **Kimi Code** | Coding and long-context tasks with Kimi models | [Kimi Code](/docs/runtime/kimi-code) |
| **WorkBuddy** | Documents, spreadsheets, and local files in a desktop app | [WorkBuddy](/docs/runtime/workbuddy) |
| **Grok Build** | Grok models and xAI capabilities | [Grok Build](/docs/runtime/grok-build) |

If you are unsure, start with ChatGPT / Codex. Choose DSH for a Web UI with configurable Responses models, or OpenCode for an open-source workspace that can use models from multiple providers.

<h2 id="prepare-key">Prepare a Compatible API Key</h2>

Sign in to the [SorryCode console](https://sorrycode.com) and confirm that your balance is available. After choosing a model, check that the API key's group supports both that model and the protocol used by the workspace. You can reuse a compatible key; create a separate one only for usage tracking, spending limits, or credential rotation.

See [Create API Key](/docs/start/create-api-key) for the steps and group rules. If the difference between workspaces and models is still unclear, read [Tools Are Not Models](/docs/concepts/tools-models-platform).

<h2 id="continue">Continue with the Tool Guide</h2>

Each workspace page contains its installation method, configuration entry, and first verification task. If it is already installed, complete only the SorryCode connection steps.

For a manual API check, see [First Request](/docs/start/first-request). For shared errors, see [Common Errors](/docs/troubleshoot/common-errors).
