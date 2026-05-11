---
title: Office Docs
slug: office-docs
order: 1
summary: The entry point for existing Word, Excel, PowerPoint, and PDF files. For new polished artifacts, go to Creation and Design.
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: Office Docs
group_order: 10
---

# Office Docs

This skill group is for existing office files.

You do not need to understand `.docx`, `.xlsx`, `.pptx`, or `.pdf` first. Start with one question:

```text
Do I already have a Word, Excel, PowerPoint, or PDF file that I need the agent to read, edit, organize, or export?
```

<h2 id="choose">How to Choose</h2>

| What you need | Start with |
| --- | --- |
| Edit Word docs, reports, comments, or tracked changes | [DOCX](/docs/skills/docx) |
| Clean Excel data, formulas, charts, or analysis | [XLSX](/docs/skills/xlsx) |
| Edit existing slides, use company templates, output native PowerPoint | [PPTX](/docs/skills/pptx) |
| Read PDFs, extract tables, split, merge, or fill forms | [PDF](/docs/skills/pdf) |

If you are not editing an existing file and want to create a polished artifact from scratch, go to [Skills / Creation and Design](/docs/skills/creation-design). That group fits images, posters, one-pagers, resumes, reports, portfolios, and web-style decks.

<h2 id="office-vs-design">Office Docs vs Creation and Design</h2>

`DOCX / XLSX / PPTX / PDF` are better for existing files: give the agent the file path, explain what to change or extract, and say what formatting should be preserved.

`Kami / Magazine Web PPT / SorryCode Image2` are better for new artifacts: give the topic, audience, material, and style, then let the agent produce something presentable or editable.

<h2 id="first-prompt">First Prompt</h2>

If you already have a file:

```text
Read this file first. Do not edit it yet. Tell me its structure, what looks wrong, and how you suggest handling it: ./material.docx
```

If you are creating from scratch:

```text
I want to create a product introduction for customers. Ask me the necessary questions first, then recommend whether I should use Kami, Magazine Web PPT, or SorryCode Image2.
```

<h2 id="install-note">Install Note</h2>

If you need to work with existing `Word / Excel / PowerPoint / PDF` files, install the matching Office skill first. Without it, the agent may still understand plain text, but it cannot reliably preserve native formatting, comments, formulas, charts, or PDF operations.

Use this order:

1. Install [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code)
2. Install [DOCX](/docs/skills/docx), [XLSX](/docs/skills/xlsx), [PPTX](/docs/skills/pptx), or [PDF](/docs/skills/pdf) for the file type
3. Give the file path and goal to the agent

If you are creating a polished artifact from scratch, start with [Kami](/docs/skills/kami), [Magazine Web PPT](/docs/skills/magazine-web-ppt), or [SorryCode Image2](/docs/skills/sorrycode-image2).
