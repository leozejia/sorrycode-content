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

These Skills work with existing Word, Excel, PowerPoint, and PDF files. To create a new polished artifact, see [Creation and Design](/docs/skills/creation-design).

<h2 id="choose">How to Choose</h2>

| File | Good for | Skill |
| --- | --- |
| Word `.docx` | Editing text, preserving formatting, comments, and tracked changes | `docx` |
| Excel `.xlsx` / `.csv` | Cleaning data, formulas, charts, and reports | `xlsx` |
| PowerPoint `.pptx` | Editing existing slides and company templates | `pptx` |
| PDF | Extracting text and tables, splitting, merging, and filling forms | `pdf` |

<h2 id="install">Install</h2>

Install [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code), then run one command for the file type:

| Skill | Codex | Claude Code |
| --- | --- | --- |
| DOCX | `npx skills add anthropics/skills -s docx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s docx -a claude-code -g -y --full-depth` |
| XLSX | `npx skills add anthropics/skills -s xlsx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s xlsx -a claude-code -g -y --full-depth` |
| PPTX | `npx skills add anthropics/skills -s pptx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s pptx -a claude-code -g -y --full-depth` |
| PDF | `npx skills add anthropics/skills -s pdf -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s pdf -a claude-code -g -y --full-depth` |

Before removing a Skill, run `npx skills list --global` to confirm its name, then run `npx skills remove --global skill-name`.

<h2 id="first-prompt">First Prompt</h2>

Put the file in the workspace and give the agent its real path:

```text
Use the DOCX Skill to read ./material.docx. Do not edit it yet. Describe the document structure, comments, and tracked changes, then suggest edits.
```

```text
Use the XLSX Skill to read ./data.xlsx. List the sheets and fields first, then check formulas, missing values, and duplicates.
```

```text
Use the PPTX Skill to read ./report.pptx. Keep the company template and give me the slide structure and edit plan first.
```

```text
Use the PDF Skill to read ./reference.pdf. Tell me its structure, main content, and which tables can be extracted. Do not change the file yet.
```

<h2 id="check">Check the Result</h2>

- Check that Word and PowerPoint formatting, comments, tracked changes, and templates remain intact
- Verify Excel formulas, numbers, sheets, and chart references
- Scanned PDFs may need OCR, and extracted tables need a manual number check
- A person must review legal, financial, contract, and important business data

Skill source: [Anthropic Skills](https://github.com/anthropics/skills).
