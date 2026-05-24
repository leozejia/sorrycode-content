---
title: Open Slide
slug: open-slide
order: 5
summary: A tool for creating React slide decks with Codex or Claude Code. Useful for code-based decks, comments, presentation mode, and HTML/PDF export.
section: tools
section_title: Tools
section_order: 28
source_url: https://github.com/1weiho/open-slide
---

# Open Slide

`Open Slide` is an agent-first slide tool.

Think of it as a way to build a React deck with Codex or Claude Code. It is not traditional PowerPoint, and it is not one global skill. It initializes a deck project so the agent can edit slides, themes, and content inside that workspace.

<h2 id="when-to-use">When to Use It</h2>

Use it for:

- technical talks, product pitches, course decks, and demo days
- decks you want to keep as code and revise over time
- comment-based slide revisions
- browser presentation mode and HTML/PDF export
- users comfortable with a project folder and a local dev server

If you are making your first deck, start with [Guizang PPT Skill](/docs/skills/magazine-web-ppt). If you must edit an existing `.pptx`, start with [PPTX](/docs/skills/pptx).

<h2 id="how-it-works">How It Works</h2>

Open Slide starts by initializing a project:

```bash
npx @open-slide/cli init my-deck
cd my-deck
codex
```

The project includes instructions and workspace skills for the agent. You do not need to memorize them first, but they explain how the workflow works:

- `/create-slide`: create slides
- `/slide-authoring`: author and organize slides
- `/apply-comments`: apply comments and revisions
- `/create-theme`: create themes

<h2 id="first-prompt">First Prompt</h2>

Inside `my-deck`, tell Codex or Claude Code:

```text
Use Open Slide to make an 8-page sharing deck about how I use AI to improve my workflow. Ask me about the audience, duration, visual style, and materials first, then propose the outline. Do not generate the final pages yet.
```

If you already have an outline:

```text
Read this Open Slide project and turn the outline below into a 10-page deck. Propose the page structure and titles first; write code only after I confirm.
```

<h2 id="how-to-choose">How to Choose</h2>

| Need | Start with |
| --- | --- |
| Edit an existing PowerPoint file | [PPTX](/docs/skills/pptx) |
| Quickly make a web deck with a strong visual system | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |
| Make a polished artifact or paper-style slides from scratch | [Kami](/docs/skills/kami) |
| Build a code-based deck with comments and HTML/PDF export | `Open Slide` |

<h2 id="not-for">When Not to Use It</h2>

Do not start here if:

- you must deliver a company PowerPoint template
- you want one prompt to produce a basic slide deck immediately
- you do not want to deal with a project folder, CLI, or local server
- you are making a long document, resume, or one-pager

<h2 id="references">References</h2>

- Repository: <https://github.com/1weiho/open-slide>
- Docs: <https://open-slide.dev/docs>
- Agent overview: <https://open-slide.dev/docs/agents/overview>
