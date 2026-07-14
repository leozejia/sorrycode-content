---
title: 首条请求
slug: first-request
order: 4
summary: 用一条最小请求验证 API Key、Base URL 和网络链路都正常工作。
section: start
section_title: 开始使用
section_order: 1
---

# 首条请求

这页主要给两种场景用：

- 你走的是手动安装，想先确认链路真的通了
- 一键安装最后的连通性检查失败了，你想自己再核一遍

如果你已经完成一键安装，而且桌面 App 能正常使用，这一步通常可以先跳过。

## 先判断你要验证哪种协议

- **OpenAI-compatible**
  适合 `Codex` 这类 runtime
- **Anthropic-compatible**
  适合 `Claude Code` 这类 runtime

## OpenAI-compatible 示例

请求地址：

`{{API_BASE_URL}}/chat/completions`

选择一把已经分配到 OpenAI-compatible 分组的 Key，并把下面的占位值替换成完整的 `sk-...`。这页只做一次性验证，不要求先设置环境变量。

### macOS / Linux

```bash
curl {{API_BASE_URL}}/chat/completions \
  -H "Authorization: Bearer sk-replace-with-openai-group-key" \
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
  -H "Authorization: Bearer sk-replace-with-openai-group-key" `
  -H "Content-Type: application/json; charset=utf-8" `
  --data-binary "@$payloadFile"
```

## Anthropic-compatible 示例

请求地址：

`{{ANTHROPIC_BASE_URL}}/v1/messages`

选择一把已经分配到 Anthropic-compatible 分组的 Key，并替换下面的占位值。不要拿 Grok 或 Image2 Key 来做这条验证。

### macOS / Linux

```bash
curl {{ANTHROPIC_BASE_URL}}/v1/messages \
  -H "x-api-key: sk-replace-with-anthropic-group-key" \
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
  -H "x-api-key: sk-replace-with-anthropic-group-key" `
  -H "anthropic-version: 2023-06-01" `
  -H "Content-Type: application/json; charset=utf-8" `
  --data-binary "@$payloadFile"
```

## 通过标准

- 返回成功状态
- 返回体里能看到模型输出

如果这两条都满足，说明至少这几层是通的：

- API Key 可用
- Base URL 正确
- 当前机器到网关的网络没拦住

## 如果失败

- `401 / 404 / 429`
  去看 [排障 / 常见问题](/docs/troubleshoot/common-errors)
- 超时 / TLS
  去看 [环境准备 / Node.js](/docs/environment/nodejs#network)
- Windows 脚本问题
  去看 [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)
