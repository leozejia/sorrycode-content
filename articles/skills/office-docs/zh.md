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

这是给已有办公文件准备的一组 skills。

你不用先理解 `.docx`、`.xlsx`、`.pptx`、`.pdf` 的技术差异。先确认手里有没有现成文件：

```text
我是不是已经有一个 Word、Excel、PowerPoint 或 PDF 文件，需要 agent 帮我读、改、整理或导出？
```

<h2 id="choose">怎么选</h2>

| 你要做什么 | 优先看 |
| --- | --- |
| 改 Word、整理报告、处理批注和修订 | [DOCX](/docs/skills/docx) |
| 整理 Excel、清洗表格、公式和图表 | [XLSX](/docs/skills/xlsx) |
| 修改已有 PPT、套用公司模板、输出原生 PowerPoint | [PPTX](/docs/skills/pptx) |
| 读取 PDF、提取表格、拆分合并、填表 | [PDF](/docs/skills/pdf) |

如果你不是在处理已有文件，而是想从零做一份能发给别人看的材料，去 [Skills / 创作与设计](/docs/skills/creation-design)。那里更适合图片、海报、一页纸、简历、报告、作品集和网页 PPT。

<h2 id="office-vs-design">办公文档和创作设计的区别</h2>

`DOCX / XLSX / PPTX / PDF` 更适合处理已有文件：你把文件路径给 agent，告诉它要改哪里、提取什么、保留什么格式。

`Kami / Magazine Web PPT / SorryCode Image2` 更适合从零做成品：你给主题、受众、素材和风格，让 agent 直接做出一份可以展示或继续修改的材料。

<h2 id="first-prompt">第一句话可以怎么说</h2>

如果你有现成文件：

```text
请先读取这个文件，不要立刻改。告诉我它的结构、有什么问题、你建议怎么处理：./材料.docx
```

如果你要从零生成：

```text
我想做一份面向客户的产品介绍。先问我必要问题，再建议应该用 Kami、Magazine Web PPT 还是 SorryCode Image2。
```

<h2 id="install-note">安装说明</h2>

如果你要处理已有 `Word / Excel / PowerPoint / PDF` 文件，需要先安装对应的 Office skill。没有安装时，agent 可能只能做普通文本理解，不能稳定保留原生格式、批注、公式、图表或 PDF 操作。

默认顺序是：

1. 先安装 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code)
2. 再按任务安装 [DOCX](/docs/skills/docx)、[XLSX](/docs/skills/xlsx)、[PPTX](/docs/skills/pptx) 或 [PDF](/docs/skills/pdf)
3. 把文件路径和目标交给 agent

如果你是从零生成一份好看的成品材料，可以先看 [Kami](/docs/skills/kami)、[Magazine Web PPT](/docs/skills/magazine-web-ppt) 或 [SorryCode Image2](/docs/skills/sorrycode-image2)。
