---
title: PDF
slug: pdf
order: 5
summary: 处理 PDF 的 skill。适合读取、提取文字和表格、拆分合并、填表和整理资料。
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: 办公文档
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/pdf
---

# PDF

`PDF` skill 适合处理 PDF 文件。

如果你有合同、论文、说明书、账单、扫描件或表单，想让 agent 帮你读取、提取、拆分、合并或填表，这类 skill 更适合。

<h2 id="what-is-it">它解决什么问题</h2>

- 从 PDF 里提取文字和表格
- 合并、拆分或整理 PDF
- 填写 PDF 表单
- 读取长 PDF 并总结结构
- 把 PDF 内容转成可编辑材料

<h2 id="when-use">什么时候用</h2>

优先用 `PDF`：

- 你只有 PDF 文件，没有 Word 原稿
- 你要提取表格、段落或关键信息
- 你要拆分、合并或填表

如果你要把 PDF 内容重新排成好看的报告，后续可以接 [Kami](/docs/skills/kami)。

<h2 id="how-to-use">怎么用</h2>

当你只有 PDF 文件，需要读取、提取、拆分、合并或填表时，先安装 `PDF` skill。

### Codex

```bash
npx skills add anthropics/skills -s pdf -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s pdf -a claude-code -g -y --full-depth
```

装完后，打开你的 AI 工作台，把 PDF 文件放进项目目录，再按下面的方式让 agent 使用。

<h2 id="first-prompt">第一句话</h2>

```text
请使用 PDF skill 读取这个文件，先告诉我目录结构、主要内容和你能提取到哪些表格：./资料.pdf
```

如果你要处理文件：

```text
请把这个 PDF 按章节拆分成多个文件，并给每个文件起一个清楚的文件名。操作前先告诉我拆分计划。
```

<h2 id="tips">小提示</h2>

- 扫描版 PDF 可能需要 OCR，效果取决于清晰度
- 表格提取后要人工检查数字是否错位
- 法律、财务、合同类 PDF 的最终结论必须人工复核
