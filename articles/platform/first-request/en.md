---
title: First Request
slug: first-request
order: 5
summary: Use one minimal request to validate the API key, Base URL, and network path. This page is a manual-path and troubleshooting reference, not the default beginner entry.
section: platform
section_title: Platform
section_order: 8
---

# First Request

This page mainly serves two cases:

- you are on the manual path and want to verify the connection directly
- the installer ended with a failed connectivity check and you want to verify it yourself

If one-click install already finished and the desktop app works normally, you can usually skip this step for now.

## First Decide Which Protocol You Want to Verify

- **OpenAI-compatible**
  fits `Codex`-style runtimes
- **Anthropic-compatible**
  fits `Claude Code`-style runtimes

## OpenAI-compatible Example

Request URL:

`{{API_BASE_URL}}/chat/completions`

### macOS / Linux

```bash
export OPENAI_API_KEY='your sk-...'

curl {{API_BASE_URL}}/chat/completions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-5.4",
    "messages": [
      {"role": "user", "content": "Reply with READY."}
    ]
  }'
```

### Windows PowerShell

```powershell
if (-not $env:OPENAI_API_KEY) {
  throw "OPENAI_API_KEY is not set."
}

$body = @{
  model = "gpt-5.4"
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
  -H "Authorization: Bearer $env:OPENAI_API_KEY" `
  -H "Content-Type: application/json; charset=utf-8" `
  --data-binary "@$payloadFile"
```

## Anthropic-compatible Example

Request URL:

`{{ANTHROPIC_BASE_URL}}/v1/messages`

### macOS / Linux

```bash
export SORRYCODE_API_KEY='your sk-...'

curl {{ANTHROPIC_BASE_URL}}/v1/messages \
  -H "x-api-key: $SORRYCODE_API_KEY" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "claude-sonnet-4-5",
    "max_tokens": 16,
    "messages": [
      {"role": "user", "content": "Reply with READY."}
    ]
  }'
```

### Windows PowerShell

```powershell
if (-not $env:SORRYCODE_API_KEY) {
  throw "SORRYCODE_API_KEY is not set."
}

$body = @{
  model = "claude-sonnet-4-5"
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
  -H "x-api-key: $env:SORRYCODE_API_KEY" `
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
  go to [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
- timeout / TLS
  go to [Environment / Node.js](/docs/environment/nodejs#network)
- Windows script issues
  go to [Environment / Windows PowerShell](/docs/environment/windows-powershell)
