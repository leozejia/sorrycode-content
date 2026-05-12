---
title: What Are Skills
slug: featured-skills
order: 1
summary: A skill is an instruction manual for the agent. After installing Codex or Claude Code, use skills to make image work, document design, slides, project reading, and engineering workflows more reliable.
section: skills
section_title: Skills
section_order: 15
---

# What Are Skills

A skill is an instruction manual for the agent.

You do not need to learn every step yourself. Install `Codex` or `Claude Code`, install the right skill, then tell the agent what you want:

```text
Use SorryCode Image2 to generate a cover.
```

```text
Use Kami to turn this content into a one-pager.
```

```text
Use Waza to check this change before I finish.
```

The skill tells the agent what to check, how to work, where to save the result, and how to explain common problems.

<h2 id="why-skills">Why Use Skills</h2>

A smart model is not enough by itself.

A frontier model can understand a lot, but it does not always know:

- what to check before starting this task
- which model, endpoint, or template to use by default
- where the result should be saved
- which errors should be explained in beginner-friendly language
- which repeated steps should be handled by scripts instead of rewritten every time

A skill turns that experience into a reusable capability pack. Install it once, then keep asking the agent to use the same working method.

<h2 id="trigger">How to Trigger Skills Reliably</h2>

The most reliable way is to name the skill directly.

```text
Use SorryCode Image2 to edit ./input/product.png into a website hero visual and save it to outputs/images/product-hero/.
```

```text
Use Kami to typeset notes.md into a polished one-page PDF.
```

```text
Use Waza check to review this change before I finish.
```

For more reliable triggering, include three things:

- which skill to use
- what you want done
- where the input or output should be

<h2 id="start">Which Skill to Start With</h2>

If you have not installed a runtime yet, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

After your runtime works, choose by goal:

- First deck, design, image, one-pager, or cover: [Skills / How to Use Design Skills](/docs/skills/design-workflow)
- Work with Word / Excel / PowerPoint / PDF: [Skills / Office Docs](/docs/skills/office-docs)
- Generate images, one-pagers, resumes, reports, or web-style decks: [Skills / Creation and Design](/docs/skills/creation-design)
- Diagnose business questions, benchmarks, or content direction: [Skills / DBSkill](/docs/skills/dbskill)
- Make AI coding workflows steadier: [Skills / Waza](/docs/skills/waza)

To understand `AGENTS.md / CLAUDE.md / DESIGN.md / MCP / Skills` as standards and capability mechanisms, go to [Agent Infrastructure](/docs/agent-infra/overview).

<h2 id="deeper">A Bit Deeper: Why Skills Are Special</h2>

A normal prompt is one-off. A skill can be installed, reused, shared, and improved over time.

A skill usually contains:

- `SKILL.md`: instructions the agent reads after the skill triggers
- `description`: helps the agent decide when to use it
- `references`: extra material loaded only when needed
- `scripts`: repeatable operations that should run reliably
- `assets`: templates, fonts, styles, or example files

So a skill is not just a longer prompt. It is a way to hand a workflow to the agent.

<h2 id="mechanism">How Skills Trigger</h2>

The most important field is the `description` at the top of `SKILL.md`.

Think of it as the skill’s usage label. The agent compares your request with the `description` to decide whether to load the skill.

Weak trigger description:

```text
Useful assistant tool.
```

Stronger trigger description:

```text
Generate or edit images. Use when the user asks for covers, posters, product visuals, avatars, game sprites, or restyling an existing image.
```

As a normal user, you do not need to learn this first. If you name the skill in your request, you are already using the most reliable trigger path.

<h2 id="skill-creator">Use Skill Creator to Make Your Own Skills</h2>

When you notice yourself repeating the same instructions to the agent, it may be time to create your own skill.

This matters especially for design, decks, images, and writing. Repeated style preferences, revision notes, and acceptance rules can become your own `DESIGN.md`, references, or skill, so the agent can start closer to your direction next time.

`Skill Creator` does not just write a longer prompt. It turns a workflow into a reusable capability:

1. Collect real usage examples
2. Define when the skill should trigger
3. Put the stable workflow into `SKILL.md`
4. Move long reference material into `references`
5. Move fragile repeated operations into `scripts`
6. Test it on real tasks and iterate

If you already use Codex, you can say:

```text
Use Skill Creator to help me turn this repeated workflow into a skill. Ask me three key questions first, then propose the skill structure.
```

<h2 id="runtime-plus-skills">Why Runtime + Skills</h2>

`Codex` / `Claude Code` decide where the agent works: reading projects, editing files, running commands, and continuing a task.

`Skills` decide how the agent should do a class of work: what to check, what to call, where to save output, and what “done” means.

A useful mental model:

```text
Runtime = the agent’s workbench
Skills = the agent’s professional playbooks
```

That is why SorryCode recommends learning `Codex / Claude Code + Skills`. You are not just learning one tool; you are building a reusable AI working system.
