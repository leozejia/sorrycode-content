---
title: Grok Image Generation
slug: grok-image
order: 2
summary: Use a SorryCode API key with Grok Imagine image models, then read the temporary image URL from the response.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: xai
group_title: xAI
group_order: 30
---

# Grok Image Generation

Use Grok image generation through the REST API. You do not need an official xAI API key. You need a SorryCode API key assigned to a Grok group.

> Grok CLI's built-in image tools currently do not inherit the custom `base_url` from a SorryCode model. Do not put a SorryCode key into those built-in media tools. Use the API request on this page.

<h2 id="prepare">Before You Start</h2>

1. Create or select an API key at `https://sorrycode.com/keys`.
2. Make sure the key uses a Grok group.
3. Store the key in the `SORRYCODE_API_KEY` environment variable.

If you do not have a key yet, read [Getting Started / Create API Key](/docs/start/create-api-key).

<h2 id="models">Choose a Model</h2>

| Model | Best for |
| --- | --- |
| `grok-imagine-image` | Fast drafts and lower-cost everyday generation |
| `grok-imagine-image-quality` | More detail and final-output quality |

For a first test, use `grok-imagine-image`, then switch to the quality model when the task needs it.

<h2 id="request">Send the First Request</h2>

Endpoint:

```text
POST https://sorrycode.com/v1/images/generations
```

Create `request.json` on macOS / Linux:

```bash
cat > request.json <<'JSON'
{
  "model": "grok-imagine-image",
  "prompt": "A blue paper kite centered on a clean white background"
}
JSON
```

Windows PowerShell:

```powershell
$json = @'
{
  "model": "grok-imagine-image",
  "prompt": "A blue paper kite centered on a clean white background"
}
'@

[System.IO.File]::WriteAllText(
  "request.json",
  $json,
  [System.Text.UTF8Encoding]::new($false)
)
```

Send the request and save the response:

```bash
curl -sS https://sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o response.json
```

Windows PowerShell:

```powershell
curl.exe -sS https://sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer $env:SORRYCODE_API_KEY" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json" `
  -o response.json
```

A successful response returns the image URL at `data[0].url`:

```json
{
  "data": [
    {
      "url": "https://...",
      "mime_type": "image/jpeg"
    }
  ]
}
```

The image URL may be temporary. Download the image to your own project or storage soon after a successful request.

<h2 id="cli-boundary">Why Grok CLI Can Report an Invalid API Key</h2>

SorryCode's Grok installer configures the custom model address used for text, Responses, and search. Grok CLI's built-in image client currently uses a separate media connection and does not read that custom address.

This creates a confusing split:

- Grok text requests work through SorryCode;
- the built-in image tool sends the SorryCode key to the official xAI endpoint;
- the official endpoint does not recognize the SorryCode key and returns `Incorrect API key provided`.

Reinstalling Grok does not change this boundary. Use
`https://sorrycode.com/v1/images/generations` instead.

<h2 id="errors">Common Issues</h2>

- `401`: the key is missing, wrong, or not sent as a Bearer token.
- `403`: media access is not enabled for the key's group.
- `400`: check `model`, `prompt`, and JSON encoding; the upstream API may also reject a parameter explicitly.
- `503`: the group has no Grok image account available right now.
- The returned URL stops opening later: it was temporary, so download successful outputs promptly.

<h2 id="next">Next Step</h2>

- Use Grok for text and search: [Models & Runtimes / Grok](/docs/runtime/grok-cli)
- Generate or animate video: [Models & Runtimes / Grok Video Generation](/docs/runtime/grok-video)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)

Upstream capability reference: [xAI Image Generation](https://docs.x.ai/developers/model-capabilities/images/generation)
