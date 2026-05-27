---
title: Kami
slug: kami
order: 3
summary: A design-focused skill for finished documents. Use it for one-pagers, long docs, resumes, portfolios, and slide decks.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/tw93/kami
---

# Kami

If you do not want flat output that looks like ordinary markdown and you want something closer to a finished document, resume, portfolio, or slide deck, `Kami` is the best first skill to install right now.

It works well for first-time users because it does not ask you to learn design jargon first. You describe the result you want, and it applies a stable paper-like design language for you.

<h2 id="what-is-kami">What Kami Is</h2>

- `Kami` is a design-focused skill for finished documents
- it covers one-pagers, long docs, formal letters, portfolios, resumes, and slide decks
- it supports Chinese and English, with a best-effort Japanese path
- it can place inline SVG charts such as bar, line, donut, timeline, tree, and waterfall charts directly into the document

More importantly, it is not just random formatting. It uses one consistent visual system, so repeated outputs feel more stable and more intentional.

Reference: [Kami official repository](https://github.com/tw93/kami)

<h2 id="what-is-good-for">What It Is Good For</h2>

Use it first for these cases:

- turn your product intro into a one-pager
- turn notes or research into a proper long document
- build a more polished resume
- build a project portfolio
- turn an outline into a slide deck quickly
- create more structured professional documents such as changelogs and equity reports

If your current goal is PPT work, this page is still the right start. For now, we use Kami's slide capability directly instead of splitting that into a second skill.

<h2 id="one-click-install">One-Click Install</h2>

These are the upstream install commands verified by SorryCode.

### Codex

```bash
npx skills add tw93/kami -a codex -g -y
```

### Claude Code

```bash
npx skills add tw93/kami -a claude-code -g -y
```

If your runtime is not ready yet, go back first:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

If you no longer need it, run `npx skills list --global` to confirm the name, then remove it with `npx skills remove --global kami`.

After install, you do not need to remember a slash command. `Kami` auto-triggers when you describe what you need.

<h2 id="how-to-use">How to Trigger It</h2>

Use natural language, not parameter hunting.

The best prompt shape is:

- what final artifact you want
- who it is for
- what language to use
- whether there is a fixed structure
- if it is slides, how many pages or what outline to follow

If you need charts, include the data and chart type directly in your prompt.

<h2 id="first-prompts">What to Say First</h2>

If you want to test documents first:

```text
Turn this product introduction into a one-pager for first-time customers, in English, with a calm professional tone.
```

If you want to test slides first:

```text
Build a 6-slide deck from the outline below for a live talk. Keep it professional and easy to follow.
```

If you want to test charts:

```text
Turn this into a long document and add a revenue breakdown donut chart plus a user growth line chart.
```

<h2 id="common-issues">Common Issues</h2>

- `npx` or `node` is missing
  start with [Environment / Node.js](/docs/environment/nodejs)
- `npm` is missing
  start with [Environment / Node.js](/docs/environment/nodejs)
- it is installed but I do not know how to call it
  describe the result you want in plain language and let Kami trigger itself
- I want to make PPT, do I need another skill
  not right now, start with `Kami`
- I use another agent
  Kami also documents a generic-agents path, but our current docs verify `Codex / Claude Code` first

<h2 id="references">References</h2>

- Official repository: <https://github.com/tw93/kami>
- The official docs explicitly list support for:
  - one-pagers
  - long docs
  - formal letters
  - portfolios
  - resumes
  - slide decks
  - changelogs
  - equity reports
  - multiple SVG diagram types
