---
title: Agent 基建怎么选
slug: overview
order: 1
summary: 先按问题选择入口：管理长会话、维护 AGENTS.md / CLAUDE.md / DESIGN.md，还是理解 MCP 和 Skills。
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
| 用 Codex，想让它长期遵守项目规则 | [AGENTS.md](/docs/agent-infra/agents-md) |
| 用 Claude Code，想维护项目 memory | [CLAUDE.md](/docs/agent-infra/claude-md) |
| 做 UI、海报、PPT、文档，希望风格别跑偏 | [DESIGN.md](/docs/agent-infra/design-md) |
| 想让 agent 连接数据库、浏览器、知识库或内部工具 | [MCP](/docs/agent-infra/mcp) |
| 想把一类重复任务变成可复用能力 | [Skills](/docs/agent-infra/skills) |

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

<h2 id="not-database">先记住一件事</h2>

聊天记录不是数据库。

长会话可以很有用，也可能变脏。缓存命中可以省钱，也可能只是在重复旧噪音。真正该长期保存的东西，应该写进项目文件；阶段性状态，应该用 handoff 交接；已经废弃的判断，就应该明确标掉。

这就是 Agent 基建的起点。
