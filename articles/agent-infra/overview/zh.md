---
title: Agent 基建是什么
slug: overview
order: 1
summary: 用一张地图理解 runtime、上下文文件、协议和 skills 的关系。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# Agent 基建是什么

AI 时代不只是打开一个聊天框。

真正稳定的 agent 工作方式，通常由四层组成：

```text
Runtime = agent 在哪里工作
上下文文件 = agent 应该长期遵守什么规则
协议 = agent 如何连接外部工具和数据
Skills = agent 如何获得某类任务的可复用工作流
```

`Codex / Claude Code` 是 runtime。`AGENTS.md / CLAUDE.md / DESIGN.md` 是上下文文件。`MCP` 是连接工具和数据的协议。`Skills` 是可以安装、复用、分发的能力包。

<h2 id="why">为什么要单独理解这些</h2>

只靠一句提示词，很难让 agent 长期稳定。

常见问题是：

- 每次都要重新解释项目结构
- 换一个 agent 后规则丢失
- 设计风格一轮一个样
- 工具和数据连接方式混乱
- 任务流程靠临场发挥，结果不稳定

这些基建概念的共同目标，是把长期上下文、工具连接和工作流沉淀下来。

<h2 id="map">一张表理解</h2>

| 概念 | 解决什么 |
| --- | --- |
| [AGENTS.md](/docs/agent-infra/agents-md) | Codex 读取的项目指令文件 |
| [CLAUDE.md](/docs/agent-infra/claude-md) | Claude Code 读取的记忆和指令文件 |
| [DESIGN.md](/docs/agent-infra/design-md) | 设计 agent 读取的设计上下文文件 |
| [MCP](/docs/agent-infra/mcp) | agent 连接外部工具和数据的协议 |
| [Skills](/docs/agent-infra/skills) | agent 可安装、可复用的能力包 |

<h2 id="relationship">和 SorryCode 的关系</h2>

SorryCode 负责帮你创建 `API Key`，把 runtime、模型和能力连接起来。

但长期要用好 AI，不只是会创建 key。你还需要知道：哪些规则应该写进项目，哪些能力应该装成 skill，哪些工具应该通过协议接入。

这就是 `Agent 基建` 这一组页面的作用。
