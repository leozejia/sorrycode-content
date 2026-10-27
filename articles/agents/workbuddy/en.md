---
title: WorkBuddy
slug: workbuddy
order: 5
summary: Install the WorkBuddy desktop app, enable it in Magpie, and confirm the connection with a file task.
section: agents
section_title: AGENTS
section_order: 10
---

# WorkBuddy

WorkBuddy provides a desktop interface for documents, spreadsheets, and local files.

## 1. Install WorkBuddy

Download the version for your system from the [WorkBuddy website](https://www.workbuddy.cn/), install it, and open it.

## 2. Enable it in Magpie

Complete [Configure SorryCode in Magpie](/docs/agents/magpie). In the Agent panel, find the matching WorkBuddy client, turn on **Connect**, and choose a model. Reopen WorkBuddy, then select the configured model in its model picker.

WorkBuddy and the international WorkBuddy AI app are separate clients. Choose the entry that matches the version you installed.

## 3. Try a file task

Choose a working folder and send:

```text
Read the documents in this folder and write a one-sentence summary for each file, labeled by filename. Reply only; do not modify the originals.
```

Grant access to that folder as needed. You do not need to open access to other folders for this first test. For connection errors, see [Common Questions](/docs/start/common-errors).
