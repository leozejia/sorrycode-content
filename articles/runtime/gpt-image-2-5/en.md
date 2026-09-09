---
title: GPT Image 2.5
slug: gpt-image-2-5
order: 3
summary: Use gpt-image-2.5-flare or gpt-image-2.5-sunburst through the SorryCode Images API; availability depends on the model catalog for your API key's group.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2.5

GPT Image 2.5 uses concrete API model IDs: `gpt-image-2.5-flare` and `gpt-image-2.5-sunburst`. `gpt-image-2.5` is the family name, not a value you can send as `model`.

SorryCode exposes both models through its OpenAI-compatible Images API. The group for your API key must allow image generation and list the model you want to use in its model catalog.

| Model | Best for |
| --- | --- |
| `gpt-image-2.5-flare` | Speed-first everyday generation, social content, and high-volume drafts |
| `gpt-image-2.5-sunburst` | Work where edit precision, subject preservation, and final quality matter most |

Both models accept text and image inputs and produce image outputs. They do not handle audio or video. The official model pages mark both models as not supporting streaming. Quality settings include `low`, `medium`, `high`, `xhigh`, `max`, and `auto`, but a particular group may not expose every option.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to read this page, use the SorryCode API key already configured in the current environment, choose an available model, generate or edit an image, save the result, and verify that the file is complete. Do not paste an API key into the conversation or write it into a project file.

<h2 id="prepare">Before You Start</h2>

1. Create or select an API key at `https://sorrycode.com/keys`.
2. Confirm that its group allows image generation and lists `gpt-image-2.5-flare` or `gpt-image-2.5-sunburst` in the model catalog.
3. For a manual request, put the key in the `Authorization: Bearer ...` header. GPT Image 2.5 does not need a separate image key or a general-purpose environment variable.

If the model catalog does not contain either ID, do not substitute the family name `gpt-image-2.5`. Switch to a group that exposes the model or ask the administrator to confirm the model configuration.

<h2 id="generate">Generate Through the Images API</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/generations
```

Create `request.json` first. This example uses Flare. Replace only the `model` value to use Sunburst:

```json
{
  "model": "gpt-image-2.5-flare",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "n": 1,
  "quality": "auto"
}
```

Send the request and replace the placeholder with your API key:

```bash
curl https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

On Windows PowerShell, use `curl.exe`:

```powershell
curl.exe https://api.sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

This page uses a non-streaming request first so you can validate the model and group configuration. GPT Image 2.5 does not use GPT Image 2's `stream` or `partial_images` examples. Check the current model catalog and response contract before adding other advanced parameters.

<h2 id="edit">Edit an Existing Image</h2>

Endpoint:

```text
POST https://api.sorrycode.com/v1/images/edits
```

Use `multipart/form-data`:

```bash
curl https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer sk-replace-with-sorrycode-key" \
  -F "model=gpt-image-2.5-sunburst" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024"
```

<h2 id="save">Save the Returned Image</h2>

- If the response contains `data[0].b64_json`, decode the Base64 data and write the image file.
- If the response contains `data[0].url`, download it promptly because temporary URLs may expire.
- An agent should confirm that the target file exists and can be read before reporting success.
- After an interrupted or timed-out request, check the previous request state before sending another paid request.

<h2 id="codex">Built-in Image Generation in Codex</h2>

Whether Codex can call an image tool depends on the tools exposed in the current session and the model catalog. When the tool is unavailable, use the Images API above. Changing the prompt cannot add a missing tool.

<h2 id="errors">Common Issues</h2>

- `400`: the family name `gpt-image-2.5` was sent instead of a concrete model ID, or the request parameters are not valid for the selected model.
- `401`: the API key is missing, wrong, or not sent as a Bearer token.
- `403`: image generation is not enabled for the current key's group.
- `503 No available compatible accounts`: the current group has no compatible image account available right now.
- `502` or `524`: an upstream failure, cancelled connection, or a synchronous request that exceeded the entrypoint wait window.

<h2 id="next">Next Step</h2>

- Use GPT Image 2: [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2)
- Set up Codex: [Models & Runtimes / Codex](/docs/runtime/codex)
- Generate Grok images: [Models & Runtimes / Grok Image Generation](/docs/runtime/grok-image)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)
