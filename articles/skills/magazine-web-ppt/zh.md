---
title: Magazine Web PPT
slug: magazine-web-ppt
order: 4
summary: 一个生成电子杂志风网页 PPT 的 skill。适合做分享会、发布会、私享会和 demo day 的单文件 HTML 幻灯片。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/op7418/guizang-ppt-skill
---

# Magazine Web PPT

如果你明确要做的是一套演讲幻灯片，而不是普通文档，`Magazine Web PPT` 是 `Kami` 之后第二个值得看的 skill。

它会生成一份单文件 HTML 横向翻页 PPT，视觉基调是“电子杂志 × 电子墨水”，适合私享会、发布会、行业分享和 demo day。

<h2 id="what-is-it">它是什么</h2>

- `Magazine Web PPT` 是一个面向演讲幻灯片的设计型 skill
- 它的产物是单文件 HTML，不是 `.pptx`
- 它支持键盘、滚轮、触屏、底部圆点和 `ESC` 缩略图索引
- 它内置 10 种页面布局和 5 套主题色

它来自归藏开源的 `guizang-ppt-skill`。SorryCode 站内文档会用一个更容易理解的名字来讲它：`Magazine Web PPT`。

参考：[guizang-ppt-skill 官方仓库](https://github.com/op7418/guizang-ppt-skill)

<h2 id="what-is-good-for">适合做什么</h2>

你可以优先把它用在这些场景：

- 线下分享或行业内部讲话
- 私享会、发布会、demo day
- AI 产品发布或研究汇报
- 需要强烈个人风格的演讲
- 想要像电子杂志一样翻页的网页 PPT

它内置的 10 种布局覆盖常见演讲结构：封面、章节幕封、数据大字报、左文右图、图片网格、Pipeline、悬念问题、大引用、Before/After 对比和图文混排。

<h2 id="what-is-not-good-for">不适合做什么</h2>

这些场景不建议优先用它：

- 大段表格数据
- 信息密度很高的培训课件
- 需要多人协作编辑的传统 PowerPoint 文件
- 只想做普通长文、简历、一页纸或作品集

如果你要做的是普通文档、简历、一页纸或作品集，先用 [Skills / Kami](/docs/skills/kami)。

如果你想把 PPT 当成一个可维护的 React 项目，支持评论修改、浏览器演讲和 HTML/PDF 导出，可以看 [工具 / Open Slide](/docs/tools/open-slide)。

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

安装完成后，不需要记特殊命令。你用自然语言说“做一份杂志风 PPT”就可以触发。

<h2 id="how-to-use">安装后怎么触发</h2>

触发时直接描述你想做的演讲，而不是先讲技术细节。

最好一次说清楚：

- 主题是什么
- 听众是谁
- 使用场景是什么
- 大概讲多久
- 有没有原始素材
- 想选哪套主题色

如果你没说全，它会先反问你 6 件事：受众、时长、素材、图片、主题色和硬约束。先对齐大纲，再开始生成 HTML。

<h2 id="first-prompts">第一句可以说什么</h2>

如果你要做私享会：

```text
帮我做一份 20 页左右的杂志风 PPT，主题是 AI 如何改变组织协作，面向公司管理层，适合 30 分钟私享会。先问我受众、素材、图片和主题色，再给大纲。
```

如果你要把文章改成幻灯片：

```text
把下面这篇文章改成一套电子杂志风格的演讲幻灯片，主题用靛蓝瓷，输出单文件 HTML。
```

如果你要做产品发布：

```text
我要做一套产品发布会 PPT，包含封面、3 个章节、数据页、Before/After 对比页和结尾页。图片我会放在 images 文件夹里。
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

<h2 id="themes">主题怎么选</h2>

它内置 5 套主题色：

- 墨水经典：通用默认、商业发布、不知道选什么时用它
- 靛蓝瓷：科技、研究、AI、技术发布会
- 森林墨：自然、可持续、文化、非虚构
- 牛皮纸：怀旧、人文、文学、独立杂志
- 沙丘：艺术、设计、创意、画廊感内容

第一次不知道选什么，就选“墨水经典”。

<h2 id="common-issues">常见问题</h2>

- 提示 `npx`、`node` 或 `npm` 找不到
  先去看 [环境准备 / Node.js](/docs/environment/nodejs)
- 它会生成 `.pptx` 吗
  默认不会，它生成的是单文件 HTML 幻灯片
- 可以自己指定任意颜色吗
  不建议，优先从 5 套主题里选，避免画面失控
- 我想做普通文档或简历
  先用 [Skills / Kami](/docs/skills/kami)
- 我用的是 OpenClaw / Hermes Agent
  上游可被其他 agent 参考，但站内当前先只验证 `Codex / Claude Code`

<h2 id="references">参考</h2>

- 官方仓库：<https://github.com/op7418/guizang-ppt-skill>
- 当前公开安装方式：`npx skills add op7418/guizang-ppt-skill`
- 官方说明里明确覆盖：
  - 单文件 HTML 横向翻页 PPT
  - 10 种页面布局
  - 5 套主题色
  - 键盘、滚轮、触屏、缩略图索引交互
