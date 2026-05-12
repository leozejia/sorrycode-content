---
title: Guizang PPT Skill
slug: magazine-web-ppt
order: 4
summary: An evolving presentation-making skill for agent-built single-file HTML decks, visual systems, deck images, and platform covers.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/op7418/guizang-ppt-skill
---

# Guizang PPT Skill

`Guizang PPT Skill` refers to the open-source `guizang-ppt-skill` by Guizang. It is not the only PPT path in SorryCode. It is one strong presentation-making skill we currently recommend.

Use it when you want an agent to create a single-file horizontal HTML deck with a clear design system. Upstream is no longer just a magazine-style template: it now covers electronic-magazine style, Swiss Style, image generation workflow, platform covers, and quality checks. For exact layouts, themes, scripts, and latest capabilities, follow the official repository.

Reference: [guizang-ppt-skill repository](https://github.com/op7418/guizang-ppt-skill)

<h2 id="what-is-it">What It Is</h2>

- a design-oriented skill for presentation work
- output is usually a single HTML file, not `.pptx`
- it helps the agent build a deck from topic, audience, duration, material, and visual direction
- upstream evolves quickly; SorryCode only documents the stable usage boundary

Think of it as giving the agent a mature presentation design workflow, not asking it to improvise from a long style prompt every time.

<h2 id="what-is-good-for">What It Is Good For</h2>

Use it for:

- talks, private salons, and internal industry sharing
- AI product launches, research presentations, and demo days
- presentations that need a strong personal visual style
- web decks that should look complete and be ready to present
- deck images or platform covers that follow the same visual system

If you only need to edit an existing `.pptx`, start with [PPTX](/docs/skills/pptx). If you need a maintainable React deck, start with [Tools / Open Slide](/docs/tools/open-slide).

<h2 id="presentation-route">How It Fits With Other PPT Paths</h2>

| Need | Start with |
| --- | --- |
| Edit an existing PowerPoint file, use a company template, deliver `.pptx` | [PPTX](/docs/skills/pptx) |
| Quickly make a web deck with a strong visual system | `Guizang PPT Skill` |
| Turn writing, reports, resumes, or portfolios into paper-like artifacts | [Kami](/docs/skills/kami) |
| Build prototypes, launch visuals, infographics, motion-like PPT, or critique | [Huashu Design](/docs/skills/huashu-design) |
| Build a code-based deck with comments and HTML/PDF export | [Tools / Open Slide](/docs/tools/open-slide) |

<h2 id="what-is-not-good-for">What It Is Not Good For</h2>

Do not start here if you need:

- a company `.pptx` template as the final deliverable
- large tables or high-density training material
- traditional PowerPoint files for long-term team editing
- general long documents, resumes, one-pagers, or portfolios

<h2 id="one-click-install">One-Click Install</h2>

These are the upstream install commands verified by SorryCode.

### Codex

```bash
npx skills add op7418/guizang-ppt-skill -a codex -g -y
```

### Claude Code

```bash
npx skills add op7418/guizang-ppt-skill -a claude-code -g -y
```

If you have not installed a runtime yet, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="how-to-use">How to Trigger It</h2>

Describe the presentation you want. Do not start with implementation details.

Try to include:

- topic
- audience
- setting
- duration
- source material and images
- visual direction, such as magazine style, Swiss Style, or product-launch style

If you do not provide everything, the skill should ask the necessary questions first. Align on the outline before generating the final file.

<h2 id="first-prompts">First Prompts</h2>

For a private salon:

```text
Use Guizang PPT Skill to make a roughly 20-page deck about how AI changes organizational collaboration. The audience is company leadership, and the talk is a 30-minute private salon. Ask the necessary questions first, then propose the outline.
```

For turning an article into slides:

```text
Use Guizang PPT Skill to turn the article below into a presentation deck. First decide whether electronic-magazine style or Swiss Style fits better, then propose the page structure.
```

For a product launch:

```text
Use Guizang PPT Skill to make a product launch deck with a cover, 3 acts, a data page, a before/after comparison, and a closing page. I will put images in an images folder.
```

<h2 id="images">How to Place Images</h2>

The simplest path is to create an `images/` folder next to the HTML file.

Use page numbers and English names:

```text
ppt/
├── index.html
└── images/
    ├── 01-cover.jpg
    ├── 03-figma.png
    └── 05-dashboard.png
```

Keep the rules simple:

- use `JPG` for photos
- use `PNG` for screenshots
- use zero-padded page numbers like `01-cover`
- to replace an image, overwrite the file with the same name instead of editing HTML paths

<h2 id="common-issues">Common Issues</h2>

- `npx`, `node`, or `npm` is missing
  See [Environment / Node.js](/docs/environment/nodejs)
- Does it generate `.pptx` files?
  Not by default. It generates a single-file HTML deck
- Why does SorryCode not list every theme and layout?
  Upstream evolves quickly. SorryCode documents selection, install, trigger, and boundaries; the official repository documents latest capabilities
- I need a normal document or resume
  Start with [Skills / Kami](/docs/skills/kami)
- I use OpenClaw or Hermes Agent
  The upstream skill can inform other agents, but SorryCode currently verifies `Codex / Claude Code`

<h2 id="references">References</h2>

- Official repository: <https://github.com/op7418/guizang-ppt-skill>
- Public install path: `npx skills add op7418/guizang-ppt-skill`
- Last checked: 2026-05-12. The upstream README covered dual visual systems, image workflow, platform covers, and quality checks
