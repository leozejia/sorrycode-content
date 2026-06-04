---
title: How to Choose Agent Infrastructure
slug: overview
order: 1
summary: Choose the right entry point for long context, project rules files, design constraints, reusable Skills, and the MCP protocol.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# How to Choose Agent Infrastructure

After you use agents for a while, the hard part is usually not whether the agent can answer.

The hard part is this:

```text
sessions keep growing
project rules get repeated
switching tools loses context
design style drifts every run
tools, data, and skills have no clear home
```

This section is not about chasing model names. It is about turning long-running work into reusable structure.

<h2 id="choose">Choose by Problem</h2>

| Your problem | Go here |
| --- | --- |
| The session is long and you do not know when to release it | [How to Manage Long-Lived Context](/docs/agent-infra/context-management) |
| You want your agent to follow project rules (Codex or Claude Code) | [Project Rules File](/docs/agent-infra/project-rules) |
| You make UI, posters, slides, or documents and want stable style | [DESIGN.md](/docs/agent-infra/design-md) |
| You want to package a repeated workflow as a reusable capability | [Skills](/docs/agent-infra/skills) |
| You want agents to connect to databases, browsers, knowledge bases, or internal tools | See MCP section below |

If you do not know where to start, read [How to Manage Long-Lived Context](/docs/agent-infra/context-management) first.

Whether you use Codex, Claude Code, or another agent runtime, the same question appears sooner or later:

```text
what should the agent keep carrying?
what should be cleared?
```

<h2 id="mental-model">Mental Model</h2>

Use this first map:

```text
Runtime = where the agent works
Session = what is happening right now
Context files = long-lived rules
Handoff = transfer note before switching sessions
MCP = how agents connect to tools and data
Skills = how agents handle a class of tasks
```

`Codex / Claude Code` are runtimes.

`AGENTS.md / CLAUDE.md / DESIGN.md` are context files.

`MCP` handles tool and data connections.

`Skills` package repeated workflows.

<h2 id="mcp">What Is MCP</h2>

MCP (Model Context Protocol) is an open protocol that standardizes how agents connect to external tools, data, and services.

The short version: if Skills are "instruction manuals" (teaching the agent how to do a type of task), MCP is the "cable" (letting the agent access databases, browsers, APIs, knowledge bases, and other external systems).

**Most ordinary users do not need to configure MCP.** You only need to care if:

- You want the agent to query your company's internal database directly
- You want the agent to operate a browser for complex workflows
- You want to expose internal tools or knowledge bases to the agent

If any of those apply, start here:
- [MCP official documentation](https://modelcontextprotocol.io/introduction)
- Claude Code and Codex each have their own MCP configuration docs

On day one with agents, you do not need MCP. Come back after your project rules, context management, and Skills are stable.

<h2 id="not-database">One Rule First</h2>

Chat history is not a database.

A long session can be useful, and it can also become dirty. Cache hits can save money, and they can also repeat old noise. Durable truth belongs in project files. Temporary state belongs in a handoff. Abandoned conclusions should be marked as abandoned.

That is the starting point for agent infrastructure.
