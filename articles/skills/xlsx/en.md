---
title: XLSX
slug: xlsx
order: 3
summary: A skill for Excel workbooks: data cleaning, formulas, charts, analysis, and reporting.
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: Office Docs
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/xlsx
---

# XLSX

The `XLSX` skill is for Excel workbooks.

If you have `.xlsx`, `.csv`, or tabular data and want an agent to clean, analyze, add formulas, create charts, or organize reports, this is steadier than pasting a table into chat.

<h2 id="what-is-it">What It Helps With</h2>

- Reading workbooks and multiple sheets
- Cleaning data, normalizing fields, handling blanks and duplicates
- Adding formulas, summaries, pivot-style views, and charts
- Working with sales, operations, finance, or user data
- Turning raw spreadsheets into report-ready structure

<h2 id="when-use">When to Use It</h2>

Use `XLSX` first when:

- you already have an Excel or CSV file
- formulas and spreadsheet structure matter
- you need data cleaning, analysis, or charts

If you want to turn the analysis into a polished report, use [Kami](/docs/skills/kami) afterward.

<h2 id="how-to-use">How to Use</h2>

When you already have Excel, CSV, or tabular data and need the agent to preserve spreadsheet structure, formulas, or charts, install the `XLSX` skill first.

### Codex

```bash
npx skills add anthropics/skills -s xlsx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s xlsx -a claude-code -g -y --full-depth
```

After installing it, open your AI workbench, put the Excel or CSV file in the project folder, then use the prompts below.

<h2 id="first-prompt">First Prompt</h2>

```text
Use the XLSX skill to read this Excel file first. Tell me what sheets it has and what each sheet appears to contain. Do not edit it yet: ./data.xlsx
```

For analysis:

```text
Analyze this sales spreadsheet. Find the highest-revenue products, fastest-growing channels, and suspicious outliers. Show me the analysis plan first, then create the result table.
```

<h2 id="tips">Tips</h2>

- Ask the agent to explain the workbook before changing formulas or charts
- Review important finance data manually
- If the file is large, say which sheet and fields matter most
