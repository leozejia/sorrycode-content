---
title: What Is Agent Infrastructure
slug: overview
order: 1
summary: A map for runtimes, context files, protocols, and skills.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# What Is Agent Infrastructure

AI work is no longer just a chat box.

A steadier agent setup usually has four layers:

```text
Runtime = where the agent works
Context files = long-lived rules the agent should follow
Protocols = how the agent connects to tools and data
Skills = reusable workflows for classes of tasks
```

`Codex / Claude Code` are runtimes. `AGENTS.md / CLAUDE.md / DESIGN.md` are context files. `MCP` connects tools and data. `Skills` are installable capability packs.

<h2 id="why">Why This Matters</h2>

One prompt is not enough for long-lived work.

Common problems:

- you repeat the same project structure every time
- switching agents loses the rules
- design style changes from run to run
- tool and data access becomes ad hoc
- task workflows depend on improvisation

These infrastructure concepts keep long-lived context, tool access, and workflows in reusable form.

<h2 id="map">Map</h2>

| Concept | What it solves |
| --- | --- |
| [AGENTS.md](/docs/agent-infra/agents-md) | Project instructions for Codex |
| [CLAUDE.md](/docs/agent-infra/claude-md) | Memory and instructions for Claude Code |
| [DESIGN.md](/docs/agent-infra/design-md) | Design context for design agents |
| [MCP](/docs/agent-infra/mcp) | Protocol for connecting tools and data |
| [Skills](/docs/agent-infra/skills) | Installable reusable workflows |

<h2 id="relationship">How This Relates to SorryCode</h2>

SorryCode helps you create an `API Key` and connect runtimes, models, and capabilities.

Using AI well over time also means knowing which rules belong in project files, which capabilities should become skills, and which tools should connect through protocols.
