---
title: 工具不是模型
slug: tools-and-models
order: 2
summary: 先分清 SorryCode、Codex、Claude Code、GPT 和 Claude 分别负责什么，再按默认组合选择工具，避免能跑但烧钱。
section: platform
section_title: Platform
section_order: 8
---

# 工具不是模型

很多人第一次用 SorryCode，会把几件事混在一起：`Codex`、`Claude Code`、`GPT`、`Claude`、`API Key`、`Base URL`。

先别急着背术语。你只要先记住这两条：

```text
想用 GPT，默认先用 Codex。
```

```text
想用 Claude，默认先用 Claude Code。
```

不是因为别的组合一定不能跑，而是因为新手第一天最重要的不是折腾兼容性，而是少走弯路，把任务稳定跑起来。

<h2 id="what-each-piece-does">它们分别负责什么</h2>

可以先这样理解：

| 名字 | 小白先这样理解 |
| --- | --- |
| `SorryCode` | 给你 API Key、额度和模型入口 |
| `Codex` | GPT 路径的 AI 工作台，能读项目、改文件、跑命令 |
| `Claude Code` | Claude 路径的 AI 工作台，能读项目、改文件、跑命令 |
| `GPT / Claude` | 真正思考和生成内容的模型 |
| `API Key` | 证明这是你的账号在调用模型的钥匙 |
| `Base URL` | 工作台连接 SorryCode 的地址 |

你打开的不是模型，而是工作台。

`Codex`、`Claude Code` 这类工作台会帮你读文件、组织上下文、调用工具、执行命令。`GPT`、`Claude` 这类模型负责生成答案和判断下一步。

SorryCode 负责把工作台接到模型上，并用你的 API Key 记录额度和用量。

<h2 id="which-one-to-use">我应该选哪个</h2>

如果你只是想开始用，按这张表选：

| 你现在想做什么 | 默认先去哪里 |
| --- | --- |
| 用 GPT 做项目、改文件、跑长任务 | [Runtime / Codex](/docs/runtime/codex) |
| 用 Claude 做项目、改文件、跑长任务 | [Runtime / Claude Code](/docs/runtime/claude-code) |
| 只是创建一把钥匙 | [Platform / 创建 API Key](/docs/platform/create-api-key) |
| 手动验证 API Key 和地址能不能通 | [Platform / 首条请求](/docs/platform/first-request) |
| 想用 OpenClaw 或 Hermes Agent | 先当成进阶自定义接入 |

如果你完全不知道选哪个，先选 `Codex`。它是当前 GPT 路径最直接的新手入口。

<h2 id="why-not-cross-wire">为什么不建议一开始乱接</h2>

你可能会看到别人说：`Claude Code` 也能跑 GPT，`OpenClaw` 也能接 GPT，`Hermes Agent` 也能接自定义模型。

这些说法很多时候没错。

但能跑，不等于适合你当默认方案。

Agent 每一轮请求里，不只是你打的那句话。它还会带上项目上下文、工具信息、历史记录、文件片段、压缩摘要和自己的工作状态。

不同工作台组织这些内容的方式不一样。你把模型接到不适合的工作台里，可能会出现这些情况：

- 每次都像重新读项目
- 上下文复用不理想
- 同样任务消耗更多 API 量
- 会话越跑越贵
- 看起来有回复，但推进很慢

所以这不是能力鄙视链，也不是说某个工具不好。它只是一个默认路径问题。

小白先把默认路径跑通，再去玩自定义接入。

<h2 id="sorrycode-one-click-install">SorryCode 一键安装在做什么</h2>

一键安装不是只帮你装软件。

它会尽量帮你把三件事配到一起：

```text
工作台 + SorryCode 地址 + 你的 API Key
```

比如：

- 安装 Codex 时，会把 Codex 接到 `{{API_BASE_URL}}`
- 安装 Claude Code 时，会把 Claude Code 接到 `{{ANTHROPIC_BASE_URL}}`
- 安装过程中会要求你填入自己的 `sk-...`

你不用第一天就理解所有配置文件。先知道它在帮你把工作台接到 SorryCode，就够了。

<h2 id="when-to-change-model">什么时候可以换模型</h2>

可以换，但先确认三件事：

- 你现在打开的是哪个工作台
- 你要用的是 GPT 还是 Claude
- 你能接受成本、缓存和上下文表现可能变化

如果只是想用新的 GPT 模型，优先在 `Codex` 里换。

如果只是想用 Claude 模型，优先按 `Claude Code` 的路径走。

不要为了追一个新模型名，就随手把它塞进另一个工作台里。

<h2 id="bad-pairing-signals">什么时候说明可能接错了</h2>

出现这些情况，先停下来检查工具和模型是不是匹配：

- 没做多少事，用量涨得很快
- 每开几轮都像重新读项目
- 明明只是小改动，却消耗很多 API 量
- 你把 GPT 填进 Claude Code，却期待和 Codex 一样省
- 你把 Claude 填进 Codex，却期待和 Claude Code 一样稳

先回到默认路径：

```text
GPT → Codex
Claude → Claude Code
```

等你知道自己为什么要跨接，再跨接。

<h2 id="next">下一步</h2>

- 想走 GPT 路径：去 [Runtime / Codex](/docs/runtime/codex)
- 想走 Claude 路径：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 还没有 API Key：去 [Platform / 创建 API Key](/docs/platform/create-api-key)
- 想自己验证请求：去 [Platform / 首条请求](/docs/platform/first-request)
- 想了解长期项目上下文：去 [Agent 基建 / AGENTS.md](/docs/agent-infra/agents-md)
