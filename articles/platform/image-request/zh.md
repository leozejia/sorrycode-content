---
title: 图像请求
slug: image-request
order: 6
summary: 用 /v1/images/generations 或 /v1/images/edits 调用 OpenAI-compatible 图片模型，包括 gpt-image-2 和 Gemini 图片模型。
section: platform
section_title: Platform
section_order: 8
---

# 图像请求

SorryCode 图片能力统一使用 OpenAI-compatible Images API：

```text
POST {{API_BASE_URL}}/images/generations
POST {{API_BASE_URL}}/images/edits
```

OpenAI 图片模型和 Gemini 图片模型都走这套接口，区别只在 `model` 名称。Google Gemini 官方也支持 OpenAI-compatible Images 请求方式，因此不需要为 Gemini 图片维护第二套公开请求协议。

<h2 id="prepare">开始前准备</h2>

你需要：

- 一个 SorryCode API Key，也就是 `sk-...`
- 账户余额和权限可用
- 一个图片想法
- 如果要编辑图片，还需要一张本地图片，比如 `./input/product.png`

如果你还没有 API Key，先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="key-model">API Key 和模型</h2>

你在控制台创建的 API Key，需要开通对应图片模型后才能使用。

小白先记住这句话：

```text
请求里不用额外切换权限。先确认当前 sk-... 能不能用目标图片模型。
```

所以如果你想用某个图片模型，不是给请求额外加一个“切换权限”的参数，而是确认当前使用的 `sk-...` 是否已经开通这个模型。

如果请求失败，先检查三件事：

- API Key 是否填对
- 这个 API Key 是否可用目标图片模型
- `model` 是否写成了当前可用的模型名

<h2 id="models">模型怎么选</h2>

| 模型 | 说明 |
| --- | --- |
| `gpt-image-2` | OpenAI 图片模型，默认推荐 |
| `gemini-3-pro-image-preview` | Gemini 图片模型，推荐作为 Gemini 默认模型 |
| `gemini-3.1-flash-image-preview` | Gemini 图片模型，可返回图片，但同步请求更容易超时 |
| `gemini-2.5-flash-image` | Google 官方 Gemini 图片模型名之一；是否可用以你当前 API Key 为准 |

`Nano Banana` / `Nano Banana Pro` 可以作为用户熟悉的产品名或营销名出现，但请求里优先写真实模型代码。

<h2 id="generate">生成图片</h2>

### macOS / Linux

```bash
export SORRYCODE_API_KEY='你的 sk-...'

curl {{API_BASE_URL}}/images/generations \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "Generate a clean 1:1 product-style image of a cute orange cat astronaut sticker on a pastel background. No text.",
    "size": "1024x1024",
    "n": 1,
    "response_format": "b64_json"
  }'
```

### Windows PowerShell

```powershell
if (-not $env:SORRYCODE_API_KEY) {
  throw "SORRYCODE_API_KEY is not set."
}

$body = @{
  model = "gpt-image-2"
  prompt = "Generate a clean 1:1 product-style image of a cute orange cat astronaut sticker on a pastel background. No text."
  size = "1024x1024"
  n = 1
  response_format = "b64_json"
}

$json = $body | ConvertTo-Json -Depth 10
[System.IO.File]::WriteAllText("request.json", $json, [System.Text.UTF8Encoding]::new($false))
Get-Content -Raw -Encoding utf8 request.json | ConvertFrom-Json | Out-Null

curl.exe "{{API_BASE_URL}}/images/generations" `
  -H "Authorization: Bearer $env:SORRYCODE_API_KEY" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

成功响应里的图片通常在：

```text
data[0].b64_json
```

<h2 id="save-image">保存返回图片</h2>

如果你把响应保存成 `response.json`，可以取出 base64 图片并保存。

macOS：

```bash
jq -r '.data[0].b64_json' response.json | base64 -D > image.png
```

Linux：

```bash
jq -r '.data[0].b64_json' response.json | base64 -d > image.png
```

<h2 id="edits">编辑图片</h2>

编辑图片使用：

```text
POST {{API_BASE_URL}}/images/edits
```

最少需要这些字段：

- `model`：图片模型名，例如 `gpt-image-2` 或已开放的 Gemini 图片模型
- `prompt`：你想怎么修改已有图片
- `image`：本地图片文件
- `size`：例如 `1024x1024`

### macOS / Linux

```bash
export SORRYCODE_API_KEY='你的 sk-...'

curl {{API_BASE_URL}}/images/edits \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -F "model=gpt-image-2" \
  -F "prompt=把这张产品截图改成更适合作为官网 hero 的视觉图：保留核心界面轮廓，背景更干净，光线更柔和" \
  -F "image=@./input/product.png" \
  -F "size=1024x1024"
```

`image=@./input/product.png` 里的路径要换成你电脑上真实存在的图片路径。

<h2 id="parameters">参数怎么填</h2>

推荐参数：

| 参数 | 推荐值 | 说明 |
| --- | --- | --- |
| `model` | `gpt-image-2` 或 `gemini-3-pro-image-preview` | 按你要用的图片模型选择 |
| `prompt` | 你的图片描述 | 生成图片时写想生成什么；编辑图片时写想怎么修改 |
| `size` | `1024x1024` | 第一次使用最稳 |
| `n` | `1` | 先生成一张 |
| `response_format` | `b64_json` | 方便直接保存图片 |

尺寸按模型能力区分。第一次请求建议用 `1024x1024`。

`gpt-image-2` 常用尺寸：

| 用途 | size |
| --- | --- |
| 默认 / 方图 | `1024x1024` |
| 横图 | `1536x1024` |
| 竖图 | `1024x1536` |
| 2K 方图 | `2048x2048` |
| 2K 横图 | `2048x1152` |
| 4K 横图 | `3840x2160` |
| 4K 竖图 | `2160x3840` |
| 让模型决定 | `auto` |

Gemini 图片模型当前只推荐 `1024x1024` 作为稳定首选。不要把 `4096x4096` 当作 4K 图片尺寸；它不符合当前上游尺寸约束。

<h2 id="streaming">流式请求</h2>

部分图片模型支持流式请求：

```json
{
  "stream": true,
  "partial_images": 2
}
```

流式会返回 SSE 事件，适合 `gpt-image-2` 的慢图或大图。但不是所有模型和上游都适合流式；Gemini 图片模型首测建议使用非流式 `response_format: "b64_json"`。

<h2 id="common-issues">常见问题</h2>

### 524

`524` 通常表示请求已经到达 SorryCode，但图片生成期间太久没有完整响应。可以稍后重试、缩短 prompt、降低尺寸，或优先使用已验证更稳定的模型。4K 图片响应体较大，当前不承诺稳定。

### 401

API Key 错误，或没有放在 `Authorization: Bearer ...` 里。

### 400

参数、模型名、源图片或图片格式不符合要求。遇到 `images endpoint requires an image model` 时，检查 `model` 是否是已开放的图片模型。

### 503 No available compatible accounts

当前 API Key 暂时不能使用这个图片模型。先检查模型名是否写对，确认这个 Key 是否已开通图片能力；如果仍然失败，联系 SorryCode 支持处理。

<h2 id="next">下一步</h2>

如果你不想手写 HTTP 请求，使用 [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)。
