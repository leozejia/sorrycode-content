---
title: 藏师傅的 PPT Skill
slug: magazine-web-ppt
order: 4
summary: 一个持续进化的 PPT 制作 skill。适合用 agent 生成有明确设计系统的单文件 HTML 演示，也能承接配图和平台封面。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/op7418/guizang-ppt-skill
---

# 藏师傅的 PPT Skill

`藏师傅的 PPT Skill` 来自歸藏老师开源的 `guizang-ppt-skill`。它不是 SorryCode 唯一的 PPT 方案，而是我们当前收录的一条优秀演示制作路线。

它适合让 agent 生成有明确设计系统的单文件 HTML 横向翻页 PPT。当前上游已经不只是“杂志风”：它包含电子杂志风、瑞士国际主义、配图流程、平台封面和质量检查。具体版式、主题、脚本和最新能力，以官方仓库为准。

参考：[guizang-ppt-skill 官方仓库](https://github.com/op7418/guizang-ppt-skill)

<h2 id="what-is-it">它是什么</h2>

- 一个面向演示表达的设计型 skill
- 产物默认是单文件 HTML，不是 `.pptx`
- 适合由 agent 按主题、受众、时长、素材和风格生成 deck
- 上游持续更新，站内只维护长期稳定的使用边界

你可以把它理解成：让 agent 按一套成熟设计工作流做 PPT，而不是每次从零写一长串“高级感”提示词。

<h2 id="what-is-good-for">适合做什么</h2>

优先用在这些场景：

- 线下分享、私享会、行业内部讲话
- AI 产品发布、研究汇报、demo day
- 需要强烈个人风格的演讲
- 想要网页翻页、视觉完整、可直接展示的 HTML deck
- 需要围绕同一视觉系统生成 PPT 配图或平台封面

如果你只需要改已有 `.pptx`，先看 [PPTX](/docs/skills/pptx)。如果你要做可维护 React deck，先看 [工具 / Open Slide](/docs/tools/open-slide)。

<h2 id="presentation-route">和其他 PPT 能力怎么选</h2>

| 需求 | 优先看 |
| --- | --- |
| 修改已有 PowerPoint、套公司模板、最终交付 `.pptx` | [PPTX](/docs/skills/pptx) |
| 快速生成有明确视觉风格的网页演示 | `藏师傅的 PPT Skill` |
| 把文章、报告、简历或作品集整理成纸面风材料 | [Kami](/docs/skills/kami) |
| 做可维护、可评论、可导出 HTML/PDF 的代码式 deck | [工具 / Open Slide](/docs/tools/open-slide) |

<h2 id="what-is-not-good-for">不适合做什么</h2>

这些场景不要优先用它：

- 必须交付公司 `.pptx` 模板
- 大段表格数据和高密度培训课件
- 需要多人长期协作编辑的传统 PowerPoint 文件
- 只想做普通长文、简历、一页纸或作品集

<h2 id="one-click-install">一键安装</h2>

这是我们验证过的上游安装命令。

### Codex

```bash
npx skills add op7418/guizang-ppt-skill -a codex -g -y
```

### Claude Code

```bash
npx skills add op7418/guizang-ppt-skill -a claude-code -g -y
```

如果你还没装好 runtime，请先回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

如果不想继续使用，先运行 `npx skills list --global` 确认名称，再用 `npx skills remove --global guizang-ppt-skill` 卸载。

<h2 id="how-to-use">安装后怎么触发</h2>

触发时直接说你要做什么演示，不要先讲实现细节。

最好一次说清：

- 主题是什么
- 听众是谁
- 使用场景是什么
- 大概讲多久
- 有没有原始素材和图片
- 想要什么视觉方向，比如杂志风、瑞士风、产品发布感

如果你没说全，它会先问必要问题。先对齐大纲，再开始生成最终文件。

<h2 id="first-prompts">第一句可以说什么</h2>

做私享会：

```text
请用藏师傅的 PPT Skill 帮我做一份 20 页左右的演示，主题是 AI 如何改变组织协作，面向公司管理层，适合 30 分钟私享会。先问我必要问题，再给大纲。
```

把文章改成幻灯片：

```text
请用藏师傅的 PPT Skill 把下面这篇文章改成一套演讲幻灯片。先判断适合电子杂志风还是瑞士风，再给我页面结构。
```

做产品发布：

```text
请用藏师傅的 PPT Skill 做一套产品发布会 deck，包含封面、3 个章节、数据页、Before/After 对比页和结尾页。图片我会放在 images 文件夹里。
```

<h2 id="images">图片怎么放</h2>

最简单的方式是：在 HTML 同级目录放一个 `images/` 文件夹。

建议按页码和英文语义命名：

```text
ppt/
├── index.html
└── images/
    ├── 01-cover.jpg
    ├── 03-figma.png
    └── 05-dashboard.png
```

规则尽量简单：

- 照片用 `JPG`
- 截图用 `PNG`
- 文件名用 `01-cover` 这种补零页码
- 想换图时，直接用同名文件覆盖，不要去改 HTML 路径

<h2 id="common-issues">常见问题</h2>

- 提示 `npx`、`node` 或 `npm` 找不到
  先去看 [环境准备 / Node.js](/docs/environment/nodejs)
- 它会生成 `.pptx` 吗
  默认不会，它生成的是单文件 HTML 幻灯片
- 为什么站内不写完整主题和版式清单
  上游在持续更新，站内只维护选择、安装、触发和边界；具体能力看官方仓库
- 我想做普通文档或简历
  先用 [Skills / Kami](/docs/skills/kami)
- 我用的是 OpenClaw / Hermes Agent
  上游可被其他 agent 参考，但站内当前先只验证 `Codex / Claude Code`

<h2 id="references">参考</h2>

- 官方仓库：<https://github.com/op7418/guizang-ppt-skill>
- 当前公开安装方式：`npx skills add op7418/guizang-ppt-skill`
- 最近核对：2026-05-12，上游 README 已覆盖双视觉系统、配图流程、平台封面和质量检查
