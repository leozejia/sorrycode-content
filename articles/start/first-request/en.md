---
title: First Request
slug: first-request
order: 4
summary: Use one minimal request to validate the API key, Base URL, and network path. This page is a manual-path and troubleshooting reference, not the default beginner entry.
section: start
section_title: Getting Started
section_order: 1
---

# First Request

Use [Magpie](/docs/agents/magpie) for the default agent setup. Skip this page if chat works. The direct checks below are only for manual development or separating client and gateway failures; they do not test Magpie's local gateway.

Copy an exact model ID from the current key group's model catalog and replace `MODEL_ID` in the matching example. Do not copy a local provider prefix displayed by Magpie in an agent. Replace the key placeholder with your own complete key, and keep it out of chat.

## First Decide Which Protocol You Want to Verify

- **OpenAI-compatible**
  fits `Codex`-style runtimes
- **Anthropic-compatible**
  fits `Claude Code`-style runtimes

## OpenAI-compatible Example

Request URL:

`{{API_BASE_URL}}/chat/completions`

Choose a key assigned to an OpenAI-compatible group and replace the placeholder below with the full `sk-...` value. This page is a one-time check, so it does not require an environment variable.

### macOS / Linux

```bash
curl {{API_BASE_URL}}/chat/completions \
  -H "Authorization: Bearer sk-replace-with-openai-group-key" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "MODEL_ID",
    "messages": [
      {"role": "user", "content": "Reply with READY."}
    ]
  }'
```

### Windows PowerShell

```powershell
$body = @{
  model = "MODEL_ID"
  messages = @(
    @{
      role = "user"
      content = "Reply with READY."
    }
  )
} | ConvertTo-Json -Depth 10 -Compress

$payloadFile = Join-Path $PWD "chat_payload.json"
[System.IO.File]::WriteAllText(
  $payloadFile,
  $body,
  [System.Text.UTF8Encoding]::new($false)
)

curl.exe "{{API_BASE_URL}}/chat/completions" `
  -H "Authorization: Bearer sk-replace-with-openai-group-key" `
  -H "Content-Type: application/json; charset=utf-8" `
  --data-binary "@$payloadFile"
```

## Anthropic-compatible Example

Request URL:

`{{ANTHROPIC_BASE_URL}}/v1/messages`

Choose a key assigned to an Anthropic-compatible group and replace the placeholder below. Do not use a Grok or Codex key for this check.

### macOS / Linux

```bash
curl {{ANTHROPIC_BASE_URL}}/v1/messages \
  -H "x-api-key: sk-replace-with-anthropic-group-key" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "MODEL_ID",
    "max_tokens": 16,
    "messages": [
      {"role": "user", "content": "Reply with READY."}
    ]
  }'
```

### Windows PowerShell

```powershell
$body = @{
  model = "MODEL_ID"
  max_tokens = 16
  messages = @(
    @{
      role = "user"
      content = "Reply with READY."
    }
  )
} | ConvertTo-Json -Depth 10 -Compress

$payloadFile = Join-Path $PWD "messages_payload.json"
[System.IO.File]::WriteAllText(
  $payloadFile,
  $body,
  [System.Text.UTF8Encoding]::new($false)
)

curl.exe "{{ANTHROPIC_BASE_URL}}/v1/messages" `
  -H "x-api-key: sk-replace-with-anthropic-group-key" `
  -H "anthropic-version: 2023-06-01" `
  -H "Content-Type: application/json; charset=utf-8" `
  --data-binary "@$payloadFile"
```

## Pass Criteria

- you receive a successful response
- the response body includes model output

If both are true, at least these layers are working:

- the API key is valid
- the Base URL is correct
- the current machine can reach the gateway

## If It Fails

- `401` / `404` / `429`
  go to [FAQ](/docs/start/common-errors)
- timeout / TLS
  go to [FAQ / Network and Connections](/docs/start/common-errors#network)
- Windows script issues
  go to [FAQ / Windows PowerShell](/docs/start/common-errors#windows-powershell)
