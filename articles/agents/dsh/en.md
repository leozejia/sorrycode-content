---
title: DeepSeek Harness
slug: dsh
order: 4
summary: Download the DSH desktop app, connect through Magpie, and try a task in a folder.
section: agents
section_title: AGENTS
section_order: 10
---

# DeepSeek Harness

DeepSeek Harness, or DSH, has a desktop app. You do not need to install Node.js first or start a Web UI from the terminal.

## 1. Install the desktop app

Open the [DeepSeek Harness website](https://www.deepseek.com/en/harness/), download the desktop version for your system, and install it. Complete any required system permission prompts on first launch.

## 2. Enable it in Magpie

Complete [Configure SorryCode in Magpie](/docs/agents/magpie). In the Agent panel, find DeepSeek Harness, turn on **Connect**, and choose a model. Reopen DSH after setup.

## 3. Open a folder and try a task

Select a working folder in DSH and send:

```text
Read this folder and list the files by type. Reply with the list only. Do not move or modify any files.
```

Once the reply reflects the actual files, continue with your own task. DSH is changing quickly, so follow the interface in your installed version. For connection errors, see [Common Questions](/docs/troubleshoot/common-errors).
