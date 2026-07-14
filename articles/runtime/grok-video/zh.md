---
title: Grok 视频生成
slug: grok-video
order: 3
summary: 通过 SorryCode 提交 Grok 文生视频或图生视频任务，并使用 request_id 轮询到完成、失败或过期。
section: runtime
section_title: 模型与工作台
section_order: 10
group: xai
group_title: xAI
group_order: 30
---

# Grok 视频生成

Grok 视频是异步 API。第一次请求只负责创建任务并返回 `request_id`；你还需要调用状态接口，直到任务变成 `done`、`failed` 或 `expired`。

本页只讲已经通过 SorryCode 生产验证的三件事：

- 文生视频；
- 图生视频；
- 根据 `request_id` 轮询结果。

> Grok CLI 的内置 `image_to_video` 当前不会继承 SorryCode 自定义模型的 `base_url`。
> 使用 SorryCode Key 时，请走本页 REST API。

<h2 id="prepare">开始前准备</h2>

在 `https://sorrycode.com/keys` 创建或选择一把 Grok 分组 Key。提交任务和轮询结果必须使用同一把 Grok Key。不要使用给 `SorryCode Image2` 准备的 Image2 Key，也不需要设置环境变量。

<h2 id="models">选择模型</h2>

| 任务 | 模型 |
| --- | --- |
| 文字生成视频 | `grok-imagine-video` |
| 把一张图片动画化 | `grok-imagine-video-1.5` |

视频按输出时长和分辨率计费。第一次测试建议使用较短时长和 `480p`，正式任务再提高规格。

<h2 id="text-to-video">文生视频</h2>

提交接口：

```text
POST https://sorrycode.com/v1/videos/generations
```

macOS / Linux 先创建 `request.json`：

```bash
cat > request.json <<'JSON'
{
  "model": "grok-imagine-video",
  "prompt": "A red paper boat gently floating on still water",
  "duration": 5,
  "resolution": "480p"
}
JSON
```

Windows PowerShell：

```powershell
$json = @'
{
  "model": "grok-imagine-video",
  "prompt": "A red paper boat gently floating on still water",
  "duration": 5,
  "resolution": "480p"
}
'@

[System.IO.File]::WriteAllText(
  "request.json",
  $json,
  [System.Text.UTF8Encoding]::new($false)
)
```

发送请求并保存任务响应：

把 `sk-replace-with-grok-group-key` 替换成你的 Grok 分组 Key。

```bash
curl -sS https://sorrycode.com/v1/videos/generations \
  -H "Authorization: Bearer sk-replace-with-grok-group-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o video-request.json
```

Windows PowerShell：

```powershell
curl.exe -sS https://sorrycode.com/v1/videos/generations `
  -H "Authorization: Bearer sk-replace-with-grok-group-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json" `
  -o video-request.json
```

成功提交后，响应里会有：

```json
{
  "request_id": "..."
}
```

这还不是最终视频。继续执行“轮询结果”。

<h2 id="image-to-video">图生视频</h2>

图生视频使用同一个提交接口。把模型换成 `grok-imagine-video-1.5`，并提供一张可公开访问的图片 URL 或 data URI：

```json
{
  "model": "grok-imagine-video-1.5",
  "prompt": "The paper kite rises gently and moves in a light breeze",
  "duration": 5,
  "resolution": "480p",
  "image": {
    "image_url": "https://example.com/input.png"
  }
}
```

仍然先把这段内容保存为 UTF-8 无 BOM 的 `request.json`，再用上一节的 `curl` 命令提交。
如果图片 URL 需要登录、只在内网可见或很快过期，上游将无法读取它。

<h2 id="poll">轮询结果</h2>

状态接口：

```text
GET https://sorrycode.com/v1/videos/{request_id}
```

macOS / Linux：

```bash
REQUEST_ID=$(jq -r '.request_id' video-request.json)
STATUS="pending"
TERMINAL=0

for attempt in $(seq 1 60); do
  RESULT=$(curl -sS \
    -H "Authorization: Bearer sk-replace-with-grok-group-key" \
    "https://sorrycode.com/v1/videos/$REQUEST_ID")

  STATUS=$(printf '%s' "$RESULT" | jq -r '.status')
  printf 'status=%s\n' "$STATUS"

  case "$STATUS" in
    done)
      printf '%s' "$RESULT" | jq -r '.video.url'
      TERMINAL=1
      break
      ;;
    failed|expired)
      printf '%s' "$RESULT" | jq .
      TERMINAL=1
      break
      ;;
  esac

  sleep 5
done

if [ "$TERMINAL" -eq 0 ]; then
  printf '轮询 60 次后仍未完成，请稍后继续查询同一个 request_id。\n' >&2
fi
```

Windows PowerShell：

```powershell
$requestId = (Get-Content "video-request.json" -Raw | ConvertFrom-Json).request_id
$result = $null

for ($attempt = 1; $attempt -le 60; $attempt++) {
  $result = curl.exe -sS `
    -H "Authorization: Bearer sk-replace-with-grok-group-key" `
    "https://sorrycode.com/v1/videos/$requestId" | ConvertFrom-Json
  $result.status

  if ($result.status -in @("done", "failed", "expired")) {
    break
  }

  if ($result.status -ne "pending") {
    throw "Unexpected video status: $($result.status)"
  }

  Start-Sleep -Seconds 5
}

if ($null -eq $result -or $result.status -notin @("done", "failed", "expired")) {
  throw "Polling did not finish after 60 attempts. Continue later with the same request_id."
}

if ($result.status -eq "done") {
  $result.video.url
} else {
  $result | ConvertTo-Json -Depth 10
}
```

状态为 `pending` 时继续等待；`done` 时读取 `video.url`；`failed` 或 `expired` 时停止轮询并检查响应信息。不要无限轮询，也不要把首次提交响应当作视频文件。

<h2 id="errors">常见问题</h2>

- `401`：API Key 缺失、错误或没有作为 Bearer Token 发送。
- `403`：当前 Key 的 Grok 分组没有开放媒体能力。
- `400`：检查模型、prompt、时长、分辨率和图片字段。
- `202 pending`：正常，表示任务还在生成，不是失败。
- `failed`：任务已终止，检查响应中的错误信息后重新提交。
- `expired`：任务结果已过期，需要重新提交。
- 图生视频失败：确认图片 URL 公网可读，或改用有效的 data URI。

<h2 id="next">下一步</h2>

- 先生成一张输入图片：[模型与工作台 / Grok 图片生成](/docs/runtime/grok-image)
- 使用 Grok 文字和搜索：[模型与工作台 / Grok](/docs/runtime/grok-cli)
- 创建 API Key：[开始使用 / 创建 API Key](/docs/start/create-api-key)

上游能力参考：[xAI Image-to-Video](https://docs.x.ai/developers/model-capabilities/video/image-to-video)
