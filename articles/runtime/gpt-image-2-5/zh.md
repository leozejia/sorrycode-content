---
title: GPT Image 2.5
slug: gpt-image-2-5
order: 3
summary: 通过 SorryCode Images API 使用 gpt-image-2.5-flare 和 gpt-image-2.5-sunburst；具体可用模型以 API Key 所属分组目录为准。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2.5

GPT Image 2.5 在 API 中使用具体的模型 ID：`gpt-image-2.5-flare` 和 `gpt-image-2.5-sunburst`。`gpt-image-2.5` 只是系列名称，不能直接当作请求里的 `model` 值。

SorryCode 通过 OpenAI 兼容的 Images API 提供这两个模型。你的 API Key 所属分组需要已经开放图片能力，并且在模型目录中列出要使用的模型。

| 模型 | 适合场景 |
| --- | --- |
| `gpt-image-2.5-flare` | 速度优先的日常生成、社交内容和高频草稿 |
| `gpt-image-2.5-sunburst` | 更在意编辑精度、主体保持和成品质量的工作 |

两者都处理文字和图片输入，输出图片，不处理音频或视频。官方模型页标注这两个模型不支持流式输出。质量档位可使用 `low`、`medium`、`high`、`xhigh`、`max` 或 `auto`，但当前分组未必开放所有选项。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它读取本页，使用当前环境已配置的 SorryCode API Key，按本页选择一个可用模型生成或编辑图片，保存结果并检查文件是否完整。不要在对话中粘贴 API Key，也不要把 Key 写进项目文件。

<h2 id="prepare">开始前准备</h2>

1. 在 `https://sorrycode.com/keys` 创建或选择一把 API Key。
2. 确认它所属分组开放图片生成，并且模型目录中有 `gpt-image-2.5-flare` 或 `gpt-image-2.5-sunburst`。
3. 手动调用时，把这把 Key 放进 `Authorization: Bearer ...` 请求头。GPT Image 2.5 不需要单独的图片 Key，也不要求设置通用环境变量。

如果模型目录里没有这两个 ID，先不要把 `gpt-image-2.5` 当作替代值。请切换到已开放对应模型的分组，或联系管理员确认模型配置。

<h2 id="generate">通过 Images API 生成</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/generations
```

先创建 `request.json`。下面用 Flare 举例，换成 Sunburst 时只需替换 `model`：

```json
{
  "model": "gpt-image-2.5-flare",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "n": 1,
  "quality": "auto"
}
```

发送请求，把示例中的占位值换成你的 API Key：

```bash
curl https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe https://api.sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

这页先使用非流式请求，便于确认模型和分组配置。GPT Image 2.5 不使用 GPT Image 2 的 `stream` 或 `partial_images` 示例；其他高级参数也应以当前模型目录和实际接口返回为准。

<h2 id="edit">编辑已有图片</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/edits
```

请求使用 `multipart/form-data`：

```bash
curl https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -F "model=gpt-image-2.5-sunburst" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024"
```

<h2 id="save">保存返回的图片</h2>

- 如果响应返回 `data[0].b64_json`，解码 Base64 后写入图片文件。
- 如果响应返回 `data[0].url`，请尽快下载并保存，临时 URL 可能过期。
- Agent 报告成功前，应确认目标文件存在且可以正常读取。
- 请求中断或超时后，先检查上一条请求状态，不要立即重复提交付费请求。

<h2 id="codex">Codex 内置生图</h2>

Codex 是否能直接使用图片工具，取决于当前会话实际提供的工具和模型目录。工具不可用时，使用上面的 Images API；继续修改提示词不会补上缺少的工具。

<h2 id="errors">常见问题</h2>

- `400`：把系列名称 `gpt-image-2.5` 当成了模型 ID，或请求参数不适合当前模型。
- `401`：API Key 缺失、错误或没有作为 Bearer Token 发送。
- `403`：当前 Key 所属分组没有开放图片能力。
- `503 No available compatible accounts`：当前分组暂时没有可用的兼容图片账号。
- `502` 或 `524`：上游失败、连接取消或同步请求超过入口等待窗口。

<h2 id="next">下一步</h2>

- 需要 GPT Image 2：[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)
- 还没接入 Codex：[模型与工作台 / Codex](/docs/runtime/codex)
- 需要 Grok 图片：[模型与工作台 / Grok 图片生成](/docs/runtime/grok-image)
- 还没有 API Key：[开始使用 / 创建 API Key](/docs/start/create-api-key)
