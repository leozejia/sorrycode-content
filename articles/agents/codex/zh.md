---
title: Codex
slug: codex
order: 2
summary: 默认推荐的 Agent。安装桌面端，通过 Magpie 接入，再打开文件夹完成第一个任务。
section: agents
section_title: AGENTS
section_order: 10
---

# Codex

不知道选哪个 Agent，就先用 Codex。它可以读取文件、修改项目和执行本机任务。

## 1. 安装桌面端

按 [Codex 官方安装说明](https://learn.chatgpt.com/docs/app)下载桌面端。当前官网使用 ChatGPT 桌面端名称，安装后在应用内进入 Codex。

## 2. 在 Magpie 中启用

先完成[用 Magpie 配置 SorryCode](/docs/agents/magpie)，在 Agent 面板找到 Codex，启用「接入」并选择模型。配置后完整退出桌面端，再重新打开。

不用另外运行 SorryCode 接入脚本，也不用手动修改配置文件。

## 3. 打开文件夹，试一个任务

在 Codex 中打开要处理的文件夹，发送：

```text
先看看这个文件夹里有什么，告诉我哪些文件值得先读。不要修改或删除文件。
```

确认它能读取正确的目录并回复，再开始实际工作。需要做图片、文档等任务时，继续看 [Skills](/docs/skills/featured-skills)；接入报错看[常见问题](/docs/troubleshoot/common-errors)。
