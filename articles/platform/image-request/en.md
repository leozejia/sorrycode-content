---
title: Image Requests
slug: image-request
order: 4
summary: Use /v1/images/generations or /v1/images/edits for OpenAI-compatible image models, including gpt-image-2 and Gemini image models.
section: platform
section_title: Platform
section_order: 8
---

# Image Requests

SorryCode image generation uses the OpenAI-compatible Images API:

```text
POST {{API_BASE_URL}}/images/generations
POST {{API_BASE_URL}}/images/edits
```

OpenAI image models and Gemini image models use the same API. The difference is the `model` name. Google Gemini officially supports OpenAI-compatible image requests, so SorryCode does not maintain a second public request protocol for Gemini images.

<h2 id="prepare">Before You Start</h2>

You need:

- a SorryCode API key, starting with `sk-...`
- enough balance and permission
- an image idea
- for image edits, a local image file such as `./input/product.png`

If you do not have an API key yet, read [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="key-model">API Key and Models</h2>

The API key you create in the console must have access to the target image model.

Remember this:

```text
You do not switch permissions inside the request. Confirm that the current sk-... key can use the target image model.
```

So if you want to use an image model, do not add a special permission-switching parameter to the request. Instead, confirm that the `sk-...` key you are using has access to that model.

If a request fails, check these first:

- whether the API key is correct
- whether the API key can use the target image model
- whether `model` is one of the currently available model names

<h2 id="models">Choosing a Model</h2>

| Model | Notes |
| --- | --- |
| `gpt-image-2` | OpenAI image model; recommended default |
| `gemini-3-pro-image-preview` | Gemini image model; recommended as the Gemini default |
| `gemini-3.1-flash-image-preview` | Gemini image model; can return images, but synchronous requests are more likely to time out |
| `gemini-2.5-flash-image` | Official Google Gemini image model code; availability depends on your current API key |

`Nano Banana` / `Nano Banana Pro` may appear as product or marketing names users recognize, but requests should use real model codes.

<h2 id="generate">Generate an Image</h2>

### macOS / Linux

```bash
export SORRYCODE_API_KEY='your sk-...'

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

The returned image is usually located at:

```text
data[0].b64_json
```

<h2 id="save-image">Saving the Returned Image</h2>

If you save the response as `response.json`, extract the base64 image and write it to a file.

macOS:

```bash
jq -r '.data[0].b64_json' response.json | base64 -D > image.png
```

Linux:

```bash
jq -r '.data[0].b64_json' response.json | base64 -d > image.png
```

<h2 id="edits">Edit an Image</h2>

Use:

```text
POST {{API_BASE_URL}}/images/edits
```

Minimum fields:

- `model`: an image model such as `gpt-image-2` or an enabled Gemini image model
- `prompt`: describe the edit
- `image`: local image file
- `size`: for example `1024x1024`

### macOS / Linux

```bash
export SORRYCODE_API_KEY='your sk-...'

curl {{API_BASE_URL}}/images/edits \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -F "model=gpt-image-2" \
  -F "prompt=Turn this product screenshot into a cleaner website hero visual. Keep the core UI shape and use softer lighting." \
  -F "image=@./input/product.png" \
  -F "size=1024x1024"
```

Replace `image=@./input/product.png` with a real image path on your computer.

<h2 id="parameters">Parameters</h2>

Recommended parameters:

| Parameter | Recommended value | Notes |
| --- | --- | --- |
| `model` | `gpt-image-2` or `gemini-3-pro-image-preview` | Choose the image model you want |
| `prompt` | your image description | Describe what to generate or how to edit |
| `size` | `1024x1024` | Best first request |
| `n` | `1` | Start with one image |
| `response_format` | `b64_json` | Easy to save locally |

Sizes depend on the model family. Use `1024x1024` for the first request.

Common `gpt-image-2` sizes:

| Use case | size |
| --- | --- |
| Default / square | `1024x1024` |
| Landscape | `1536x1024` |
| Portrait | `1024x1536` |
| 2K square | `2048x2048` |
| 2K landscape | `2048x1152` |
| 4K landscape | `3840x2160` |
| 4K portrait | `2160x3840` |
| Let the model choose | `auto` |

For Gemini image models, currently prefer `1024x1024` as the stable first-run size. Do not use `4096x4096` as a 4K image size; it does not meet the current upstream size constraints.

<h2 id="streaming">Streaming Requests</h2>

Some image models support streaming:

```json
{
  "stream": true,
  "partial_images": 2
}
```

Streaming returns SSE events and can help with slow or large `gpt-image-2` requests. Not every model or upstream is a good fit for streaming; for Gemini image first-run checks, use non-streaming `response_format: "b64_json"`.

<h2 id="common-issues">Common Issues</h2>

### 524

`524` usually means the request reached SorryCode, but image generation took too long without a complete response. Retry later, shorten the prompt, reduce the size, or start with a verified stable model. 4K image responses are large and are not yet promised as stable.

### 401

The API key is wrong or missing from `Authorization: Bearer ...`.

### 400

A parameter, model name, source image, or image format does not meet the requirement. If you see `images endpoint requires an image model`, check that `model` is an enabled image model.

### 503 No available compatible accounts

The current API key cannot use this image model right now. Check that the model name is correct and that this key has image access. If it still fails, contact SorryCode support.

<h2 id="next">Next Step</h2>

If you do not want to write HTTP requests, use [Skills / SorryCode Image2](/docs/skills/sorrycode-image2).
