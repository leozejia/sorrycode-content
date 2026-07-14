---
title: Grok 图片生成
slug: grok-image
order: 2
summary: 使用 SorryCode API Key 调用 Grok Imagine 图片模型，生成图片并读取返回的临时 URL。
section: runtime
section_title: 模型与工作台
section_order: 10
group: xai
group_title: xAI
group_order: 30
---

# Grok 图片生成

Grok 图片生成通过标准 REST API 使用，不需要 xAI 官方 API Key。你需要的是一把可以使用
Grok 分组的 SorryCode API Key。

> Grok CLI 的内置图片工具目前不会继承 SorryCode 自定义模型的 `base_url`。不要把
> SorryCode Key 填进内置图片工具；请使用本页的 API 请求。

<h2 id="prepare">开始前准备</h2>

1. 在 `https://sorrycode.com/keys` 创建或选择一把 API Key。
2. 确认这把 Key 使用 Grok 分组。
3. 复制这把 Grok Key，稍后直接替换请求头里的占位值。

这把 Key 可以和 Grok CLI 使用同一个 Grok 分组，但不要使用给 `SorryCode Image2` 准备的 Image2 Key。本页不要求设置环境变量。

如果你还没有 Key，先看 [开始使用 / 创建 API Key](/docs/start/create-api-key)。

<h2 id="models">选择模型</h2>

| 模型 | 适合 |
| --- | --- |
| `grok-imagine-image` | 快速草稿、较低成本的日常生成 |
| `grok-imagine-image-quality` | 更重视细节和成品质量 |

第一次可以先用 `grok-imagine-image` 跑通链路，再按需要切换质量模型。

<h2 id="request">发送第一条请求</h2>

接口：

```text
POST https://sorrycode.com/v1/images/generations
```

macOS / Linux 先创建 `request.json`：

```bash
cat > request.json <<'JSON'
{
  "model": "grok-imagine-image",
  "prompt": "A blue paper kite centered on a clean white background"
}
JSON
```

Windows PowerShell：

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

发送请求并保存响应：

把 `sk-replace-with-grok-group-key` 替换成你的 Grok 分组 Key。

```bash
curl -sS https://sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer sk-replace-with-grok-group-key" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o response.json
```

Windows PowerShell：

```powershell
curl.exe -sS https://sorrycode.com/v1/images/generations `
  -H "Authorization: Bearer sk-replace-with-grok-group-key" `
  -H "Content-Type: application/json" `
  --data-binary "@request.json" `
  -o response.json
```

成功响应会在 `data[0].url` 返回图片地址：

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

图片地址可能是临时地址。需要长期保留时，请在成功后及时下载到自己的项目或存储。

<h2 id="cli-boundary">为什么 Grok CLI 里会报 API Key 无效</h2>

SorryCode 的 Grok 一键安装会配置文字对话、Responses 和搜索所需的自定义模型地址。
当前 Grok CLI 的内置图片客户端使用另一条媒体连接，不读取这个自定义地址。

因此会出现这种现象：

- Grok 文字对话可以正常走 SorryCode；
- 内置图片工具把 SorryCode Key 发到 xAI 官方入口；
- xAI 官方入口不认识 SorryCode Key，于是返回 `Incorrect API key provided`。

这不是重新安装 Grok 可以解决的问题。当前正确入口就是本页的
`https://sorrycode.com/v1/images/generations`。

<h2 id="errors">常见问题</h2>

- `401`：Key 缺失、错误或没有按 Bearer Token 发送。
- `403`：当前 Key 的分组没有开放媒体能力。
- `400`：检查 `model`、`prompt` 和 JSON 编码；上游也可能明确拒绝某个参数。
- `503`：当前分组暂时没有可用的 Grok 图片账号。
- 返回 URL 但浏览器稍后打不开：临时地址已失效，生成后应及时下载。

<h2 id="next">下一步</h2>

- 使用 Grok 文字和搜索：[模型与工作台 / Grok](/docs/runtime/grok-cli)
- 生成或动画化视频：[模型与工作台 / Grok 视频生成](/docs/runtime/grok-video)
- 创建 API Key：[开始使用 / 创建 API Key](/docs/start/create-api-key)

上游能力参考：[xAI Image Generation](https://docs.x.ai/developers/model-capabilities/images/generation)
