---
title: Pi Agent
slug: pi-agent
order: 1
summary: 安装 Pi Agent，通过 Responses 或 Anthropic Messages 接入 SorryCode 模型（包括 Gemini 3.7 Flash 和 Gemini 3.8 Flash），并完成文本和文件工具验证。
section: runtime
section_title: 模型与工作台
section_order: 10
group: pi
group_title: Pi Agent
group_order: 23
---

# Pi Agent

Pi 是 [earendil-works/pi](https://github.com/earendil-works/pi) 提供的终端 Coding Agent，可以读项目、改文件和执行命令。Pi 不绑定某个模型，也不只支持一个模型。你可以在同一份配置里接入多把 Key、多个 provider、多个模型，比如 GPT、Claude、Gemini、Grok，以及 DeepSeek、GLM、Kimi、Qwen 等国产模型。

这里说的是 [pi.dev](https://pi.dev/) 对应的 Pi，不是其他同名项目。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="prepare-key">准备 API Key</h2>

Pi 可以通过 SorryCode 的 Responses API 或 Anthropic Messages API 调用模型。在 [SorryCode API Key 页面](https://sorrycode.com/keys) 为每个模型分组准备 Key，例如 GPT、Claude、Gemini、Grok 或国产模型分组。下面的 Gemini 示例使用 Gemini 分组 Key。

不同 Key 属于不同分组，看到的模型也不同。先查询每把 Key 实际开放的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 SorryCode API Key>"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <你的 SorryCode API Key>"
```

配置时遵循三个原则：

- 只把 `/v1/models` 返回的准确模型 ID 写入常规模型目录。
- 未返回但可路由的别名只用于诊断，不写入 `models.json`。同一模型的别名和规范 ID 不得同时配置。
- 每把 Key 单独使用一个 provider 名。Pi 的 `/login` 按 provider 保存 Key，重复登录同一个 provider 会覆盖旧 Key。

例如 Claude 分组返回 `claude-opus-5` 和 `claude-opus-4-6`，就用 Claude 分组的 Key 配这两个模型；Grok 分组返回 `grok-4.6`，就用 Grok 分组的 Key 配 `grok-4.6`。`gemini-3.7-flash` 和 `gemini-3.8-flash` 都使用 Gemini 分组的 Key。

<h2 id="install">安装 Pi</h2>

Pi 当前要求 Node.js `22.19.0` 或更高版本。先检查：

```bash
node --version
npm --version
```

如果命令不存在或版本过低，先阅读 [Node.js](/docs/environment/nodejs)。环境准备好后，使用 Pi 官方包安装：

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

macOS、Linux 和 Windows 都使用这条 npm 命令。安装后确认版本：

```bash
pi --version
```

<h2 id="configure">在 models.json 配置多模型</h2>

Pi 的自定义模型配置文件是：

- macOS / Linux：`~/.pi/agent/models.json`
- Windows：`%USERPROFILE%\.pi\agent\models.json`

macOS / Linux 可以先创建目录并打开文件：

```bash
mkdir -p ~/.pi/agent
nano ~/.pi/agent/models.json
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME\.pi\agent" | Out-Null
notepad "$HOME\.pi\agent\models.json"
```

如果文件里已有其他 provider，把下面的内容合并到 `providers` 中，不要覆盖原有配置。下面的 provider 条目只用于说明多 Key 结构，不是需要照抄的完整模型目录：

```json
{
  "providers": {
    "sorrycode-gpt": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "gpt-5.6-sol",
          "name": "GPT-5.6 Sol",
          "contextWindow": 1050000,
          "maxTokens": 128000,
          "input": ["text", "image"],
          "reasoning": true,
          "thinkingLevelMap": {
            "off": "none",
            "minimal": null,
            "low": "low",
            "medium": "medium",
            "high": "high",
            "xhigh": "xhigh",
            "max": "max"
          }
        }
      ]
    },
    "sorrycode-gemini": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "gemini-3.7-flash",
          "name": "Gemini 3.7 Flash via SorryCode",
          "input": ["text"]
        },
        {
          "id": "gemini-3.8-flash",
          "name": "Gemini 3.8 Flash via SorryCode",
          "input": ["text"]
        }
      ]
    },
    "sorrycode-claude": {
      "baseUrl": "https://sorrycode.com",
      "api": "anthropic-messages",
      "models": [
        {
          "id": "claude-opus-5",
          "name": "Claude Opus 5",
          "contextWindow": 200000,
          "maxTokens": 16384,
          "input": ["text"],
          "reasoning": false
        },
        {
          "id": "claude-opus-4-6",
          "name": "Claude Opus 4.6",
          "contextWindow": 200000,
          "maxTokens": 16384,
          "input": ["text"],
          "reasoning": false
        }
      ]
    },
    "sorrycode-cn": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "deepseek-v4-flash",
          "name": "DeepSeek V4 Flash",
          "contextWindow": 1000000,
          "maxTokens": 384000,
          "input": ["text"],
          "reasoning": true,
          "thinkingLevelMap": {
            "off": null,
            "minimal": null,
            "low": "low",
            "medium": "medium",
            "high": "high",
            "xhigh": "xhigh",
            "max": "max"
          }
        }
      ]
    }
  }
}
```

provider 名只是本地标识。每把 Key 对应一个 provider；同一 Key 分组返回的多个模型可以放进该 provider 的 `models` 数组。需要其他分组时，按同样结构新增 provider，不要覆盖已有 Key。

字段说明：

- `id`：发给 API 的准确模型 ID，来自对应 Key 的 `/v1/models`。
- `contextWindow`：Pi 用来计算上下文占用和自动压缩。省略时 Pi 使用 128,000。
- `maxTokens`：单次响应最大输出。省略时 Pi 使用 16,384。
- `input`：`["text"]` 只支持文本，`["text", "image"]` 支持文本和图片。
- `reasoning`：模型支持推理时设为 `true`。
- `thinkingLevelMap`：控制 Pi 显示哪些思考档位。字符串表示支持并发送该值，`null` 表示隐藏不支持的档位；`xhigh` 和 `max` 必须显式写入才会显示。

模型 ID、能力和思考档位都会变化。只保留实际需要且已经用当前 Key 验证过的模型，不要把其他平台或旧配置的完整目录直接复制进来。

<h2 id="login">为每个 provider 保存 API Key</h2>

运行 Pi：

```bash
pi
```

进入界面后，为每个 provider 分别登录：

```text
/login sorrycode-gpt
/login sorrycode-gemini
/login sorrycode-claude
/login sorrycode-cn
```

示例列出上面的 provider。实际使用时，为每个已配置 provider 执行一次 `/login`，并粘贴对应分组的 Key。Pi 会把凭证保存到自己的认证文件中，不需要设置环境变量，也不要把 Key 写进 `models.json`。

然后输入 `/model`，选择 provider 和模型，例如 `sorrycode-gemini/gemini-3.7-flash`。

要确认配置和认证都正确，先运行：

```bash
pi --list-models
pi auth check --provider sorrycode-claude --model claude-opus-5 --json
```

`--list-models` 能看到你配置的所有模型；`auth check` 返回 `ready` 表示该 provider 已保存可用 Key。

<h2 id="verify">验证文本和工具调用</h2>

用你当前能用的任意模型验证最小文本响应。下面以 `claude-opus-5` 为例：

```bash
pi --provider sorrycode-claude --model claude-opus-5 --no-tools --no-session -p "Reply with PI_SORRYCODE_OK only."
```

看到 `PI_SORRYCODE_OK` 后，可以用当前支持工具调用的模型在空测试目录中验证文件工具。下面继续使用 GPT 示例：

```bash
mkdir pi-sorrycode-test
cd pi-sorrycode-test
pi --provider sorrycode-gpt --model gpt-5.6-sol --no-session -p "Create pi-check.txt containing PI_TOOL_OK and a final newline. Do not modify other files."
```

任务结束后找到 `pi-check.txt`，并确认内容是 `PI_TOOL_OK`。这说明该模型和 Pi 的工具调用链路都已可用。

<h2 id="thinking">设置思考深度</h2>

在会话内按 `Shift+Tab` 循环思考深度，或用 `/settings` 设置默认思考深度。也可以直接启动：

```bash
pi --provider <provider> --model <model> --thinking <level>
```

例如：

```bash
pi --provider sorrycode-gpt --model gpt-5.6-sol --thinking max
```

思考档位是否真的可用，要用最小请求实际验证，不要只看映射里写了什么。如果上游返回 `400`（例如 `level "xhigh" not supported`），说明该档位当前不可用；即使 Pi 里显示了它，请求也会失败。

<h2 id="common-issues">常见问题</h2>

- `pi` 命令不存在：关闭并重新打开终端，再检查 npm 全局命令目录是否在 `PATH` 中
- `/login` 中没有某个 provider：先保存 `models.json`，再重新启动 Pi
- `/model` 中没有目标模型：检查 JSON 格式、认证状态、模型条目和 Key 所属分组
- `401`：Key 不完整、已失效，或保存的不是当前所选分组的 Key
- `404` 或 model not found：重新查询 `/v1/models`，使用返回结果中的准确 ID
- 能回复但不能创建文件：确认使用经过验证的模型，并检查当前任务是否允许 `write` 工具
- Windows 阻止 `pi.ps1`：阅读 [Windows PowerShell](/docs/environment/windows-powershell)
- `/v1/responses` 返回 `502`：模型可能被列出但上游分组暂时不可用；先重试或查询 SorryCode 状态，不要只改 Pi 配置
- `400` 且提示 `level "..." not supported`：上游不支持当前思考档位，先改用支持档位，或把 `thinkingLevelMap` 中对应值设为 `null`
- 模型在 `models.json` 里但 `/model` 看不到：先确认该 provider 已登录，运行 `pi auth check --provider <provider> --model <model> --json`
- 模型 ID 不在 `/v1/models` 里：不要加入常规模型目录；如需排障，可以单独发送最小 `/v1/responses` 请求，但成功也不代表应该同时保存该别名
- 不同 Key 的模型看不到：不要在同一 provider 下覆盖 Key，给每组模型单独建 provider

参考：[Pi 官网](https://pi.dev/)、[Pi 官方仓库](https://github.com/earendil-works/pi)、[Pi 自定义模型文档](https://pi.dev/docs/latest/models)。
