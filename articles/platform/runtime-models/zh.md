---
title: 工具与模型
slug: runtime-models
order: 2
summary: 分清 Codex、Claude Code、协议和模型，避免把模型接到不合适的工具里，造成缓存差和 API 量浪费。
section: platform
section_title: Platform
section_order: 8
---

# 工具与模型

很多新手会把 `Codex`、`Claude Code`、`gpt-5.4`、`claude-sonnet-4-5` 混在一起。

先记住一句话：

```text
工具不是模型。工具只是开车的人，模型才是发动机。
```

`Codex` 和 `Claude Code` 都是 agent runtime。它们负责读项目、发请求、改文件、执行命令。真正消耗 API 量的是它们背后调用的模型。

<h2 id="five-pieces">先把五件事分开</h2>

| 名字 | 它负责什么 | 小白先这样理解 |
| --- | --- | --- |
| `模型` | 思考、生成文字或图片 | 发动机，例如 GPT、Claude |
| `Agent Runtime` | 读文件、改文件、运行命令、管理上下文 | AI 工作台，例如 Codex、Claude Code |
| `Skills` | 告诉 agent 某类任务该怎么做 | 装进工作台的能力包 |
| `MCP` | 让 agent 连接外部工具和数据 | 进阶连接方式，新手不用先学 |
| `SorryCode` | 提供 API Key、额度和模型访问入口 | 把工作台接到模型上的地方 |

第一天不需要先学 `MCP` 或协议细节。真正会影响成本和体验的是：你打开的是哪个工作台，背后接的是哪个模型。

<h2 id="simple-map">最简单的对应关系</h2>

默认先按这张表理解：

| 你打开的工具 | 默认协议心智 | 推荐模型心智 | 不建议新手这样做 |
| --- | --- | --- | --- |
| `Codex` | OpenAI-compatible | `gpt-5.4` 这类 GPT 模型 | 在 Codex 里硬接 Claude 模型 |
| `Claude Code` | Anthropic-compatible | `claude-sonnet-4-5` 这类 Claude 模型 | 在 Claude Code 里硬接 GPT 模型 |
| `OpenClaw` | Custom / OpenAI-compatible | 进阶自定义接入 | 小白把它当 Codex 替代品跑 GPT |
| `Hermes Agent` | Custom endpoint | 进阶自定义接入 | 小白把它当 Codex 替代品跑 GPT |

这不是说技术上永远不能跨接，而是说：小白默认不要跨接。当前最大价值的默认组合是 `Codex + GPT`、`Claude Code + Claude`。`OpenClaw / Hermes Agent` 可以作为进阶自定义接入，但不要默认认为它们跑 GPT 的缓存和成本表现一定等同于 Codex。

<h2 id="why-it-costs-more">为什么接错会更贵</h2>

Agent runtime 不只是把你的问题原样发给模型。

它还会做很多事情：

- 组织项目上下文
- 维护对话状态
- 调用工具
- 压缩历史
- 处理缓存
- 按自己的协议格式拼请求

如果你用 `Claude Code / OpenClaw / Hermes Agent` 去跑 `gpt-5.4`，或者用 `Codex` 去跑 Claude 模型，就可能出现这些问题：

- runtime 的请求格式和模型最擅长的格式不匹配
- 上下文缓存命中率变低
- 同样任务需要发送更多 token
- 对话历史更容易重复计费
- 看起来“能用”，但实际 API 消耗不划算

所以它不是“能不能跑”的问题，而是“值不值得这样跑”的问题。

<h2 id="beginner-rule">小白默认规则</h2>

如果你不确定，就按这两条：

```text
用 GPT 模型，优先走 Codex。
```

```text
用 Claude 模型，优先走 Claude Code。
```

不要为了追一个新模型名，就随手把它塞到另一个 runtime 里。

如果你看到别人说“Claude Code 也能跑 GPT”，先把它当成进阶玩法，不要当成默认省钱方案。

<h2 id="what-sorrycode-installs">SorryCode 一键安装做了什么</h2>

SorryCode 的一键安装不是只帮你装工具，也会帮你写入一组默认匹配关系：

- `Runtime / Codex`
  - 写入 OpenAI-compatible Base URL
  - 默认使用 GPT 模型
  - 这是 GPT 路径的默认主入口
- `Runtime / Claude Code`
  - 写入 Anthropic-compatible Base URL
  - 默认使用 Claude 模型
  - 这是 Claude 路径的默认主入口
- `OpenClaw / Hermes Agent`
  - 属于进阶自定义接入
  - 可以验证网关兼容性，但不作为小白省钱默认路径

这就是为什么我们建议小白先用一键安装，而不是一开始手动改配置。

<h2 id="when-change-model">什么时候可以改模型</h2>

可以改，但先满足这几个条件：

- 你知道当前打开的是哪个 runtime
- 你知道它走 OpenAI-compatible 还是 Anthropic-compatible
- 你知道目标模型是否适合这个 runtime
- 你能接受缓存命中、上下文组织、计费表现可能变化
- 你愿意观察用量，而不是只看是否能返回内容

如果只是想用最新 GPT 模型，优先在 `Codex` 里改，例如：

```bash
codex -m gpt-5.5
```

如果只是想用 Claude 模型，优先在 `Claude Code` 里按 Claude Code 的方式配置。

<h2 id="cost-check">怎么判断是不是不划算</h2>

出现这些信号时，先停下来检查工具和模型是否匹配：

- 同一个项目反复问几句，用量涨得很快
- 明明没有让它大改代码，却消耗很多 API 量
- 每次对话都像重新读项目，缓存没有明显效果
- 你在 `Claude Code / OpenClaw / Hermes Agent` 里填的是 GPT 模型名，却期待和 Codex 一样的成本表现
- 你在 `Codex` 里填的是 Claude 模型名

这时先回到默认路径：

- GPT 模型：用 [Runtime / Codex](/docs/runtime/codex)
- Claude 模型：用 [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="next">下一步</h2>

- 要跑 GPT / Codex 路径：去 [Runtime / Codex](/docs/runtime/codex)
- 要跑 Claude Code 路径：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 要手动验证协议：去 [Platform / 首条请求](/docs/platform/first-request)
