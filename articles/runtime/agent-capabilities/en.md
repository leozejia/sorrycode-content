---
title: How Agent Capabilities Are Extended
slug: agent-capabilities
order: 1
summary: Understand what runtimes, experts, skills, MCP, and plugins each provide, and how they fit together.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: general
group_title: General
group_order: 40
---

# How Agent Capabilities Are Extended

Runtimes such as Codex and WorkBuddy use terms including Expert, Skill, MCP, and Plugin. These are different layers, and products do not always use the same names in the same way.

Start with the question each mechanism answers:

| Mechanism | Question | Main role |
| --- | --- | --- |
| Runtime / workbench | Where does the work happen? | Runs the agent and manages models, sessions, permissions, and projects |
| Expert / agent | Who does the work? | Defines a role, experience, method, and collaboration pattern |
| Skill | How is the work done? | Provides a reusable workflow, standard, or task method |
| MCP / tool / connector | What can the agent access or do? | Connects files, browsers, databases, and external services |
| Plugin | How is it installed and distributed? | Packages related capabilities for a specific runtime |

<h2 id="runtime">The Runtime Determines Where Work Happens</h2>

A runtime is the workbench where an agent runs, such as Codex or WorkBuddy. It determines the available models, project access, permission prompts, and supported extension mechanisms.

The same term can refer to different contracts in different runtimes. When you see “Plugin,” first identify which product defines it instead of applying another product's installation steps.

<h2 id="expert">An Expert Determines Who Does the Work</h2>

In WorkBuddy, an Expert combines a persona, methodology, and toolchain for a specific kind of problem. An Expert Team adds collaboration: a lead divides the task, multiple Experts work on their parts, and the lead integrates the result.

An Expert does not receive extra system permissions. It still accesses files and external services through configured Skills, MCP servers, or tools under the current workspace authorization.

Other runtimes may express a similar idea through agents, subagents, or custom roles without using the word Expert.

<h2 id="skill">A Skill Determines How Work Is Done</h2>

A Skill is a reusable work method. It can define steps, decision criteria, output formats, and constraints for a class of tasks, and may include scripts, references, or templates.

A Skill solves “how to complete this task consistently.” It does not automatically grant access to a browser, database, or external API. A Skill may be installed on its own or packaged inside a Plugin.

<h2 id="tools">MCP and Tools Determine What Can Be Accessed</h2>

MCP servers, tools, and connectors expose data or actions to an agent, such as reading a webpage, querying a database, calling a business system, or controlling a local app.

They usually require their own configuration and authorization. A Skill can tell the agent when to use a tool, but it does not replace the connection, credentials, or permissions.

<h2 id="plugin">A Plugin Packages and Installs Capabilities</h2>

A Plugin is a distribution unit for a runtime, not another word for a tool.

For example, a Codex Plugin can contain Skills, app or connector mappings, MCP configuration, hooks, and assets. What appears after installation, and how it is invoked, depends on the bundled components. There is no universal cross-product `@PluginName` invocation rule.

An ability delivered as a Plugin may therefore include a Skill or MCP integration. Plugin describes how it is delivered; Skill and MCP describe what is delivered.

<h2 id="choose">How to Choose</h2>

- Choose the runtime first: decide where the task will be completed
- Use an Expert, agent, or orchestration mechanism when you need a defined role or multi-agent collaboration
- Install or write a Skill when you need a reusable work method
- Configure MCP, a tool, or a connector when the agent needs external data or actions
- Use a Plugin when several components need to be packaged and distributed together

For example, a WorkBuddy Expert can follow a Skill and query a service through MCP. A Codex Plugin can install a Skill and MCP configuration together. These mechanisms compose; they do not replace one another.

<h2 id="next">Continue Reading</h2>

- [WorkBuddy](/docs/runtime/workbuddy): configure a model and understand Expert and Expert Team
- [Make AI Remember Work Methods](/docs/agent-memory/remember-skills): understand and use Skills
- [Codex](/docs/runtime/codex): install Codex and connect it to SorryCode

Refer to the upstream [Codex Plugin documentation](https://developers.openai.com/plugins/build/plugins) and [WorkBuddy Expert Center](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center) for product-specific definitions.
