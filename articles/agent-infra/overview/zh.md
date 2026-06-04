---
title: Agent 基建怎么选
slug: overview
order: 1
summary: 先按问题选择入口：管理长会话、维护项目规则文件、统一设计约束、封装可复用 Skills，以及了解 MCP 协议。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# Agent 基建怎么选

Agent 用久了，真正麻烦的通常不是“它会不会回答”。

麻烦的是这些事：

```text
会话越跑越长
项目规则反复解释
换一个工具后上下文丢了
设计风格每次都变
工具、数据和技能不知道该放哪里
```

`Agent 基建` 这组文档不教你追模型名字。它教你把长期工作整理成可复用的东西。

<h2 id="choose">先按问题选入口</h2>

| 你现在遇到的问题 | 去哪里 |
| --- | --- |
| 会话很长，不知道什么时候该释放 | [长期上下文怎么管理](/docs/agent-infra/context-management) |
| 想让 Agent 长期遵守项目规则（Codex / Claude Code 通用） | [项目规则文件](/docs/agent-infra/project-rules) |
| 做 UI、海报、PPT、文档，希望风格别跑偏 | [DESIGN.md](/docs/agent-infra/design-md) |
| 想把一类重复任务变成可复用能力 | [Skills](/docs/agent-infra/skills) |
| 想让 agent 连接数据库、浏览器、知识库或内部工具 | 看下方 MCP 说明 |

如果你不确定从哪开始，先看 [长期上下文怎么管理](/docs/agent-infra/context-management)。

因为无论你用 Codex、Claude Code，还是别的 agent runtime，都迟早会遇到同一个问题：

```text
哪些内容应该继续留给 agent？
哪些内容应该清掉？
```

<h2 id="mental-model">一张图理解</h2>

可以先这样分：

```text
Runtime = agent 在哪里工作
会话 = 现在正在推进什么
上下文文件 = 长期应该遵守什么
handoff = 换会话前怎么交接
MCP = agent 怎么接外部工具和数据
Skills = agent 遇到某类任务时怎么做
```

`Codex / Claude Code` 是 runtime。

`AGENTS.md / CLAUDE.md / DESIGN.md` 是上下文文件。

`MCP` 负责工具和数据连接。

`Skills` 负责把重复工作流打包。

<h2 id="mcp">MCP 是什么</h2>

MCP（Model Context Protocol）是一个开放协议，让 Agent 连接外部工具、数据和服务的标准化方式。

简单说：如果 Skills 是"操作手册"（教 Agent 怎么做某类任务），MCP 就是"连接线"（让 Agent 能访问数据库、浏览器、API、知识库等外部系统）。

**大多数普通用户不需要主动配置 MCP。** 以下情况才需要关心：

- 你想让 Agent 直接查询公司内部数据库
- 你想让 Agent 操作浏览器完成复杂流程
- 你想把内部工具或知识库暴露给 Agent

如果你属于以上情况，参考：
- [MCP 官方文档](https://modelcontextprotocol.io/introduction)
- Claude Code 和 Codex 各自的 MCP 配置文档

第一天用 Agent，先不需要学 MCP。等你的项目规则文件、上下文管理和 Skills 都稳定了，再回来看。

<h2 id="not-database">先记住一件事</h2>

聊天记录不是数据库。

长会话可以很有用，也可能变脏。缓存命中可以省钱，也可能只是在重复旧噪音。真正该长期保存的东西，应该写进项目文件；阶段性状态，应该用 handoff 交接；已经废弃的判断，就应该明确标掉。

这就是 Agent 基建的起点。
