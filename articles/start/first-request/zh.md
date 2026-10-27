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

默认先通过 [Magpie](/docs/agents/magpie)接入 Agent。能正常对话就跳过这页。只有手动开发或需要区分客户端与网关问题时，才做下面的直连检查；它不用于验证 Magpie 的本地网关。

先从当前 Key 所属分组的模型目录复制准确 ID，替换对应示例中的 `MODEL_ID`。不要直接复制 Magpie 在 Agent 中显示的本地供应商前缀。密钥也要替换成自己的完整 Key，不要把真实值发到聊天里。

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

## Anthropic-compatible 示例

请求地址：

`{{ANTHROPIC_BASE_URL}}/v1/messages`

选择一把已经分配到 Anthropic-compatible 分组的 Key，并替换下面的占位值。不要使用未开放此协议或模型的分组 Key。

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
