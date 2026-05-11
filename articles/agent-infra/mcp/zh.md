---
title: MCP
slug: mcp
order: 5
summary: Model Context Protocol，让 agent 连接外部工具、数据和服务的开放协议。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# MCP

`MCP` 是 `Model Context Protocol`。

它解决的是：agent 如何安全、稳定地连接外部工具、数据和服务。

<h2 id="what-is-it">它是什么</h2>

可以把 MCP 理解成 agent 的连接协议。

模型本身只会生成文本。agent runtime 让模型能读文件、跑命令、改项目。MCP 进一步让 agent 通过统一方式连接数据库、浏览器、设计工具、知识库、内部系统等外部能力。

<h2 id="who-reads-it">谁会使用它</h2>

使用 MCP 的通常不是普通用户手动调用，而是：

- Claude Code、Codex 等 agent runtime
- 本地或远程 MCP server
- 需要把工具和数据暴露给 agent 的应用

<h2 id="problem">它解决什么问题</h2>

没有协议时，每个工具都要单独接一套方式。

MCP 的价值是把连接方式标准化：

- 工具如何暴露给 agent
- agent 如何发现可用能力
- 参数和返回结果如何表达
- 权限和边界如何收口

<h2 id="when-care">什么时候需要关心</h2>

第一天不需要先学 MCP。

当你遇到下面这些需求时，再看它：

- 让 agent 查数据库
- 让 agent 操作浏览器
- 让 agent 读取公司知识库
- 让 agent 调内部工具
- 想把自己的工具开放给多个 agent runtime

<h2 id="relationship">和 Skills 的区别</h2>

`Skills` 更像操作手册：告诉 agent 某类任务应该怎么做。

`MCP` 更像连接协议：告诉 agent 可以调用哪些外部工具和数据。

它们可以一起用。一个 skill 可以指导 agent 何时调用某个 MCP 工具。

<h2 id="reference">参考</h2>

- Model Context Protocol：<https://modelcontextprotocol.io/introduction>
