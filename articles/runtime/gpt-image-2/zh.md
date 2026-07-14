---
title: GPT Image 2
slug: gpt-image-2
order: 2
summary: 在 Codex 中直接用自然语言生图，或通过 SorryCode Images API 和 SorryCode Image2 Skill 使用 gpt-image-2。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2

`gpt-image-2` 是 SorryCode 当前主推的 OpenAI 图片模型。你可以按任务复杂度选择三种入口：

| 需求 | 推荐入口 |
| --- | --- |
| 快速生成、继续用自然语言修改 | Codex App 对话 |
| 自己开发程序或接入工作流 | Images API |
| 编辑本地图片、固定输出目录、保存诊断 | SorryCode Image2 Skill |

第一次使用时，优先在 Codex App 里直接说需求。

<h2 id="codex">在 Codex 中直接生成</h2>

完成 [Codex 接入](/docs/runtime/codex) 后，直接说：

```text
帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。
```

生成后可以继续提出具体修改：

```text
把标题区域留得更宽一些，减少装饰元素，改成横版。
```

这条路径不需要你手写模型参数。Codex 会在当前对话中完成图片调用和迭代。

<h2 id="api">通过 Images API 生成</h2>

开发者入口是：

```text
POST https://sorrycode.com/v1/images/generations
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

发送请求：

```bash
curl -N https://sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe -N https://sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer $env:SORRYCODE_API_KEY" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

图片生成可能比文本慢。默认保留 `stream: true` 和 `partial_images: 2`，客户端会先收到
中间事件，再收到完成事件。需要自动保存图片和诊断文件时，直接使用下面的 Skill。

<h2 id="skill">使用 SorryCode Image2 Skill</h2>

[SorryCode Image2](/docs/skills/sorrycode-image2) 只使用 `gpt-image-2`，适合：

- 编辑本地 PNG、JPEG 或 WebP；
- 固定输出目录和尺寸；
- 保存 prompt、请求、响应和流式事件；
- 在项目里重复执行同一套图片任务。

你可以把这句话交给 Codex 或 Claude Code：

```text
请安装 SorryCode Image2，然后用 gpt-image-2 生成一张 1024x1024 的图片，保存到 outputs/images/first-run/。运行前先检查 SORRYCODE_API_KEY。
```

<h2 id="errors">常见问题</h2>

- `401`：API Key 缺失、错误或没有作为 Bearer Token 发送。
- `403`：当前 API Key 所属分组没有开放图片能力。
- `400`：检查模型、prompt、尺寸和图片输入格式。
- `503 No available compatible accounts`：当前分组暂时没有可用的兼容图片账号。
- 请求长时间没有结果：保留流式参数，缩短 prompt 或先用 `1024x1024` 重试。

<h2 id="next">下一步</h2>

- 还没接入 Codex：[模型与工作台 / Codex](/docs/runtime/codex)
- 需要可复现工作流：[Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- 还没有 API Key：[Platform / 创建 API Key](/docs/platform/create-api-key)
