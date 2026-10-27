---
title: Other Agents
slug: other-agents
order: 6
summary: Already use another agent? Install it from its official source and enable the matching client in Magpie.
section: agents
section_title: AGENTS
section_order: 10
---

# Other Agents

If you have not chosen a tool, start with [Codex](/docs/agents/codex). If you already use one of these tools, you do not need to switch workspaces just to connect to SorryCode.

## Downloads and choices

| Agent | Official source | Note |
| --- | --- | --- |
| OpenCode | [Download](https://opencode.ai/download) | Desktop and terminal versions are available; use the one you installed |
| Pi Agent | [Website](https://pi.dev/) | A lightweight terminal tool; follow its current installation guide |
| Kimi Code | [Installation guide](https://www.kimi.com/code/docs/kimi-code-cli/guides/getting-started.html) | A terminal tool; choose a model from Magpie's current list |
| Grok Build | [Official installer](https://x.ai/cli/install.sh) | Connecting a text model does not mean built-in image and video tools also go through SorryCode |
| Cursor | [Download](https://cursor.com/downloads) | The CLI, regular editor, and Private Inference build are different clients; do not mix their configurations |

## Connect through Magpie

1. Install the tool from its official source.
2. Follow [Configure SorryCode in Magpie](/docs/agents/magpie) to add a provider and models, then enable the matching client in the Agent panel. Use only entries that Magpie displays and supports. Do not apply Cursor Private Inference settings to the regular Cursor editor.
3. Reopen the tool, choose a working folder, and send: “List the main files in this folder. Do not modify anything.”

If Magpie does not recognize the client, confirm that installation is complete and the client type matches, then update Magpie. Do not run an old connector or edit configuration files to overwrite its settings. For other errors, see [Common Questions](/docs/troubleshoot/common-errors).
