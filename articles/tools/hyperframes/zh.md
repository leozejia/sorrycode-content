---
title: HyperFrames
slug: hyperframes
order: 6
summary: 用 agent 写 HTML 视频 composition，再预览和渲染成 MP4 的工具链。适合产品短视频、发布动效、课程片头和社媒视频。
section: tools
section_title: 工具
section_order: 28
source_url: https://github.com/heygen-com/hyperframes
---

# HyperFrames

`HyperFrames` 是一个给 agent 用的视频工具链。

它不是普通视频生成模型，也不是剪辑软件。它更像“用 HTML/CSS/JavaScript 写一段视频”，再通过 CLI 预览和渲染成 `MP4`。

Codex App 插件只是入口之一。如果你在 CLI 里用 Codex 或 Claude Code，也可以使用 HyperFrames。

如果你只是想先把 Codex App 里的 HyperFrames 插件启用，先看 [Runtime / Codex App 插件配置](/docs/runtime/codex-plugins)。那篇处理插件入口灰色、`/plugins` 找不到插件、`hyperframes@openai-curated` 写法这些配置问题。

本页继续讲 HyperFrames 本身：什么时候适合用它，以及怎么初始化、预览和渲染视频项目。

<h2 id="when-to-use">什么时候用它</h2>

适合这些任务：

- 产品发布短视频
- 课程片头或章节转场
- 社媒动效和宣传短片
- 把网页式视觉做成 MP4
- 用 agent 生成可复用的视频 composition

如果你只需要一张静态图，先用 [SorryCode Image2](/docs/skills/sorrycode-image2)。如果你要做演讲幻灯片，先看 [Magazine Web PPT](/docs/skills/magazine-web-ppt) 或 [Open Slide](/docs/tools/open-slide)。

<h2 id="how-it-works">它怎么工作</h2>

典型流程是：

```text
初始化视频项目 -> 让 agent 写 composition -> 本地预览 -> 渲染 MP4
```

常用命令：

```bash
npx hyperframes init my-video
cd my-video
codex
```

在项目里让 agent 写好视频后，再预览和导出：

```bash
npx hyperframes preview
npx hyperframes render --output final.mp4
```

<h2 id="first-prompt">第一句话</h2>

进入项目后，可以说：

```text
请用 HyperFrames 做一个 20 秒产品发布短视频。先给我脚本、分镜、视觉方向和节奏，不要直接渲染。
```

如果你已有网页或产品介绍：

```text
请用 HyperFrames 把这段产品介绍做成 15 秒社媒视频。先设计 4 个镜头，每个镜头说明文案、画面和动效。
```

<h2 id="before-start">开始前先确认</h2>

第一次使用前，先检查环境：

```bash
node -v
npx hyperframes doctor
```

如果缺 Node.js，先看 [环境准备 / Node.js](/docs/environment/nodejs)。

<h2 id="how-to-choose">和图片、PPT 怎么选</h2>

| 需求 | 优先看 |
| --- | --- |
| 静态封面、海报、插图 | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| 网页风或杂志风演讲 PPT | [Magazine Web PPT](/docs/skills/magazine-web-ppt) |
| 代码式 React deck | [Open Slide](/docs/tools/open-slide) |
| App 原型、动效、信息图和设计评审 | [Huashu Design](/docs/skills/huashu-design) |
| MP4 短视频和网页式动效 | `HyperFrames` |

<h2 id="not-for">不适合什么</h2>

这些场景不要优先用 HyperFrames：

- 长视频剪辑
- 真人素材复杂后期
- 大量音轨、字幕和剪辑时间线
- 想用“一句话视频模型”直接生成真人视频

HyperFrames 更适合可控的网页式短视频和 motion graphics。

<h2 id="references">参考</h2>

- 官方文档：<https://hyperframes.heygen.com/quickstart>
- CLI 文档：<https://hyperframes.heygen.com/packages/cli>
- 官方仓库：<https://github.com/heygen-com/hyperframes>
