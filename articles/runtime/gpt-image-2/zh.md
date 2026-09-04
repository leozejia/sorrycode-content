---
title: GPT Image 2
slug: gpt-image-2
order: 2
summary: 通过 SorryCode Images API 使用 gpt-image-2，支持生成、编辑和流式返回；Codex 内置生图以当前会话实际提供的工具为准。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2

SorryCode 通过 OpenAI 兼容的 Images API 提供 `gpt-image-2`。你可以在 Codex 的自然语言任务中让 Agent 读取本页并执行请求，也可以自己写程序调用接口。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它读取本页，使用当前环境已配置的 SorryCode API Key，按本页接口生成或编辑图片，保存结果并检查文件是否完整。不要在对话中粘贴 API Key，也不要把 Key 写进项目文件。如果当前环境没有可用 Key，让 Agent 告诉你去 API Key 页面选择支持图片能力的分组并完成接入。

<h2 id="codex">Codex 内置生图</h2>

如果当前 Codex 会话已经提供图片生成工具，可以直接说：

```text
帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，给标题留出清晰区域。
```

这条路径由 Codex 的 Responses 图片工具完成，不需要手写接口参数。自定义 provider 不一定提供这个工具。工具不可用时，按下面的 Images API 路径执行；继续修改提示词不会补上缺少的工具。

<h2 id="prepare">开始前准备</h2>

1. 在 `https://sorrycode.com/keys` 创建或选择一把 API Key。
2. 确认它所属分组开放图片生成，并且可以路由到 `gpt-image-2`。
3. 手动调用时，把这把 Key 放进 `Authorization: Bearer ...` 请求头。GPT Image 2 API 不需要单独的图片 Key，也不要求设置通用环境变量。

如果你使用 Codex 的一键接入，安装器会保存当前选择的 Key。不同分组的 Key 不能仅凭 `sk-` 前缀互换。

<h2 id="generate">通过 Images API 生成</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/generations
```

先创建 `request.json`。macOS / Linux：

```bash
cat > request.json <<'JSON'
{
  "model": "gpt-image-2",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "n": 1,
  "stream": true,
  "partial_images": 2,
  "response_format": "b64_json"
}
JSON
```

Windows PowerShell：

```powershell
$json = @'
{
  "model": "gpt-image-2",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "n": 1,
  "stream": true,
  "partial_images": 2,
  "response_format": "b64_json"
}
'@

[System.IO.File]::WriteAllText(
  "request.json",
  $json,
  [System.Text.UTF8Encoding]::new($false)
)
```

发送请求，把示例中的占位值换成你的 API Key：

```bash
curl -N https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe -N https://api.sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

图片生成可能比文本慢。保留 `stream: true` 和 `partial_images: 2`，客户端会先收到中间事件，再收到完成事件。只把完成事件里的最终图片保存下来。

<h2 id="edit">编辑已有图片</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/edits
```

请求使用 `multipart/form-data`，输入支持 PNG、JPEG 和 WebP：

```bash
curl https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -F "model=gpt-image-2" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024"
```

<h2 id="save">保存返回的图片</h2>

- `response_format: b64_json` 返回 Base64 数据。解码 `data[0].b64_json` 后写入 `.png` 或接口返回的实际格式。
- `response_format: url` 返回 `data[0].url`。临时 URL 可能过期，拿到后立即下载并保存。
- 流式请求中的中间图片只用于预览。等收到完成事件后再保存最终结果。

Agent 可以直接完成解码、下载和落盘，但应在报告成功前确认目标文件存在且能正常读取。请求中断或超时后，先检查上一条请求状态，不要立即重复提交付费请求。

<h2 id="agent">让 Agent 直接执行</h2>

把本页 Markdown 或链接交给 Agent，然后说明任务和保存位置：

```text
请读取 GPT Image 2 接入文档，使用当前环境已配置的 SorryCode API Key，调用 Images API 生成一张 1024x1024 的图片，保存到 outputs/images/first-run/，确认文件可以读取后再告诉我结果。不要让我粘贴 API Key，也不要把 Key 写入文件。
```

如果 Agent 没有可用的 HTTP 或文件工具，它只能给出请求示例，不能代替实际生成。此时按本页的 Curl 示例执行。

<h2 id="errors">常见问题</h2>

- `401`：API Key 缺失、错误或没有作为 Bearer Token 发送。
- `403`：当前 Key 所属分组没有开放图片能力。
- `400`：检查模型、prompt、尺寸和图片输入格式。
- `503 No available compatible accounts`：当前分组暂时没有可用的兼容图片账号。
- 长时间没有结果：保留流式参数，先用 `1024x1024` 验证链路；超时后先确认上一条请求状态。

<h2 id="next">下一步</h2>

- 还没接入 Codex：[模型与工作台 / Codex](/docs/runtime/codex)
- 需要 Grok 图片：[模型与工作台 / Grok 图片生成](/docs/runtime/grok-image)
- 需要 Grok 视频：[模型与工作台 / Grok 视频生成](/docs/runtime/grok-video)
- 还没有 API Key：[开始使用 / 创建 API Key](/docs/start/create-api-key)
