---
title: 工具不是模型
slug: tools-and-models
order: 3
summary: 先分清工作台、模型、API Key 和 Base URL，再按 GPT→Codex、Claude→Claude Code 的默认路径开始。
section: platform
section_title: Platform
section_order: 8
---

# 工具不是模型

很多新手会把几件事混在一起：

```text
Codex、Claude Code、GPT、Claude、API Key、Base URL、SorryCode
```

这页只解决一个问题：

```text
我到底是在用工具，还是在用模型？
```

先记住一句话：

```text
Codex / Claude Code 是工作台，GPT / Claude 是模型，SorryCode 是把工作台接到模型上的入口。
```

## 先分清这些名字

| 名字 | 小白先这样理解 |
| --- | --- |
| `SorryCode` | 给你 API Key、余额和模型入口 |
| `Codex` | GPT 路径的 AI 工作台 |
| `Claude Code` | Claude 路径的 AI 工作台 |
| `GPT / Claude / Gemini` | 真正思考和生成内容的模型 |
| `API Key` | 证明这是你的账号在调用模型的钥匙 |
| `Base URL` | 工作台连接 SorryCode 的地址 |

你打开的通常不是模型，而是工作台。

工作台负责读文件、组织上下文、调用工具、执行命令。模型负责理解、推理和生成。

SorryCode 负责让这些工作台通过你的 API Key 调用模型，并从你的余额里记录用量。

## 默认怎么选

如果你不知道怎么选，先按默认路径走。

| 你想用什么 | 默认入口 |
| --- | --- |
| GPT / OpenAI-compatible 路径 | [Runtime / Codex](/docs/runtime/codex) |
| Claude / Anthropic-compatible 路径 | [Runtime / Claude Code](/docs/runtime/claude-code) |
| 只是创建钥匙 | [Platform / 创建 API Key](/docs/platform/create-api-key) |
| 想先理解成本 | [Platform / AI 成本怎么计算](/docs/platform/ai-cost-basics) |

如果你完全不知道选哪个，先选 `Codex`。

它是 GPT 路径最直接的新手入口。

## 为什么不建议一开始乱接

你可能会看到别人说：

```text
Claude Code 也能跑 GPT。
```

```text
某些 agent 也能接各种自定义模型。
```

很多时候，能跑是真的。

但能跑，不代表适合作为新手默认路径。

agent 每一轮请求里，不只是你打的那句话。它还会带上历史、工具信息、文件片段、项目规则、压缩摘要和工作状态。

不同工作台组织这些内容的方式不一样。

工作台和模型不匹配时，可能出现：

- 每几轮都像重新读项目
- 上下文复用不理想
- 同样任务消耗更多
- 会话越跑越慢
- 有回复，但推进效率很低

这不是说某个工具不好。

它只是默认路径问题。

新手先把默认路径跑通，再去玩自定义接入。

## SorryCode 一键安装在做什么

一键安装会尽量帮你把三件事接好：

```text
工作台 + SorryCode 地址 + 你的 API Key
```

比如：

- 安装 Codex 时，会把 Codex 接到 `{{API_BASE_URL}}`
- 安装 Claude Code 时，会把 Claude Code 接到 `{{ANTHROPIC_BASE_URL}}`
- 安装过程中会要求你填入自己的 `sk-...`

你不用第一天就理解所有配置文件。

先知道它是在帮你把工作台接到 SorryCode，就够了。

## 成本在哪里看

成本不是这页的主题。

这里只给一个入口：

```text
AI 消耗通常落回 input、output、cache。
```

为什么 agent 看起来没写几个字也会消耗很多，继续看 [Platform / AI 成本怎么计算](/docs/platform/ai-cost-basics)。

## 下一步

- 不知道自己适不适合：看 [Platform / SorryCode 适合谁](/docs/platform/who-is-sorrycode-for)
- 想理解成本：看 [Platform / AI 成本怎么计算](/docs/platform/ai-cost-basics)
- 想走 GPT 路径：看 [Runtime / Codex](/docs/runtime/codex)
- 想走 Claude 路径：看 [Runtime / Claude Code](/docs/runtime/claude-code)
- 还没有 API Key：看 [Platform / 创建 API Key](/docs/platform/create-api-key)
