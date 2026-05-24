---
title: DOCX
slug: docx
order: 2
summary: A skill for Word documents: reading, editing, preserving formatting, comments, and tracked changes.
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: Office Docs
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/docx
---

# DOCX

The `DOCX` skill is for Word documents.

If you already have a `.docx` file and want an agent to read, organize, edit, preserve formatting, handle comments, or work with tracked changes, this is steadier than pasting the text into chat.

<h2 id="what-is-it">What It Helps With</h2>

- Reading Word document structure
- Editing content while preserving formatting where possible
- Handling comments, tracked changes, headings, and paragraphs
- Working on resumes, contracts, reports, notices, and manuals
- Turning rough material into a formal document

<h2 id="when-use">When to Use It</h2>

Use `DOCX` first when:

- you already have a `.docx` file
- the final output should still be a Word document
- formatting, comments, tracked changes, or headings matter

If you are creating a polished document from scratch, start with [Kami](/docs/skills/kami).

<h2 id="how-to-use">How to Use</h2>

When you already have a Word file and need the agent to preserve structure, comments, or tracked changes, install the `DOCX` skill first.

### Codex

```bash
npx skills add anthropics/skills -s docx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s docx -a claude-code -g -y --full-depth
```

If you no longer need it, run `npx skills list --global` to confirm the name, then remove it with `npx skills remove --global docx`.

After installing it, open your AI workbench, put the Word file in the project folder, then use the prompts below.

<h2 id="first-prompt">First Prompt</h2>

```text
Use the DOCX skill to read this Word document first. Do not edit it yet. Tell me its structure, main issues, and how you suggest improving it: ./material.docx
```

When you are ready to edit:

```text
Edit this Word document so it is more suitable for customers. Preserve the original heading structure and formatting where possible. List the planned changes before editing.
```

<h2 id="tips">Tips</h2>

- Ask the agent to read and diagnose before editing
- Say whether formatting, comments, or tracked changes should be preserved
- Review important contracts, quotes, or legal documents manually
