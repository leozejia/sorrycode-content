---
title: 创作与设计
slug: creation-design
order: 1
summary: 图片、海报、一页纸、简历、报告、作品集和网页 PPT 的入口。先判断你要生成图片，还是做成品表达。
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

<h2 id="choose">怎么选</h2>

| 你要做什么 | 优先看 |
| --- | --- |
| 生成封面、海报、插图、产品视觉或 2D 游戏素材 | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| 做一页纸、简历、报告、白皮书、作品集或纸面风幻灯片 | [Kami](/docs/skills/kami) |
| 做网页风、杂志风演讲幻灯片 | [Magazine Web PPT](/docs/skills/magazine-web-ppt) |
| 做可评论、可维护、可导出 HTML/PDF 的代码式 PPT | [工具 / Open Slide](/docs/tools/open-slide) |
| 做产品短视频、发布动效或社媒 MP4 | [工具 / HyperFrames](/docs/tools/hyperframes) |
| 做 App 原型、动效、信息图、设计变体或专家评审 | [Huashu Design](/docs/skills/huashu-design) |
| 想理解为什么设计类 skill 更稳定 | [为什么设计类 Skills 特殊](/docs/skills/design-skills) |
| 想让一个项目长期保持同一套视觉规则 | [Agent 基建 / DESIGN.md](/docs/agent-infra/design-md) |

<h2 id="office-vs-design">它和办公文档的区别</h2>

[办公文档](/docs/skills/office-docs) 处理的是已有文件，比如改一个 Word、整理一个 Excel、修改一个 PowerPoint、拆分一个 PDF。

`创作与设计` 处理的是成品表达：你给主题、受众、素材和风格，让 agent 生成可以展示、发布或继续修改的结果。

<h2 id="first-prompt">第一句话可以怎么说</h2>

如果你还不知道该用哪个 skill，可以直接问 agent：

```text
我想做一个可以发给别人的成品材料。请先判断我应该用 SorryCode Image2、Kami 还是 Magazine Web PPT，再问我必要问题。
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
3. 需要演讲展示时，再看 [Magazine Web PPT](/docs/skills/magazine-web-ppt)
4. 需要代码式 PPT 或视频工具链时，再看 [Open Slide](/docs/tools/open-slide) 和 [HyperFrames](/docs/tools/hyperframes)
5. 需要 App 原型、动效或复杂设计交付时，再看 [Huashu Design](/docs/skills/huashu-design)

如果你想研究完整设计工作台，而不是只安装一个 skill，可以看 [工具 / Open Design](/docs/tools/open-design)。
