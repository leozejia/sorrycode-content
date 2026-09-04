---
title: GPT Image 2
slug: gpt-image-2
order: 2
summary: Use gpt-image-2 through the SorryCode Images API for generation, editing, and streaming; built-in Codex generation depends on the tools exposed in the current session.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2

SorryCode exposes `gpt-image-2` through an OpenAI-compatible Images API. An agent can read this page and execute the request in a Codex task, or you can call the endpoint from your own program.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to read this page, use the SorryCode API key already configured in the current environment, call the image endpoint, save the result, and verify that the file is complete. Do not paste an API key into the conversation or write it into a project file. If no usable key is configured, ask the agent to direct you to the API Key page to choose a group with image access and complete the connection.

<h2 id="codex">Built-in Image Generation in Codex</h2>

If the current Codex session exposes an image-generation tool, say:

```text
Generate a clean warm podcast cover about AI coding for beginners. Leave a clear area for the title.
```

This path uses Codex's Responses image tool and does not require manual request parameters. A custom provider may not expose that tool. When it is unavailable, use the Images API below. Changing the prompt cannot add a missing tool.

<h2 id="prepare">Before You Start</h2>

1. Create or select an API key at `https://sorrycode.com/keys`.
2. Confirm that its group allows image generation and can route `gpt-image-2`.
3. For a manual request, put the key in the `Authorization: Bearer ...` header. GPT Image 2 does not need a separate image key or a general-purpose environment variable.

When you use Codex's connection flow, the installer saves the selected key. Keys from different groups are not interchangeable just because they share the `sk-` prefix.

<h2 id="generate">Generate Through the Images API</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/generations
```

Create `request.json` first. macOS / Linux:

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

Windows PowerShell:

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

Send the request and replace the placeholder with your API key:

```bash
curl -N https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

On Windows PowerShell, use `curl.exe`:

```powershell
curl.exe -N https://api.sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

Image generation can take longer than text. Keep `stream: true` and `partial_images: 2` so the client receives progress events before the completion event. Save only the final image from the completion event.

<h2 id="edit">Edit an Existing Image</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/edits
```

Use `multipart/form-data`. The input can be PNG, JPEG, or WebP:

```bash
curl https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -F "model=gpt-image-2" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024"
```

<h2 id="save">Save the Returned Image</h2>

- `response_format: b64_json` returns Base64 data. Decode `data[0].b64_json` and write it to `.png` or the actual format returned by the API.
- `response_format: url` returns `data[0].url`. Temporary URLs may expire, so download the file promptly.
- Partial images in a stream are previews. Save the final image after the completion event.

An agent can decode, download, and write the file, but it should confirm that the target file exists and can be read before reporting success. After an interrupted or timed-out request, check the previous request state before sending another paid request.

<h2 id="agent">Let an Agent Execute It</h2>

Give the agent this page or its Markdown, then specify the task and output path:

```text
Read the GPT Image 2 integration guide. Use the SorryCode API key already configured in the current environment, call the Images API to generate a 1024x1024 image, save it to outputs/images/first-run/, and verify that the file can be read before reporting success. Do not ask me to paste an API key or write it into a file.
```

If the agent has no HTTP or file tool, it can provide the request but cannot perform the generation. Run the Curl example from this page instead.

<h2 id="errors">Common Issues</h2>

- `401`: the API key is missing, wrong, or not sent as a Bearer token.
- `403`: image generation is not enabled for the current key's group.
- `400`: check the model, prompt, size, and image input format.
- `503 No available compatible accounts`: the current group has no compatible image account available right now.
- No result for a long time: keep streaming enabled and validate the path first with `1024x1024`; after a timeout, check the previous request state before retrying.

<h2 id="next">Next Step</h2>

- Set up Codex: [Models & Runtimes / Codex](/docs/runtime/codex)
- Generate Grok images: [Models & Runtimes / Grok Image Generation](/docs/runtime/grok-image)
- Generate Grok videos: [Models & Runtimes / Grok Video Generation](/docs/runtime/grok-video)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)
