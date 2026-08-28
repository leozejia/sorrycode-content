---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: 自动复用当前 SorryCode Codex Key，通过 gpt-image-2-all 或 gpt-image-2 生成和编辑图片，并保存可复现的项目文件。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

Codex 内置图片工具是否可用，取决于当前会话实际提供的工具。使用 SorryCode 自定义
provider 时，稳定做法是安装本 Skill。Images API 和 Codex 内置生图的区别见
[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)。

`SorryCode Image2` 适合需要固定输出和可复现过程的图片任务。Agent 会自动查找当前 SorryCode Codex Key，调用图片接口，并把 prompt、响应、诊断和图片文件保存到项目中。

标准尺寸先尝试 `gpt-image-2-all`，明确失败且可以安全重试时再尝试 `gpt-image-2`。2K 和 4K 尺寸使用 `gpt-image-2`。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="when-to-use">什么时候使用</h2>

这些情况适合安装：

- 编辑已有的本地图片
- 指定尺寸和输出目录
- 保存 `prompt.txt`、`response.json` 或 `events.ndjson`
- 在项目里重复执行同一套图片流程

当前 Codex 会话明确提供内置图片工具时，也可以直接在对话中生图。

<h2 id="one-click-install">安装</h2>

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

如果还没装好工作台，先看：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

卸载前先运行 `npx skills list --global` 确认名称，再执行 `npx skills remove --global sorrycode-image2`。

<h2 id="api-key">复用 Codex Key</h2>

先按 [模型与工作台 / Codex](/docs/runtime/codex) 完成 SorryCode Codex 接入。Skill 会从当前 Codex 配置中确认活动的 SorryCode provider，并自动读取它正在使用的 Key。你不需要创建图片专用 Key，也不需要设置环境变量。

在 Claude Code 中使用这个 Skill 时，同一台机器也要先完成 SorryCode Codex 接入。Agent 仍会读取这份 Codex 配置，不会建立第二套凭据。

如果 Agent 找不到 Key，请回到 `https://sorrycode.com/keys`，选择准备给 Codex 使用的 Key，点击「接入工具」，再执行一次 Codex 接入命令。不要把真实 Key 发进 Agent 对话、写入项目文件或放进截图。

图片请求固定发送到 `https://api.sorrycode.com/v1`。

<h2 id="first-prompt">第一句可以说什么</h2>

生成图片：

```text
请用 SorryCode Image2 生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。保存到 outputs/images/first-cover/。
```

编辑图片：

```text
请用 SorryCode Image2 编辑 ./input/product.png，保留核心界面轮廓，让背景更干净、光线更柔和。保存到 outputs/images/product-hero/。
```

指定尺寸：

```text
请用 SorryCode Image2 生成一张官网 hero 横图，尺寸使用 1536x1024，保存到 outputs/images/website-hero/。
```

常用尺寸包括 `1024x1024`、`1536x1024` 和 `1024x1536`。第一次运行建议用 `1024x1024`。

<h2 id="what-it-saves">它会保存什么</h2>

默认建议保存到：

```text
outputs/images/你的任务名/
```

目录中通常会有：

- `prompt.txt`
- `request.json`
- `response.json` 或 `events.ndjson`
- 生成或编辑后的图片文件

<h2 id="common-issues">常见问题</h2>

- 找不到 Key：在 API Key 页面重新执行「接入工具 / Codex」，然后再次运行 Skill
- `401`：当前 Codex Key 已失效，请重新接入 Codex
- `403`：当前 Codex Key 所属分组没有开放图片能力
- `400`：检查输入图片、prompt、尺寸和模型
- 请求中断或超时：不要立即重复发送付费请求，先查看诊断文件并确认上一条请求的状态
- `503 No available compatible accounts`：当前 Codex 分组暂时没有可用的图片账号，请稍后重试

<h2 id="more-aigc">更多 AIGC 需求</h2>

SorryCode Image2 负责 `gpt-image-2-all` 和 `gpt-image-2` 的生成与编辑。需要更多 AIGC 模型、素材生产或专门的视觉资产工作流时，请使用 [SorryAssets](https://sorryassets.com)。

<h2 id="next">下一步</h2>

- 返回 OpenAI 图片能力总览：[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)
- 查看源码：[linxiverse/sorrycode-image2](https://github.com/linxiverse/sorrycode-image2)
