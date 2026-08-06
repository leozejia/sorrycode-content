---
title: 办公文档
slug: office-docs
order: 1
summary: Word、Excel、PowerPoint、PDF 这类已有办公文件的处理入口。想从零做成品，请去创作与设计。
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: 办公文档
group_order: 10
---

# 办公文档

这组 Skills 用来处理已有的 Word、Excel、PowerPoint 和 PDF 文件。想从零制作一份成品材料，去看[创作与设计](/docs/skills/creation-design)。

<h2 id="choose">怎么选</h2>

| 文件 | 适合的任务 | Skill |
| --- | --- |
| Word `.docx` | 编辑正文、保留格式、处理批注和修订 | `docx` |
| Excel `.xlsx` / `.csv` | 清洗数据、公式、图表和报表 | `xlsx` |
| PowerPoint `.pptx` | 修改已有幻灯片、套公司模板 | `pptx` |
| PDF | 提取文字和表格、拆分、合并或填表 | `pdf` |

<h2 id="install">安装</h2>

先安装 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code)，再按文件类型运行一条命令：

| Skill | Codex | Claude Code |
| --- | --- | --- |
| DOCX | `npx skills add anthropics/skills -s docx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s docx -a claude-code -g -y --full-depth` |
| XLSX | `npx skills add anthropics/skills -s xlsx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s xlsx -a claude-code -g -y --full-depth` |
| PPTX | `npx skills add anthropics/skills -s pptx -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s pptx -a claude-code -g -y --full-depth` |
| PDF | `npx skills add anthropics/skills -s pdf -a codex -g -y --full-depth` | `npx skills add anthropics/skills -s pdf -a claude-code -g -y --full-depth` |

卸载前先运行 `npx skills list --global` 确认名称，再运行 `npx skills remove --global skill-name`。

<h2 id="first-prompt">第一句话</h2>

把文件放进工作目录，并把真实路径告诉 Agent：

```text
请使用 DOCX Skill 读取 ./材料.docx，先不要修改。告诉我文档结构、批注和修订情况，再给出修改建议。
```

```text
请使用 XLSX Skill 读取 ./数据.xlsx，先说明有哪些工作表和字段，再检查公式、空值和重复数据。
```

```text
请使用 PPTX Skill 读取 ./汇报.pptx，保留公司模板，先给出页面结构和修改计划。
```

```text
请使用 PDF Skill 读取 ./资料.pdf，告诉我目录结构、主要内容和可以提取的表格，先不要改文件。
```

<h2 id="check">处理后检查</h2>

- Word 和 PowerPoint 要检查原有格式、批注、修订和模板是否保留
- Excel 要复核公式、数字、工作表和图表引用
- 扫描版 PDF 可能需要 OCR，表格提取后要检查数字是否错位
- 法律、财务、合同和重要经营数据必须由人复核

Skill 来源：[Anthropic Skills](https://github.com/anthropics/skills)。
