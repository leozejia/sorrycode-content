---
title: XLSX
slug: xlsx
order: 3
summary: 处理 Excel 表格的 skill。适合数据清洗、公式、图表、经营分析和报表整理。
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: 办公文档
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/xlsx
---

# XLSX

`XLSX` skill 适合处理 Excel 表格。

如果你有 `.xlsx`、`.csv` 或表格数据，想让 agent 帮你清洗、分析、补公式、做图表或整理报表，这类 skill 会保留表格结构，比直接把表格复制到聊天框更适合处理工作簿。

<h2 id="what-is-it">它解决什么问题</h2>

- 读取 Excel 工作簿和多个 sheet
- 清洗数据、统一字段、处理空值和重复项
- 增加公式、汇总、透视视角和图表
- 整理销售、运营、财务、用户数据
- 把原始表格改成更适合汇报的结构

<h2 id="when-use">什么时候用</h2>

优先用 `XLSX`：

- 你已经有 Excel 文件或 CSV 文件
- 你希望保留表格结构和公式
- 你要做经营分析、数据清洗或图表

如果你要把分析结果排成正式报告，后续可以接 [Kami](/docs/skills/kami)。

<h2 id="how-to-use">怎么用</h2>

当你已经有 Excel、CSV 或表格数据，并且希望 agent 保留表格结构、公式或图表时，先安装 `XLSX` skill。

### Codex

```bash
npx skills add anthropics/skills -s xlsx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s xlsx -a claude-code -g -y --full-depth
```

如果不想继续使用，先运行 `npx skills list --global` 确认名称，再用 `npx skills remove --global xlsx` 卸载。

装完后，打开你的 AI 工作台，把 Excel 或 CSV 文件放进项目目录，再按下面的方式让 agent 使用。

<h2 id="first-prompt">第一句话</h2>

```text
请使用 XLSX skill 读取这个 Excel 文件，先告诉我有哪些 sheet、每个 sheet 大概是什么数据，不要立刻修改：./数据.xlsx
```

如果你要分析：

```text
请帮我分析这份销售表，找出销售额最高的产品、增长最快的渠道和异常数据。先给分析计划，再生成结果表。
```

<h2 id="tips">小提示</h2>

- 先让 agent 解释表格结构，再让它改公式或图表
- 重要财务数据要人工复核
- 如果表很大，先说明你最关心哪个 sheet 和哪些字段
