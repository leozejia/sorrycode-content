---
title: Creation and Design
slug: creation-design
order: 1
summary: The entry point for images, posters, one-pagers, resumes, reports, portfolios, and presentation work.
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

If this is your first time making a deck, design, image, one-pager, or cover, read [How to Use Design Skills](/docs/skills/design-workflow) first. These deliverables usually take a few rounds of judgment and revision: start with an editable draft, then use specific feedback to move it closer to what you need.

<h2 id="choose">How to Choose</h2>

| What you need | Start with |
| --- | --- |
| Generate covers, posters, illustrations, product visuals, or 2D game assets | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| Make one-pagers, resumes, reports, white papers, portfolios, or paper-style slides | [Kami](/docs/skills/kami) |
| Quickly make a web deck with a strong visual system | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |
| Make code-based decks with comments and HTML/PDF export | [Tools / Open Slide](/docs/tools/open-slide) |
| Make product videos, launch motion, or social MP4 clips | [Tools / HyperFrames](/docs/tools/hyperframes) |
| Keep one project aligned to the same visual rules over time | [Agent Infrastructure / DESIGN.md](/docs/agent-memory/remember-design) |

<h2 id="office-vs-design">How It Differs From Office Docs</h2>

[Office Docs](/docs/skills/office-docs) is for existing files, such as editing Word documents, cleaning Excel workbooks, updating PowerPoint decks, or splitting PDFs.

`Creation and Design` is for finished artifacts: give the agent the topic, audience, material, and style, then ask it to produce something you can show, publish, or keep editing.

<h2 id="presentation-route">Presentation / PPT Delivery Route</h2>

PPT is not one tool category. It is a delivery format. Start with what you actually need to deliver:

| What you really need | Start with |
| --- | --- |
| Edit an existing PowerPoint file, use a company template, deliver `.pptx` | [PPTX](/docs/skills/pptx) |
| Quickly make a web deck with a strong visual system | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |
| Turn writing, reports, resumes, or portfolios into paper-like artifacts | [Kami](/docs/skills/kami) |
| Build a code-based deck with comments and HTML/PDF export | [Tools / Open Slide](/docs/tools/open-slide) |
| Build presentation videos, launch motion, or social MP4 clips | [Tools / HyperFrames](/docs/tools/hyperframes) |

If this is your first sharing deck, start with [Village / Make a Sharing Deck](/docs/skills/magazine-web-ppt). It gives you a default path instead of a full tool comparison.

<h2 id="first-prompt">First Prompt</h2>

If you do not know which skill to use, ask the agent:

```text
I want to create a polished artifact that I can share with other people. First decide whether I should use SorryCode Image2, Kami, Guizang PPT Skill, PPTX, Open Slide, or HyperFrames, then ask me the necessary questions.
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
3. Use the [Presentation / PPT Delivery Route](#presentation-route) when you need a presentation
4. Use [Open Slide](/docs/tools/open-slide) or [HyperFrames](/docs/tools/hyperframes) when you need a code-based deck or video toolchain

If you want a full design workbench instead of a single skill, see [Tools / Open Design](/docs/tools/open-design).
