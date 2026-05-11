---
title: Open Slide
slug: open-slide
order: 5
summary: 用 Codex 或 Claude Code 写 React 幻灯片的工具。适合代码式 deck、评论修改、演讲预览和 HTML/PDF 导出。
section: tools
section_title: 工具
section_order: 28
source_url: https://github.com/1weiho/open-slide
---

# Open Slide

`Open Slide` 是一个 agent-first 的幻灯片工具。

你可以把它理解成：用 Codex 或 Claude Code 写一套 React 幻灯片。它不是普通 PowerPoint，也不是单个全局 skill；它会初始化一个 deck 项目，让 agent 在项目里写页面、主题和内容。

<h2 id="when-to-use">什么时候用它</h2>

适合这些场景：

- 技术分享、产品路演、课程演示、demo day
- 想用代码维护一套可以反复修改的 deck
- 想让 agent 按评论继续改幻灯片
- 想在浏览器里演讲，并导出 HTML 或 PDF
- 能接受一个项目目录和本地开发服务

如果你只是第一次做 PPT，先看 [Magazine Web PPT](/docs/skills/magazine-web-ppt)。如果你必须修改已有 `.pptx` 文件，先看 [PPTX](/docs/skills/pptx)。

<h2 id="how-it-works">它怎么工作</h2>

Open Slide 的入口是初始化一个项目：

```bash
npx @open-slide/cli init my-deck
cd my-deck
codex
```

项目里会准备给 agent 看的说明和 workspace skills。你不用先背这些名字，但知道它们存在会更容易理解：

- `/create-slide`：创建幻灯片
- `/slide-authoring`：写和组织 slide
- `/apply-comments`：根据评论修改
- `/create-theme`：创建主题

<h2 id="first-prompt">第一句话</h2>

进入 `my-deck` 后，可以对 Codex 或 Claude Code 说：

```text
请用 Open Slide 帮我做一套 8 页分享 deck，主题是我如何用 AI 改造工作流。先问我受众、演讲时长、视觉风格和素材，再给大纲，不要直接生成最终页面。
```

如果你已经有提纲：

```text
请读取这个 Open Slide 项目，把下面的提纲改成 10 页 deck。先给页面结构和每页标题，确认后再写代码。
```

<h2 id="how-to-choose">和其他 PPT 能力怎么选</h2>

| 需求 | 优先看 |
| --- | --- |
| 改已有 PowerPoint 文件 | [PPTX](/docs/skills/pptx) |
| 快速做一套杂志风网页 PPT | [Magazine Web PPT](/docs/skills/magazine-web-ppt) |
| 从零做一份成品材料或纸面风幻灯片 | [Kami](/docs/skills/kami) |
| 做复杂设计、动效或可编辑 PPTX | [Huashu Design](/docs/skills/huashu-design) |
| 做可维护、可评论、可导出 HTML/PDF 的代码式 deck | `Open Slide` |

<h2 id="not-for">不适合什么</h2>

这些场景先不要用 Open Slide：

- 你必须交付公司 PowerPoint 模板
- 你只想复制一句话马上得到普通 PPT
- 你不想看到项目目录、命令行或本地服务
- 你要做长文档、简历、一页纸

<h2 id="references">参考</h2>

- 官方仓库：<https://github.com/1weiho/open-slide>
- 官方文档：<https://open-slide.dev/docs>
- Agent 说明：<https://open-slide.dev/docs/agents/overview>
