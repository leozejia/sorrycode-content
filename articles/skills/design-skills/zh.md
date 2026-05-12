---
title: 为什么设计类 Skills 特殊
slug: design-skills
order: 6
summary: 设计类 skills 不是让 agent 多写几句审美词，而是把风格、约束、素材和交付标准固定下来。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
---

# 为什么设计类 Skills 特殊

设计类任务很容易失控。

你让 agent 做一张封面、一页纸、网页 PPT 或产品视觉，它不只要理解文字，还要处理风格、层级、留白、配色、素材、导出格式和修改轮次。只靠一句“做得高级一点”，结果通常不稳定。

设计类 skill 的作用，是把这些容易漂移的要求提前写进工作流。

<h2 id="what-changes">装了以后有什么不同</h2>

普通提示词通常只告诉 agent 这次要做什么。设计类 skill 会额外告诉 agent：

- 开始前应该问哪些问题
- 默认采用什么视觉语言
- 哪些排版和配色不要碰
- 素材应该放在哪里
- 最后应该输出什么文件
- 失败时应该怎么继续修改

这也是为什么 `Kami`、`藏师傅的 PPT Skill`、`SorryCode Image2`、`Huashu Design` 这类 skill 更适合做成品，而不是每次从零写一长串提示词。

<h2 id="when-use">什么时候该用</h2>

优先用设计类 skill：

- 你要生成封面、海报、文章配图或产品视觉
- 你要把一段内容做成一页纸、简历、报告或作品集
- 你要做一套能展示的网页 PPT
- 你要做 App 原型、动效、信息图或设计变体
- 你希望多次生成保持同一种风格
- 你希望 agent 保存文件，而不是只在聊天里给一段文字

如果你只是要改一个已有 Word、Excel、PowerPoint 或 PDF 文件，先看 [Skills / 办公文档](/docs/skills/office-docs)。

<h2 id="first-prompt">第一句话可以怎么说</h2>

做图片：

```text
请用 SorryCode Image2 生成一张公众号封面，主题是 AI 编程入门，暖色调，中文标题清晰，保存到 outputs/images/cover/。
```

做文档：

```text
请用 Kami 把下面这段产品介绍做成一页纸，面向第一次了解我们的客户。先问我必要问题，再开始排版。
```

做演示：

```text
请用藏师傅的 PPT Skill 做一套 12 页左右的产品发布会网页演示。先判断适合电子杂志风还是瑞士风，再给大纲，不要直接生成最终文件。
```

<h2 id="design-md">更进一步：把设计要求写下来</h2>

如果你已经有品牌色、字体、页面风格、参考案例或禁用规则，可以把它们整理成 `DESIGN.md`。

`DESIGN.md` 不是 skill，而是设计 agent 的上下文文件。下一篇看：[Agent 基建 / DESIGN.md](/docs/agent-infra/design-md)。

如果你想看一个完整设计工作台如何组合 `SKILL.md + DESIGN.md + artifact preview`，可以看 [工具 / Open Design](/docs/tools/open-design)。
