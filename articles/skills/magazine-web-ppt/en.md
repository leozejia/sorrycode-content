---
title: Magazine Web PPT
slug: magazine-web-ppt
order: 4
summary: A skill for building editorial magazine-style web presentations as single-file HTML decks.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/op7418/guizang-ppt-skill
---

# Magazine Web PPT

If you specifically need a presentation deck instead of a general document, `Magazine Web PPT` is the second skill worth looking at after `Kami`.

It generates a single-file HTML horizontal deck with an “electronic magazine × electronic ink” visual style. It works well for talks, launches, private salons, industry sharing, and demo days.

<h2 id="what-is-it">What It Is</h2>

- `Magazine Web PPT` is a design-oriented skill for presentation decks
- the output is a single HTML file, not a `.pptx`
- it supports keyboard, wheel, touch, bottom dots, and an `ESC` thumbnail index
- it includes 10 slide layouts and 5 color themes

It comes from Guizang’s open-source `guizang-ppt-skill`. SorryCode documents it as `Magazine Web PPT` so beginners can understand what it is for.

Reference: [guizang-ppt-skill repository](https://github.com/op7418/guizang-ppt-skill)

<h2 id="what-is-good-for">What It Is Good For</h2>

Use it for:

- offline talks or internal industry sharing
- private salons, launches, and demo days
- AI product launches or research presentations
- talks that need a strong personal visual style
- web decks that feel like flipping through an editorial magazine

The 10 built-in layouts cover common talk structures: cover, act divider, data poster, text-image split, image grid, pipeline, suspense question, quote, before/after, and mixed editorial layout.

<h2 id="what-is-not-good-for">What It Is Not Good For</h2>

Do not start here if you need:

- large tables
- high-density training materials
- traditional PowerPoint files for team editing
- general documents, resumes, one-pagers, or portfolios

For general documents, resumes, one-pagers, or portfolios, start with [Skills / Kami](/docs/skills/kami).

If you want to maintain the deck as a React project with comments, browser presentation, and HTML/PDF export, see [Tools / Open Slide](/docs/tools/open-slide).

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

After install, there is no special slash command to remember. Natural language like “make a magazine-style PPT” is enough.

<h2 id="how-to-use">How to Trigger It</h2>

Describe the talk you want to make, not the implementation details.

Try to include:

- topic
- audience
- setting
- duration
- source material
- preferred theme

If you do not provide everything, the skill will ask six clarifying questions first: audience, duration, materials, images, theme, and hard constraints. It should align on outline before generating HTML.

<h2 id="first-prompts">First Prompts</h2>

For a private salon:

```text
Help me make a 20-page magazine-style PPT about how AI changes organizational collaboration. The audience is company leadership, and the talk is a 30-minute private salon. Ask me about audience, materials, images, and theme first, then propose an outline.
```

For turning an article into slides:

```text
Turn the article below into an electronic-magazine-style presentation deck. Use the Indigo Porcelain theme and output a single HTML file.
```

For a product launch:

```text
I need a product launch deck with a cover, 3 acts, a data page, a before/after comparison, and a closing page. I will put images in an images folder.
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

<h2 id="themes">How to Pick a Theme</h2>

It includes 5 color themes:

- Monocle Ink: safe default for general and business talks
- Indigo Porcelain: technology, research, AI, engineering talks
- Forest Ink: nature, sustainability, culture, nonfiction
- Kraft Paper: nostalgic, literary, humanities, indie magazine style
- Dune: art, design, creative, gallery-like content

If you are unsure, choose Monocle Ink.

<h2 id="common-issues">Common Issues</h2>

- `npx`, `node`, or `npm` is missing
  See [Environment / Node.js](/docs/environment/nodejs)
- Does it generate `.pptx` files?
  Not by default. It generates a single-file HTML deck
- Can I use any custom hex color?
  Prefer the 5 built-in themes to keep the visual system stable
- I need a normal document or resume
  Start with [Skills / Kami](/docs/skills/kami)
- I use OpenClaw or Hermes Agent
  The upstream skill can inform other agents, but SorryCode currently verifies `Codex / Claude Code`

<h2 id="references">References</h2>

- Official repository: <https://github.com/op7418/guizang-ppt-skill>
- Public install path: `npx skills add op7418/guizang-ppt-skill`
- Upstream explicitly covers:
  - single-file HTML horizontal decks
  - 10 slide layouts
  - 5 color themes
  - keyboard, wheel, touch, and thumbnail-index interactions
