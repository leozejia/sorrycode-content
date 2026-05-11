---
title: MCP
slug: mcp
order: 5
summary: Model Context Protocol, an open protocol for connecting agents to tools, data, and services.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# MCP

`MCP` means `Model Context Protocol`.

It answers one question: how should agents connect to external tools, data, and services?

<h2 id="what-is-it">What It Is</h2>

MCP is a connection protocol for agents.

Models generate text. Agent runtimes let models read files, run commands, and work inside projects. MCP gives agents a standard way to connect to databases, browsers, design tools, knowledge bases, internal systems, and other capabilities.

<h2 id="who-uses-it">Who Uses It</h2>

Normal users usually do not call MCP by hand. It is used by:

- agent runtimes such as Claude Code and Codex
- local or remote MCP servers
- apps that expose tools and data to agents

<h2 id="problem">What It Solves</h2>

Without a protocol, every tool needs its own integration path.

MCP standardizes:

- how tools are exposed to agents
- how agents discover available capabilities
- how parameters and results are represented
- how permissions and boundaries are handled

<h2 id="when-care">When You Need to Care</h2>

You do not need MCP on day one.

Look at it when you want an agent to:

- query a database
- control a browser
- read a company knowledge base
- call internal tools
- expose your own tool to multiple agent runtimes

<h2 id="relationship">Relationship With Skills</h2>

`Skills` are more like playbooks: they tell the agent how to do a class of work.

`MCP` is more like a connection protocol: it tells the agent what external tools and data it can use.

They can work together. A skill can tell the agent when to call an MCP tool.

<h2 id="reference">Reference</h2>

- Model Context Protocol: <https://modelcontextprotocol.io/introduction>
