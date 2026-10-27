---
title: What Are Skills
slug: skills
order: 8
summary: A Skill is a reusable set of instructions for an agent. Choose one when needed, not from a mandatory starter list.
section: concepts
section_title: Core Concepts
section_order: 5
---

# What Are Skills

When you repeatedly ask an agent to follow the same process, you can save that process as a Skill for it to read when needed.

A Skill usually has a `SKILL.md` instruction file and may include reference material, scripts, and templates. It explains how to do a type of task. It is not another model.

<h2 id="when">When You Need One</h2>

Start by asking the agent to do the task. If its existing capabilities are enough, you do not need another Skill.

Choose a Skill when you want to reuse a workflow, output format, or set of checks. Tasks and preferences differ; there is no required starter list.

<h2 id="use">How to Use One</h2>

1. Choose a trusted source and read the purpose, dependencies, and permission requirements.
2. Follow your agent's installation instructions and confirm that it recognizes the Skill. Locations and management commands can differ between clients.
3. Name the Skill in your request and specify the input, goal, and output location.

For example, after installing a report-organizing Skill:

```text
Use my installed Report Organizer Skill to process notes.md and save the result to outputs/report.md. Ask me for missing material instead of inventing data.
```

Report Organizer is an example name. Replace it with a Skill you actually installed. Installation scripts may run commands or access files; do not run material from an unknown source without checking it.

<h2 id="make">Can You Make Your Own?</h2>

Yes. Give the agent your repeated steps, examples, and acceptance criteria. Ask it to package them in a format your client supports, then test on real tasks. Keep the useful process, not every temporary instruction.

<h2 id="relationship">Project Rules, Skills, and MCP</h2>

- `AGENTS.md / CLAUDE.md`: long-lived project rules. See [project rules](/docs/agent-memory/remember-rules).
- `DESIGN.md`: project visual requirements. See [design style](/docs/agent-memory/remember-design).
- Skill: a working method loaded when a task needs it.
- MCP: a protocol for connecting tools and data, not the working method itself.

A Skill does not automatically provide tools, API keys, or extra permissions, and it does not guarantee a correct result. Magpie handles model connections, which is separate from installing Skills. External services still need their own setup and authorization, and important outputs still need review.
