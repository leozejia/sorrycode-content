# 演示 / PPT 交付路线

更新时间：2026-08-06

这份文档定义 SorryCode 如何组织 PPT、slides 和演示表达相关内容。它是内部治理文档，不进入线上 docs。

## 核心判断

PPT 是一种交付形态。用户说“做 PPT”时，可能需要修改已有 `.pptx`、生成网页演示、整理报告，或者制作可导出的代码式 deck。

公开文档不把某个 skill 写成唯一方案。路线图负责分流，具体 skill 和工具页面只讲自己的能力。

PPT 需要反复修改。公开表达应强调从可修改初稿开始，再通过具体反馈逐步调整，不承诺一句话产出最终成品。

## 路线图

| 需求 | 默认入口 | 页面位置 |
| --- | --- | --- |
| 修改已有 PowerPoint、套公司模板、交付 `.pptx` | `PPTX` | `Skills / 办公文档` |
| 生成有明确视觉风格的网页演示 | `藏师傅的 PPT Skill` | `Skills / 创作与设计` |
| 把报告、简历或作品集排成纸面风 slides | `Kami` | `Skills / 创作与设计` |
| 制作可维护、可评论、可导出的代码式 deck | `Open Slide` | `Tools` |
| 制作演示视频、发布动效或社媒 MP4 | `HyperFrames` | `Tools` |

新工具加入对应路线，不重复改写其他入口页。当前公开页面和路由以根 `index.json` 及 section index 为准。

## 藏师傅的 PPT Skill

上游是 `op7418/guizang-ppt-skill`，站内标题保留作者名称。它适合由 agent 生成具有明确设计系统的单文件 HTML 横向翻页 PPT。

单页只维护长期稳定的信息：适合与不适合的任务、安装、触发、与其他路线的选择，以及最近验证口径。具体版式、主题和校验能力以官方仓库为准。

## Kami

Kami 的主要任务是排版成品。它适合把文字、访谈、报告、简历、白皮书和作品集整理成克制的可交付材料。用于 slides 时，它更接近纸面文档的演示版。

Kami 可以进入演示路线图，但单页仍按自己的核心能力写，不改名为 PPT skill。

## 页面分工

`藏师傅的 PPT Skill` 可以作为第一次制作网页演示的默认路径。`Skills / 创作与设计` 承担路线分流，单个 skill 页面只保留一小段选择说明。

设计类页面应链接到 `Skills / 创作与设计`，帮助用户区分质量问题、场景要求和个人偏好。高频偏好可以沉淀到 `DESIGN.md`、references 或用户自己的 skill。

调整名称、slug、目录或栏目时，按 `docs/information-architecture.md` 的硬切原则和 `docs/operator-restructuring-guide.md` 的执行清单处理。
