---
title: GPT Image 2.5
slug: gpt-image-2-5
order: 3
summary: Use gpt-image-2.5-flare for fast generation or gpt-image-2.5-sunburst for high-quality generation and precise editing.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2.5

SorryCode provides two GPT Image 2.5 models through its OpenAI-compatible Images API:

| Model ID | Best for |
| --- | --- |
| `gpt-image-2.5-flare` | Fast everyday generation and rapid drafts |
| `gpt-image-2.5-sunburst` | Higher-quality generation and precise image editing |

Both models accept text or image inputs and produce images. The request must use one of the full model IDs in the table.

<h2 id="prepare">Configure an API Key</h2>

1. Create or select a key on the [API Key page](https://sorrycode.com/keys).
2. Choose a group that includes the model you want to use.
3. Send the key as `Authorization: Bearer YOUR_API_KEY`.

<h2 id="generate">Generate an Image</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/generations
```

Create `request.json`. Flare is the recommended default for everyday generation:

```json
{
  "model": "gpt-image-2.5-flare",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "quality": "auto"
}
```

Send the request:

```bash
curl -sS https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o response.json
```

On Windows PowerShell, use `curl.exe` and keep the request body in `request.json`.

<h2 id="edit">Edit an Image</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/edits
```

Upload the image as `multipart/form-data`. Sunburst is recommended for precise editing:

```bash
curl -sS https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=gpt-image-2.5-sunburst" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024" \
  -o response.json
```

<h2 id="result">Save the Image</h2>

- If the response contains `data[0].b64_json`, decode the Base64 value into an image file.
- If the response contains `data[0].url`, download and save the image promptly.

Both models support `low`, `medium`, `high`, `xhigh`, `max`, and `auto` quality. Common sizes are `1024x1024`, `1536x1024`, and `1024x1536`.

<h2 id="next">Next Step</h2>

- Use GPT Image 2: [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2)
- Generate Grok images: [Models & Runtimes / Grok Image Generation](/docs/runtime/grok-image)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)
