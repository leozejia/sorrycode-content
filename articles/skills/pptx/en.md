---
title: PPTX
slug: pptx
order: 4
summary: A skill for native PowerPoint files: editing existing decks, using templates, and preparing reports or pitch decks.
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: Office Docs
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/pptx
---

# PPTX

The `PPTX` skill is for native PowerPoint files.

If you already have a `.pptx` template, company report, pitch deck, or course deck, and you want an agent to improve structure, unify copy, or update slides, this is the right direction.

<h2 id="what-is-it">What It Helps With</h2>

- Reading existing PowerPoint files
- Editing slide text and structure
- Unifying titles, sections, and messaging
- Working inside an existing company template
- Turning long-form material or outlines into native `.pptx`

<h2 id="when-use">When to Use It</h2>

Use `PPTX` first when:

- the final output must be `.pptx`
- you already have a company template or existing deck
- you want to keep editing in PowerPoint

If you want to create a web deck with a strong visual system from scratch, start with [Guizang PPT Skill](/docs/skills/magazine-web-ppt). If you want a paper-like designed slide deck, [Kami](/docs/skills/kami) may also fit.

<h2 id="how-to-use">How to Use</h2>

When you already have a PowerPoint file, company template, or must deliver `.pptx`, install the `PPTX` skill first.

### Codex

```bash
npx skills add anthropics/skills -s pptx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s pptx -a claude-code -g -y --full-depth
```

If you no longer need it, run `npx skills list --global` to confirm the name, then remove it with `npx skills remove --global pptx`.

After installing it, open your AI workbench, put the PowerPoint file in the project folder, then use the prompts below.

<h2 id="first-prompt">First Prompt</h2>

```text
Use the PPTX skill to read this PowerPoint file first. Tell me the page count, structure, and topic of each slide. Do not edit it yet: ./deck.pptx
```

For rewriting:

```text
Make this deck better for a 15-minute pitch. Keep the original template style. First propose the new slide structure and titles, then wait for my confirmation before editing the file.
```

<h2 id="tips">Tips</h2>

- If you have a company template, put it in the project folder too
- Say whether the output must be `.pptx` or can be HTML slides
- Confirm the outline before letting the agent rewrite the deck
