---
title: Creation and Design
slug: creation-design
order: 1
summary: The entry point for images, posters, one-pagers, resumes, reports, portfolios, and web-style decks.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
---

# Creation and Design

This skill group is for finished artifacts.

If you want the agent to make an image, a polished document, or a presentation deck instead of only giving you text in chat, start here.

<h2 id="choose">How to Choose</h2>

| What you need | Start with |
| --- | --- |
| Generate covers, posters, illustrations, product visuals, or 2D game assets | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| Make one-pagers, resumes, reports, white papers, portfolios, or paper-style slides | [Kami](/docs/skills/kami) |
| Make web-style or magazine-style presentation decks | [Magazine Web PPT](/docs/skills/magazine-web-ppt) |
| Make code-based decks with comments and HTML/PDF export | [Tools / Open Slide](/docs/tools/open-slide) |
| Make product videos, launch motion, or social MP4 clips | [Tools / HyperFrames](/docs/tools/hyperframes) |
| Make app prototypes, motion design, infographics, variations, or design critique | [Huashu Design](/docs/skills/huashu-design) |
| Understand why design skills are steadier than prompts | [Why Design Skills Are Different](/docs/skills/design-skills) |
| Keep one project aligned to the same visual rules over time | [Agent Infrastructure / DESIGN.md](/docs/agent-infra/design-md) |

<h2 id="office-vs-design">How It Differs From Office Docs</h2>

[Office Docs](/docs/skills/office-docs) is for existing files, such as editing Word documents, cleaning Excel workbooks, updating PowerPoint decks, or splitting PDFs.

`Creation and Design` is for finished artifacts: give the agent the topic, audience, material, and style, then ask it to produce something you can show, publish, or keep editing.

<h2 id="first-prompt">First Prompt</h2>

If you do not know which skill to use, ask the agent:

```text
I want to create a polished artifact that I can share with other people. First decide whether I should use SorryCode Image2, Kami, or Magazine Web PPT, then ask me the necessary questions.
```

If you already know you need an image:

```text
Use SorryCode Image2 to generate an article cover about AI coding for beginners. Keep the title clear and save it to outputs/images/cover/.
```

If you need a one-pager:

```text
Use Kami to turn the product introduction below into a one-pager for first-time customers. Ask the necessary questions first, then start layout.
```

<h2 id="install-note">Install Note</h2>

Install [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code) first, then install the skill that matches the task.

For a first run, use this order:

1. Install [SorryCode Image2](/docs/skills/sorrycode-image2) and generate your first image
2. Install [Kami](/docs/skills/kami) and make a one-pager
3. Use [Magazine Web PPT](/docs/skills/magazine-web-ppt) when you need a presentation
4. Use [Open Slide](/docs/tools/open-slide) or [HyperFrames](/docs/tools/hyperframes) when you need a code-based deck or video toolchain
5. Use [Huashu Design](/docs/skills/huashu-design) when you need prototypes, motion, or more complex design work

If you want a full design workbench instead of a single skill, see [Tools / Open Design](/docs/tools/open-design).
