---
title: PDF
slug: pdf
order: 5
summary: A skill for PDFs: reading, extracting text and tables, splitting, merging, filling forms, and organizing material.
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: Office Docs
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/pdf
---

# PDF

The `PDF` skill is for PDF files.

If you have contracts, papers, manuals, invoices, scans, or forms, and want an agent to read, extract, split, merge, or fill them, this is the right direction.

<h2 id="what-is-it">What It Helps With</h2>

- Extracting text and tables from PDFs
- Merging, splitting, or organizing PDFs
- Filling PDF forms
- Reading long PDFs and summarizing structure
- Turning PDF content into editable material

<h2 id="when-use">When to Use It</h2>

Use `PDF` first when:

- you only have a PDF, not the original Word file
- you need tables, paragraphs, or key information extracted
- you need to split, merge, or fill forms

If you want to turn PDF content into a polished report, use [Kami](/docs/skills/kami) afterward.

<h2 id="how-to-use">How to Use</h2>

When you only have a PDF file and need reading, extraction, splitting, merging, or form filling, install the `PDF` skill first.

### Codex

```bash
npx skills add anthropics/skills -s pdf -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s pdf -a claude-code -g -y --full-depth
```

After installing it, open your AI workbench, put the PDF file in the project folder, then use the prompts below.

<h2 id="first-prompt">First Prompt</h2>

```text
Use the PDF skill to read this file. First tell me its structure, main content, and which tables you can extract: ./material.pdf
```

For file operations:

```text
Split this PDF by chapter and give each output file a clear filename. Tell me the split plan before doing it.
```

<h2 id="tips">Tips</h2>

- Scanned PDFs may need OCR, and quality depends on image clarity
- Check extracted table numbers manually
- Legal, finance, and contract conclusions still need human review
