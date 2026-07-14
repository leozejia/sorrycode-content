---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: 使用 gpt-image-2 生成或编辑图片，并保存 prompt、响应、诊断和图片文件。适合需要固定输出和可复现工作流的进阶任务。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

如果只是想快速生成一张图片，先在 `Codex App` 里直接说出需求，不需要安装 Skill。
自然语言生图、Images API 和本 Skill 的完整分流见
[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)。

`SorryCode Image2` 适合需要固定输出和可复现过程的图片任务。它会检查 API Key，调用图片接口，并把 prompt、响应、诊断和图片文件保存到项目中。

当前只支持 `gpt-image-2`。

<h2 id="when-to-use">什么时候使用</h2>

这些情况适合安装：

- 编辑已有的本地图片
- 指定尺寸和输出目录
- 保存 `prompt.txt`、`response.json` 或 `events.ndjson`
- 在项目里重复执行同一套图片流程

如果只是第一次生图或快速改一版，直接在 Codex App 中对话更简单。

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

<h2 id="api-key">设置图片 API Key</h2>

Skill 读取 `SORRYCODE_API_KEY`。如果还没有 API Key，先去 [Platform / 创建 API Key](/docs/platform/create-api-key)。

你可以把下面这句话交给 Codex 或 Claude Code：

```text
请帮我把 SorryCode 图片 API Key 设置成长期可用。我的 key 是：sk-...。如果当前系统是 Windows，请用用户级 PowerShell 设置；如果是 macOS，请写入 zsh 配置。设置前先告诉我会改哪里。
```

Windows PowerShell：

```powershell
[Environment]::SetEnvironmentVariable("SORRYCODE_API_KEY", "你的 sk-...", "User")
```

macOS / Linux：

```bash
echo "export SORRYCODE_API_KEY='你的 sk-...'" >> ~/.zshrc
source ~/.zshrc
```

这个变量只供 SorryCode Image2 使用，不会修改 Codex 的模型配置。

<h2 id="first-prompt">第一句可以说什么</h2>

生成图片：

```text
请用 SorryCode Image2 生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。使用 gpt-image-2，保存到 outputs/images/first-cover/。
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

- 缺少 `SORRYCODE_API_KEY`：先创建 API Key，再重新打开工作台或终端
- `401`：API Key 不正确或没有正确设置
- `400`：检查输入图片、prompt、尺寸和模型；当前模型必须是 `gpt-image-2`
- `524`：降低图片尺寸、缩短 prompt，或稍后重试
- `503 No available compatible accounts`：当前 API Key 暂时无法使用图片模型，请检查权限或稍后重试

<h2 id="more-aigc">更多 AIGC 需求</h2>

SorryCode Image2 只负责 `gpt-image-2` 的生成和编辑。需要更多 AIGC 模型、素材生产或专门的视觉资产工作流时，请使用 [SorryAssets](https://sorryassets.com)。

<h2 id="next">下一步</h2>

- 返回 OpenAI 图片能力总览：[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)
- 查看源码：[linxiverse/sorrycode-image2](https://github.com/linxiverse/sorrycode-image2)
