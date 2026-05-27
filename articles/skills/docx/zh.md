---
title: DOCX
slug: docx
order: 2
summary: 处理 Word 文档的 skill。适合读取、编辑、保留格式、处理批注和修订。
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: 办公文档
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/docx
---

# DOCX

`DOCX` skill 适合处理 Word 文档。

如果你手上已经有 `.docx` 文件，想让 agent 帮你读取、整理、改写、保留格式、处理批注或修订，这类 skill 会读取文档结构，比直接复制正文更适合处理 Word 文件。

<h2 id="what-is-it">它解决什么问题</h2>

- 读取 Word 文档结构
- 修改正文但尽量保留原有格式
- 处理批注、修订、标题层级和段落
- 整理简历、合同、报告、通知、说明书
- 把散乱内容改成正式文档

<h2 id="when-use">什么时候用</h2>

优先用 `DOCX`：

- 你已经有一个 `.docx` 文件
- 你希望改完后仍然是 Word 文档
- 你关心格式、批注、修订或标题结构

如果你是从零做一份好看的成品文档，先看 [Kami](/docs/skills/kami)。

<h2 id="how-to-use">怎么用</h2>

当你已经有 Word 文件，并且希望 agent 保留结构、批注或修订时，先安装 `DOCX` skill。

### Codex

```bash
npx skills add anthropics/skills -s docx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s docx -a claude-code -g -y --full-depth
```

如果不想继续使用，先运行 `npx skills list --global` 确认名称，再用 `npx skills remove --global docx` 卸载。

装完后，打开你的 AI 工作台，把 Word 文件放进项目目录，再按下面的方式让 agent 使用。

<h2 id="first-prompt">第一句话</h2>

```text
请使用 DOCX skill 读取这个 Word 文档，先不要修改。告诉我它的结构、主要问题、以及你建议怎么改：./材料.docx
```

如果你确认要修改：

```text
请在保留原有标题结构和格式的前提下，把这份 Word 文档改得更适合发给客户。修改前先列出你准备改哪些部分。
```

<h2 id="tips">小提示</h2>

- 先让 agent 读取和诊断，不要一上来直接改
- 明确告诉它要不要保留格式、批注、修订记录
- 重要合同、报价或法律文件，改完仍需要人工复核
