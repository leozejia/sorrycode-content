---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 创建 API Key，用 Magpie 配置，再打开 Codex 完成第一个任务。
section: start
section_title: 开始使用
section_order: 1
---

# 第一次使用 SorryCode

第一次使用，按下面三步走。不需要先学终端命令、配置文件或比较所有模型。

## 1. 创建 API Key

登录 [SorryCode 控制台](https://sorrycode.com)，充值余额，并按[创建 API Key](/docs/start/create-api-key)选择需要的模型分组、复制密钥。

## 2. 用 Magpie 配置

按[用 Magpie 配置 SorryCode](/docs/agents/magpie)，从官网安装 Magpie，添加自定义供应商、填入对应分组的 Key，再点击「获取模型」。

先配置一个要用的分组即可，不用一次添加全部模型。

## 3. 安装 Agent，开始任务

不确定选什么，就按 [Codex](/docs/agents/codex)安装桌面端，在 Magpie 的 Agent 面板启用，然后打开一个文件夹试用：

```text
告诉我这个文件夹里有哪些主要文件。先只读取，不修改内容。
```

已经习惯其他工具，也可以用 [Claude Code](/docs/agents/claude-code)、[DeepSeek Harness](/docs/agents/dsh)、[WorkBuddy](/docs/agents/workbuddy) 或[其他 Agents](/docs/agents/other-agents)。它们都从 Magpie 的对应入口接入，不用再学一套配置。

能正常回复后，就可以开始自己的任务，不必先装 Skill。需要复用工作方法时，再了解 [Skills](/docs/concepts/skills)。接入失败看[常见问题](/docs/start/common-errors)；只有需要手动排查 API 时才看[首条请求](/docs/start/first-request)。
