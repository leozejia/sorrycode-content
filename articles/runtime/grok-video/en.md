---
title: Grok Video Generation
slug: grok-video
order: 3
summary: Submit Grok text-to-video or image-to-video jobs through SorryCode, then poll the request_id until the job is done, failed, or expired.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: xai
group_title: xAI
group_order: 30
---

# Grok Video Generation

Grok video uses an asynchronous API. The first request creates a job and returns a `request_id`. You must then call the status endpoint until the job becomes `done`, `failed`, or `expired`.

This page covers the three paths verified on SorryCode production:

- text-to-video generation;
- image-to-video generation;
- polling a result by `request_id`.

> Grok CLI's built-in `image_to_video` tool currently does not inherit the custom `base_url` from a SorryCode model. When using a SorryCode key, use the REST API on this page.

<h2 id="models">Choose a Model</h2>

| Task | Model |
| --- | --- |
| Generate video from text | `grok-imagine-video` |
| Animate a still image | `grok-imagine-video-1.5` |

Video usage is priced by output duration and resolution. For a first test, use a short duration at `480p`, then raise the specification for a real task.

<h2 id="text-to-video">Text to Video</h2>

Submission endpoint:

```text
POST https://sorrycode.com/v1/videos/generations
```

Create `request.json` on macOS / Linux:

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

Windows PowerShell:

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

Send the request and save the job response:

```bash
curl -sS https://sorrycode.com/v1/videos/generations \
  -H "Authorization: Bearer $SORRYCODE_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o video-request.json
```

Windows PowerShell:

```powershell
curl.exe -sS https://sorrycode.com/v1/videos/generations `
  -H "Authorization: Bearer $env:SORRYCODE_API_KEY" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json" `
  -o video-request.json
```

A successful submission returns:

```json
{
  "request_id": "..."
}
```

This is not the final video. Continue with the polling step.

<h2 id="image-to-video">Image to Video</h2>

Image-to-video uses the same submission endpoint. Switch to `grok-imagine-video-1.5` and provide a publicly readable image URL or data URI:

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

Save this body as UTF-8 without BOM in `request.json`, then submit it with the same `curl` command from the previous section. The upstream service cannot read an image URL that requires sign-in, exists only on a private network, or expires too quickly.

<h2 id="poll">Poll the Result</h2>

Status endpoint:

```text
GET https://sorrycode.com/v1/videos/{request_id}
```

macOS / Linux:

```bash
REQUEST_ID=$(jq -r '.request_id' video-request.json)

while true; do
  RESULT=$(curl -sS \
    -H "Authorization: Bearer $SORRYCODE_API_KEY" \
    "https://sorrycode.com/v1/videos/$REQUEST_ID")

  STATUS=$(printf '%s' "$RESULT" | jq -r '.status')
  printf 'status=%s\n' "$STATUS"

  case "$STATUS" in
    done)
      printf '%s' "$RESULT" | jq -r '.video.url'
      break
      ;;
    failed|expired)
      printf '%s' "$RESULT" | jq .
      break
      ;;
  esac

  sleep 5
done
```

Windows PowerShell:

```powershell
$requestId = (Get-Content "video-request.json" -Raw | ConvertFrom-Json).request_id

do {
  Start-Sleep -Seconds 5
  $result = curl.exe -sS `
    -H "Authorization: Bearer $env:SORRYCODE_API_KEY" `
    "https://sorrycode.com/v1/videos/$requestId" | ConvertFrom-Json
  $result.status
} while ($result.status -eq "pending")

if ($result.status -eq "done") {
  $result.video.url
} else {
  $result | ConvertTo-Json -Depth 10
}
```

Keep waiting while the status is `pending`. Read `video.url` when it becomes `done`. Stop and inspect the response on `failed` or `expired`. Do not poll forever, and do not treat the initial submission response as the video file.

<h2 id="errors">Common Issues</h2>

- `401`: the API key is missing, wrong, or not sent as a Bearer token.
- `403`: media access is not enabled for the key's Grok group.
- `400`: check the model, prompt, duration, resolution, and image field.
- `202 pending`: normal; the job is still generating.
- `failed`: the job ended; inspect the response before submitting again.
- `expired`: the result expired and the job must be submitted again.
- Image-to-video fails: make sure the image URL is publicly readable, or use a valid data URI.

<h2 id="next">Next Step</h2>

- Generate a source image: [Models & Runtimes / Grok Image Generation](/docs/runtime/grok-image)
- Use Grok for text and search: [Models & Runtimes / Grok](/docs/runtime/grok-cli)
- Create an API key: [Getting Started / Create API Key](/docs/start/create-api-key)

Upstream capability reference: [xAI Image-to-Video](https://docs.x.ai/developers/model-capabilities/video/image-to-video)
