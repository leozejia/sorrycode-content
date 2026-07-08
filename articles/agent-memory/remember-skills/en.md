---
title: Make AI Remember Work Methods
slug: remember-skills
order: 5
summary: Turn repetitive workflows into Skills, making AI remember how to do images, documents, code review, and other tasks.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# Make AI Remember Work Methods

`Skills` are installable, reusable capability packs for agents.

If a runtime decides where the agent works, skills decide how the agent should handle a class of tasks.

This is not a SorryCode-only concept. The Codex docs describe skills as the authoring format for reusable workflows and say they build on the open agent skills standard. Different agent runtimes can use different install locations and loading details, but the core idea is the same: package a reusable workflow so the agent can read it at the right time.

<h2 id="what-is-it">What It Is</h2>

A skill often contains:

- `SKILL.md`: the main instructions read by the agent
- `description`: helps the agent decide when to trigger it
- `references`: long material loaded only when needed
- `scripts`: repeatable operations that should run reliably
- `assets`: templates, fonts, images, or examples
- `agents/openai.yaml`: optional Codex App metadata, invocation policy, and dependencies

A skill is not a longer prompt. It is a reusable workflow.

Codex first sees each skill’s `name / description / file path` and uses that short listing to decide whether a skill is relevant. It reads the full `SKILL.md` only after selecting that skill. This is progressive disclosure: keep the initial context small, then load the full workflow only when needed.

<h2 id="who-reads-it">Who Reads It</h2>

Skills are read by agent runtimes that support them, such as Codex, Claude Code, or compatible workbenches.

Users usually do not need to memorize the internals. Name the skill directly:

```text
Use Kami to turn this content into a one-pager.
```

<h2 id="trigger">How to Trigger a Skill</h2>

The reliable path is simple:

- name the skill directly, such as “Use Kami”; in Codex CLI / IDE, you can also use `/skills` or `$` to choose one
- describe the task type, such as “turn this content into a one-pager”
- provide input material, audience, and output location
- if the project has rules, ask the agent to read `AGENTS.md / CLAUDE.md / DESIGN.md` first

Do not only say “make this better.” The closer your request is to the skill description, the more reliably it will trigger.

<h2 id="how-to-make">How to Create a Skill</h2>

Creating a skill is not about writing a longer prompt. It is about making the workflow explicit:

1. Define which tasks the skill is for.
2. Put the agent workflow in `SKILL.md`.
3. Put long reference material in `references/` so the agent loads it only when needed.
4. Put repeatable or error-prone operations in `scripts/`.
5. Put templates, fonts, and example files in `assets/`.
6. Test the skill on real tasks to see whether it triggers reliably.

If you repeat the same kind of work often, use `Skill Creator` to turn it into your own skill.

<h2 id="where">Where to Put Skills</h2>

Codex reads skills from several locations. For most users, the important ones are:

- repository skills: `.agents/skills`
- user skills: `~/.agents/skills`
- built-in system skills, such as `skill-creator`

Repository skills are good for teams. User skills are good for your own workflows across projects. The one-line install commands in public docs usually install skills at the user level.

If a newly installed skill does not appear, restart the runtime.

<h2 id="problem">What It Solves</h2>

Without a skill, the agent has to improvise every time:

- what to check first
- which tool to use
- where files should be saved
- how to explain failures
- how to verify the result

Skills capture that working method.

<h2 id="relationship">Relationship With AGENTS.md and MCP</h2>

- `AGENTS.md / CLAUDE.md`: long-lived project rules
- `DESIGN.md`: design context
- `MCP`: tool and data connection protocol
- `Skills`: workflow capability packs

They can work together. An image skill can read `DESIGN.md`, then call an image API or an MCP tool.

<h2 id="where-next">Next</h2>

To install concrete skills, go to [Skills / What Are Skills](/docs/skills/featured-skills).

<h2 id="reference">Reference</h2>

- OpenAI Codex / Skills: <https://developers.openai.com/codex/skills>
