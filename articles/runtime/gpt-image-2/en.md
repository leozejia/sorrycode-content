---
title: GPT Image 2
slug: gpt-image-2
order: 2
summary: Generate images with natural language in Codex, or use gpt-image-2 through the SorryCode Images API and SorryCode Image2 Skill.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2

`gpt-image-2` is the main OpenAI image model on SorryCode. Choose the entry point that matches your task:

| Need | Recommended entry |
| --- | --- |
| Generate quickly and revise with natural language | Codex App conversation |
| Build your own integration or workflow | Images API |
| Edit local images, fix output folders, save diagnostics | SorryCode Image2 Skill |

For a first run, ask for the image directly in Codex App.

<h2 id="codex">Generate Directly in Codex</h2>

After completing [Codex setup](/docs/runtime/codex), say:

```text
Generate a clean warm podcast cover about AI coding for beginners. Leave enough room for a title.
```

Then give a concrete revision:

```text
Make the title area wider, remove some decoration, and change it to a landscape layout.
```

You do not need to write model parameters for this path. Codex handles the image call inside the conversation.

<h2 id="api">Generate through the Images API</h2>

The developer endpoint is:

```text
POST https://sorrycode.com/v1/images/generations
```

Create or select an Image2 key assigned to an image group that supports `gpt-image-2`. Do not use a Grok-group key. The API example on this page puts the key directly in the request and does not require an environment variable.

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

Send the request:

Replace `sk-replace-with-image2-group-key` with your Image2 key.

```bash
curl -N https://sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-image2-group-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json"
```

On Windows PowerShell, use `curl.exe`:

```powershell
curl.exe -N https://sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-image2-group-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json"
```

Image generation can take much longer than text. Keep `stream: true` and `partial_images: 2` so the client receives progress events before the completion event. Use the Skill below when you want the output image and diagnostics saved automatically.

<h2 id="skill">Use the SorryCode Image2 Skill</h2>

[SorryCode Image2](/docs/skills/sorrycode-image2) uses only `gpt-image-2`. It is the better path when you need to:

- edit a local PNG, JPEG, or WebP file;
- choose an exact output folder and size;
- save the prompt, request, response, and streaming events;
- repeat the same image task inside a project.

Give this instruction to Codex or Claude Code:

```text
Install SorryCode Image2 and configure the Image2 key as shown on the Skill page. Then use gpt-image-2 to generate a 1024x1024 image and save it to outputs/images/first-run/.
```

<h2 id="errors">Common Issues</h2>

- `401`: the API key is missing, wrong, or not sent as a Bearer token.
- `403`: image generation is not enabled for the API key's group.
- `400`: check the model, prompt, size, and image input format.
- `503 No available compatible accounts`: the group has no compatible image account available right now.
- No result for a long time: keep streaming enabled, shorten the prompt, or retry at `1024x1024`.

<h2 id="next">Next Step</h2>

- Set up Codex: [Models & Runtimes / Codex](/docs/runtime/codex)
- Use a reproducible workflow: [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)
