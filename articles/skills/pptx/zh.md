---
title: PPTX
slug: pptx
order: 4
summary: 处理 PowerPoint 原生文件的 skill。适合修改已有 PPT、套模板、整理汇报材料和路演稿。
section: skills
section_title: Skills
section_order: 15
group: office-docs
group_title: 办公文档
group_order: 10
source_url: https://github.com/anthropics/skills/tree/main/skills/pptx
---

# PPTX

`PPTX` skill 适合处理 PowerPoint 原生文件。

如果你已经有 `.pptx` 模板、公司汇报材料、路演稿或课程课件，想让 agent 帮你改结构、统一文字、整理页面，这类 skill 更适合。

<h2 id="what-is-it">它解决什么问题</h2>

- 读取已有 PowerPoint 文件
- 修改页面文字和结构
- 统一标题、章节和表达方式
- 按已有模板整理汇报材料
- 把长文或提纲变成原生 `.pptx`

<h2 id="when-use">什么时候用</h2>

优先用 `PPTX`：

- 你需要最终产物是 `.pptx`
- 你有公司模板或已有 PPT
- 你要继续用 PowerPoint 编辑

如果你想从零做一套有明确视觉风格的网页演示，先看 [藏师傅的 PPT Skill](/docs/skills/magazine-web-ppt)。如果你想从零做一套纸面设计风幻灯片，也可以看 [Kami](/docs/skills/kami)。

<h2 id="how-to-use">怎么用</h2>

当你已经有 PowerPoint 文件、公司模板或必须交付 `.pptx` 时，先安装 `PPTX` skill。

### Codex

```bash
npx skills add anthropics/skills -s pptx -a codex -g -y --full-depth
```

### Claude Code

```bash
npx skills add anthropics/skills -s pptx -a claude-code -g -y --full-depth
```

装完后，打开你的 AI 工作台，把 PowerPoint 文件放进项目目录，再按下面的方式让 agent 使用。

<h2 id="first-prompt">第一句话</h2>

```text
请使用 PPTX skill 读取这份 PowerPoint，先告诉我页数、结构和每页主题，不要立刻修改：./汇报.pptx
```

如果你要重写：

```text
请把这份 PPT 改得更适合 15 分钟路演。保留原模板风格，先给我新的页结构和每页标题，确认后再修改文件。
```

<h2 id="tips">小提示</h2>

- 如果有公司模板，先把模板文件也放进项目目录
- 明确最终要 `.pptx`，还是可以接受网页 HTML 幻灯片
- 修改前先确认大纲，避免 agent 直接大改页面
