---
title: GPT Image 2.5
slug: gpt-image-2-5
order: 3
summary: 使用 gpt-image-2.5-flare 快速生成图片，或使用 gpt-image-2.5-sunburst 进行高质量生成和精确编辑。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT Image 2.5

SorryCode 通过 OpenAI 兼容的 Images API 提供两个 GPT Image 2.5 模型：

| 模型 ID | 适合场景 |
| --- | --- |
| `gpt-image-2.5-flare` | 速度优先的日常生成和快速出稿 |
| `gpt-image-2.5-sunburst` | 更高质量的生成和精确图片编辑 |

两者都接受文字或图片输入，输出图片。请求中的 `model` 必须填写表格中的完整模型 ID。

如果你想让 Agent 负责安装、配置 Skill、保存图片和检查结果，请看 [SorryCode Image2](/docs/skills/sorrycode-image2)。本页只维护 GPT Image 2.5 的模型和参数。

<h2 id="prepare">配置 API Key</h2>

1. 在 [API Key 页面](https://sorrycode.com/keys) 创建或选择一把 Key。
2. 为 Key 选择包含目标模型的分组。
3. 在请求头中发送 `Authorization: Bearer YOUR_API_KEY`。

<h2 id="generate">生成图片</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/generations
```

先创建 `request.json`。日常生成建议使用 Flare：

```json
{
  "model": "gpt-image-2.5-flare",
  "prompt": "A small red paper boat floating on a calm lake",
  "size": "1024x1024",
  "quality": "auto"
}
```

发送请求：

```bash
curl -sS https://api.sorrycode.com/v1/images/generations \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  --data-binary "@request.json" \
  -o response.json
```

Windows PowerShell 使用 `curl.exe`，请求体仍从 `request.json` 读取。

<h2 id="edit">编辑图片</h2>

接口：

```text
POST https://api.sorrycode.com/v1/images/edits
```

使用 `multipart/form-data` 上传图片。精确编辑建议使用 Sunburst：

```bash
curl -sS https://api.sorrycode.com/v1/images/edits \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -F "model=gpt-image-2.5-sunburst" \
  -F "prompt=Turn this into a watercolor illustration" \
  -F "image=@input.png" \
  -F "size=1024x1024" \
  -o response.json
```

<h2 id="result">保存图片</h2>

- 返回 `data[0].b64_json` 时，将 Base64 解码为图片文件。
- 返回 `data[0].url` 时，尽快下载并保存图片。

两个模型都支持 `low`、`medium`、`high`、`xhigh`、`max` 和 `auto` 质量档位。常用尺寸为 `1024x1024`、`1536x1024` 和 `1024x1536`。

<h2 id="next">下一步</h2>

- 使用 GPT Image 2：[模型与工作台 / GPT Image 2](/docs/runtime/gpt-image-2)
- 生成 Grok 图片：[模型与工作台 / Grok 图片生成](/docs/runtime/grok-image)
- 创建 API Key：[开始使用 / 创建 API Key](/docs/start/create-api-key)
