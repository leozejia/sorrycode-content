---
title: 创作与设计
slug: creation-design
order: 1
summary: 图片、海报、一页纸、简历、报告、作品集和演示表达的入口。先判断你要生成图片、处理内容，还是做 PPT / slides。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
---

# 创作与设计

这是给成品表达准备的一组 skills。

如果你想让 agent 直接做出一张图、一份材料或一套演示，而不是只给你一段文字，先从这里选。

如果你第一次做 PPT、设计、图片、一页纸或封面，可以先读 [设计类 Skills 怎么用](/docs/skills/design-workflow)。这类产物通常需要几轮判断和修改，先得到可修改的初稿，再通过具体反馈逐步靠近你要的结果。

<h2 id="choose">怎么选</h2>

| 你要做什么 | 优先看 |
| --- | --- |
| 生成封面、海报、插图、产品视觉或 2D 游戏素材 | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| 做一页纸、简历、报告、白皮书、作品集或纸面风幻灯片 | [Kami](/docs/skills/kami) |
| 快速生成有明确视觉风格的网页演示 | [藏师傅的 PPT Skill](/docs/skills/magazine-web-ppt) |
| 做可评论、可维护、可导出 HTML/PDF 的代码式 PPT | [工具 / Open Slide](/docs/tools/open-slide) |
| 做产品短视频、发布动效或社媒 MP4 | [工具 / HyperFrames](/docs/tools/hyperframes) |
| 做 App 原型、动效、信息图、设计变体或专家评审 | [Huashu Design](/docs/skills/huashu-design) |
| 想让一个项目长期保持同一套视觉规则 | [Agent 基建 / DESIGN.md](/docs/agent-infra/design-md) |

<h2 id="office-vs-design">它和办公文档的区别</h2>

[办公文档](/docs/skills/office-docs) 处理的是已有文件，比如改一个 Word、整理一个 Excel、修改一个 PowerPoint、拆分一个 PDF。

`创作与设计` 处理的是成品表达：你给主题、受众、素材和风格，让 agent 生成可以展示、发布或继续修改的结果。

<h2 id="presentation-route">演示 / PPT 交付路线</h2>

PPT 不是一种单一工具，而是一种交付形态。先看最终要交付什么：

| 你真正需要的是 | 优先看 |
| --- | --- |
| 修改已有 PowerPoint、套公司模板、最终交付 `.pptx` | [PPTX](/docs/skills/pptx) |
| 快速做一套有明确视觉风格的网页演示 | [藏师傅的 PPT Skill](/docs/skills/magazine-web-ppt) |
| 把文章、报告、简历或作品集整理成纸面风材料 | [Kami](/docs/skills/kami) |
| 做 App 原型、发布视觉、信息图、动效感 PPT 或专家评审 | [Huashu Design](/docs/skills/huashu-design) |
| 做可维护、可评论、可导出 HTML/PDF 的代码式 deck | [工具 / Open Slide](/docs/tools/open-slide) |
| 做演示视频、发布动效或社媒 MP4 | [工具 / HyperFrames](/docs/tools/hyperframes) |

第一次只是想做一套分享稿，可以直接走 [新手村 / 做一套分享 PPT](/docs/village/share-ppt)。那里会给默认路径，不展开完整比较。

<h2 id="first-prompt">第一句话可以怎么说</h2>

如果你还不知道该用哪个 skill，可以直接问 agent：

```text
我想做一个可以发给别人的成品材料。请先判断我应该用 SorryCode Image2、Kami、藏师傅的 PPT Skill、PPTX、Huashu Design 还是 Open Slide，再问我必要问题。
```

如果你已经知道要做图片：

```text
请用 SorryCode Image2 生成一张公众号封面，主题是 AI 编程入门，中文标题清晰，保存到 outputs/images/cover/。
```

如果你要做一页纸：

```text
请用 Kami 把下面这段产品介绍做成一页纸，面向第一次了解我们的客户。先问我必要问题，再开始排版。
```

<h2 id="install-note">安装说明</h2>

先安装 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code)，再按任务安装对应 skill。

如果你只是第一次尝试，建议顺序是：

1. 先装 [SorryCode Image2](/docs/skills/sorrycode-image2)，生成第一张图
2. 再装 [Kami](/docs/skills/kami)，做一份一页纸
3. 需要演讲展示时，再看 [演示 / PPT 交付路线](#presentation-route)
4. 需要代码式 PPT 或视频工具链时，再看 [Open Slide](/docs/tools/open-slide) 和 [HyperFrames](/docs/tools/hyperframes)
5. 需要 App 原型、动效或复杂设计交付时，再看 [Huashu Design](/docs/skills/huashu-design)

如果你想研究完整设计工作台，而不是只安装一个 skill，可以看 [工具 / Open Design](/docs/tools/open-design)。
