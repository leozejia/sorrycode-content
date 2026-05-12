---
title: Why Design Skills Are Different
slug: design-skills
order: 6
summary: Design skills do more than add visual words to a prompt. They fix style, constraints, assets, and delivery rules before the agent starts.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
---

# Why Design Skills Are Different

Design tasks drift fast.

When you ask an agent to make a cover, one-pager, web deck, or product visual, it has to handle style, hierarchy, spacing, colors, assets, export format, and revision flow. A prompt like “make it look premium” does not give the agent enough structure.

A design skill turns those unstable requirements into a working process.

<h2 id="what-changes">What Changes After Installing One</h2>

A normal prompt tells the agent what you want this time. A design skill can also tell it:

- what questions to ask before starting
- which visual language to use by default
- which layout and color choices to avoid
- where assets should live
- what files to export
- how to continue after a failed attempt

That is why skills like `Kami`, `Guizang PPT Skill`, `SorryCode Image2`, and `Huashu Design` work better as reusable skills than as long prompts you rewrite every time.

<h2 id="when-use">When to Use One</h2>

Use a design skill first when:

- you want a cover, poster, article image, or product visual
- you want to turn content into a one-pager, resume, report, or portfolio
- you want a presentation deck that can be shown to other people
- you want app prototypes, motion design, infographics, or design variations
- you want repeated outputs to keep the same style
- you want saved files, not only text in chat

If you are editing an existing Word, Excel, PowerPoint, or PDF file, start with [Skills / Office Docs](/docs/skills/office-docs).

<h2 id="first-prompt">First Prompts</h2>

For images:

```text
Use SorryCode Image2 to generate a warm article cover about AI coding for beginners. Keep the Chinese title clear and save it to outputs/images/cover/.
```

For documents:

```text
Use Kami to turn the product introduction below into a one-pager for first-time customers. Ask the necessary questions first, then start layout.
```

For presentations:

```text
Use Guizang PPT Skill to build a 12-page web deck for my product launch. First decide whether electronic-magazine style or Swiss Style fits better, then propose the outline. Do not generate the final file yet.
```

<h2 id="design-md">Next Step: Write the Design Rules Down</h2>

If you already have brand colors, fonts, page style, references, or rules to avoid, put them in `DESIGN.md`.

`DESIGN.md` is not a skill. It is a design context file for agents. Next: [Agent Infrastructure / DESIGN.md](/docs/agent-infra/design-md).

If you want to see a full design workbench that combines `SKILL.md`, `DESIGN.md`, and artifact preview, see [Tools / Open Design](/docs/tools/open-design).
