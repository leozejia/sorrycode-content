---
title: SorryCode Image2
slug: sorrycode-image2
order: 5
summary: 通过一个可复用的 Agent Skill，使用 SorryCode 生成或编辑 GPT Image 2 和 GPT Image 2.5 图片，并把结果保存到项目目录。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

`SorryCode Image2` 是一个给 Codex 和 Claude Code 使用的图片 Skill。它把图片请求、Key 配置、结果保存和完成检查串成一条可复用的路径。

它适合这些任务：

- 生成封面、海报、插图和产品视觉
- 编辑已有的 PNG、JPEG 或 WebP 图片
- 指定模型、尺寸、质量和输出目录
- 让 Agent 保存图片后检查文件是否真的可读取

如果你只想手动调用 Images API，直接看 [GPT Image 2](/docs/runtime/gpt-image-2) 或 [GPT Image 2.5](/docs/runtime/gpt-image-2-5)。如果你希望 Agent 负责执行和保存结果，再安装这个 Skill。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据本页完成 Skill 安装、Key 配置和一次最小图片验证，并列出需要你手动确认的步骤。不要在对话中粘贴 API Key。

<h2 id="install">安装</h2>

先安装 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code)，再运行：

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -a claude-code -g -y
```

也可以使用原生插件路径：

```text
codex plugin marketplace add linxiverse/sorrycode-image2
codex plugin add sorrycode-image2@sorrycode-image2
```

安装完成后，让 Agent 重新读取当前可用的 Skills。不要把仓库 README 整段复制进项目规则文件。

<h2 id="key">配置 Image2 的 Key</h2>

在 [API Key 页面](https://sorrycode.com/keys) 创建或选择一把可以访问目标图片模型的 Key。GPT Image 2 和 GPT Image 2.5 使用 OpenAI / Codex 分组，不要拿 Grok 分组 Key 直接替换。

然后让 Agent 找到已安装的 `sorrycode-image2` Skill，并运行它自带的配置脚本：

```bash
node /path/to/sorrycode-image2/scripts/configure-key.mjs
```

脚本会隐藏输入，把 Key 写入 Skill 的安装目录旁 `.env`，变量名是：

```text
SORRYCODE_IMAGE2_API_KEY
```

这个 `.env` 只属于该 Skill，文件权限是用户可读写，且不会写入 Git、项目文件或诊断输出。重新安装并替换整个 Skill 目录后，需要再次运行配置脚本。也可以在进程环境中临时提供同名变量，进程环境优先于 Skill 本地 `.env`。

不要把 Key 放进 Prompt、截图、项目文件或 shell 历史。直接调用 API 时，不需要设置这个 Skill 专用变量，按模型页面在请求头中发送 Bearer Token 即可。

<h2 id="use">安装后怎么用</h2>

直接点名 Skill，并说明图片内容和保存位置：

```text
请使用 SorryCode Image2 生成一张中文播客封面，主题是 AI 编程入门，暖色调，给标题留出清晰区域，保存到 outputs/images/podcast-cover/。
```

编辑已有图片：

```text
请使用 SorryCode Image2 编辑 ./input.png，把背景改成浅蓝色，保留主体和原来的文字，保存到 outputs/images/edited-cover/。
```

如果需要指定模型、尺寸或质量，也直接写清楚：

```text
请使用 SorryCode Image2，显式调用 gpt-image-2，生成 1024x1024 的蓝色圆形白底图片，保存到 outputs/images/blue-circle/。
```

Skill 的默认路径是：

| 任务 | 默认模型或行为 |
| --- | --- |
| 新图片生成 | `gpt-image-2.5-flare`，`quality: auto` |
| 图片编辑 | `gpt-image-2.5-sunburst`，`quality: auto` |
| 显式使用 `gpt-image-2` | 默认开启流式返回，保存最终图片 |

这些是默认值和示例，不是本地模型白名单。你明确提供的 `--model` 会原样交给 API，模型是否存在、Key 是否有权限以及参数是否支持，由 SorryCode API 决定。

<h2 id="result">结果和保存位置</h2>

没有指定路径时，结果保存到：

```text
outputs/images/<short-slug>/
```

Skill 会保存请求摘要、必要的诊断信息和最终图片。流式请求中的中间图片只用于预览，完成后才保存最终结果。Agent 报告成功前，应确认目标文件存在、格式正确并且可以打开。

如果请求中断、超时或下载结果失败，不要立刻重复提交。上一条付费请求可能仍在处理，先确认它的状态。

<h2 id="boundaries">边界</h2>

- 这个 Skill 只负责通过 SorryCode Images API 生成和编辑图片，不负责 Grok 图片或视频。
- 编辑输入支持 PNG、JPEG 和 WebP。
- 一次只发送一笔付费请求，不会自动切换 Key、模型或其他应用。
- 需要视频时，请看 [Grok 视频生成](/docs/runtime/grok-video)。
- 需要手动请求格式和完整 Images API 说明时，请看 [GPT Image 2](/docs/runtime/gpt-image-2) 和 [GPT Image 2.5](/docs/runtime/gpt-image-2-5)。

<h2 id="troubleshoot">常见问题</h2>

- 找不到 Key：运行 Skill 自带的 `configure-key.mjs`，不要把 Key 粘贴到对话里。
- `401`：检查 Key 是否正确，并确认请求使用 Bearer Token。
- `403`：当前 Key 所属分组没有目标图片能力，回到 API Key 页面换成匹配的分组。
- `400`：检查模型 ID、提示词、尺寸、质量和输入图片格式。
- 超时或连接中断：不要自动重试，先检查上一条请求的状态。

<h2 id="references">参考</h2>

- [GPT Image 2](/docs/runtime/gpt-image-2)：`gpt-image-2` 的 Images API、流式返回和编辑请求
- [GPT Image 2.5](/docs/runtime/gpt-image-2-5)：Flare 和 Sunburst 的模型选择与参数
- [SorryCode Image2 官方仓库](https://github.com/linxiverse/sorrycode-image2)：Skill 安装包和最新脚本
