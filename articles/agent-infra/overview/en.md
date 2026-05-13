---
title: How to Choose Agent Infrastructure
slug: overview
order: 1
summary: Choose the right entry point for long context, AGENTS.md, CLAUDE.md, DESIGN.md, MCP, and Skills.
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
| You use Codex and want it to follow project rules | [AGENTS.md](/docs/agent-infra/agents-md) |
| You use Claude Code and want to maintain project memory | [CLAUDE.md](/docs/agent-infra/claude-md) |
| You make UI, posters, slides, or documents and want stable style | [DESIGN.md](/docs/agent-infra/design-md) |
| You want agents to connect to databases, browsers, knowledge bases, or internal tools | [MCP](/docs/agent-infra/mcp) |
| You want to package a repeated workflow as a reusable capability | [Skills](/docs/agent-infra/skills) |

If you do not know where to start, read [How to Manage Long-Lived Context](/docs/agent-infra/context-management) first.

Whether you use Codex, Claude Code, OpenClaw, or another agent runtime, the same question appears sooner or later:

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

<h2 id="not-database">One Rule First</h2>

Chat history is not a database.

A long session can be useful, and it can also become dirty. Cache hits can save money, and they can also repeat old noise. Durable truth belongs in project files. Temporary state belongs in a handoff. Abandoned conclusions should be marked as abandoned.

That is the starting point for agent infrastructure.
