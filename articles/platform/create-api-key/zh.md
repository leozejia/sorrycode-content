---
title: 创建 API Key
slug: create-api-key
order: 1
summary: 先理解 API Key 是什么，再在 SorryCode 控制台创建一个 sk-... 给 Codex、Claude Code 或 Skills 使用。
section: platform
section_title: Platform
section_order: 8
---

# 创建 API Key

`API` 可以先理解成“工具和模型说话的通道”。

你平时和 AI 聊天，是打开网页，在输入框里打字。`Codex`、`Claude Code`、`Skills` 这些工具不会像人一样点网页，它们需要用软件之间的方式去请求模型，这种方式就叫 API。

`API Key` 是这条通道上的钥匙，用来证明这是你的 SorryCode 账号在使用模型。它通常长这样：`sk-...`。

无论你后面走 Codex、Claude Code、CC-Switch、图片 Skill，还是手动请求，这一步都绕不开。现在的一键安装也会在流程里要求你输入 API Key，所以最好先在控制台把它准备好。

## 最短路径

1. 打开 `https://sorrycode.com/login` 登录 SorryCode 控制台
2. 在控制台里找到 `API 密钥`
3. 如果还没有，就创建一个新的密钥
4. 复制它并安全保存

你最后拿到的，应该是一个 `sk-...`。

快速入口是：

`https://sorrycode.com/keys`

但不要只记这个地址。更重要的是记住它在控制台里的位置，因为很多小白第一次进去时，根本不知道自己应该点哪里。

## 你真正要记住什么

小白先记住三句话：

- `API` 是通道
- `API Key` 是钥匙
- `SorryCode` 是创建钥匙、管理额度、把工具接到模型上的地方

如果你走的是一键安装，安装器会帮你写入大部分配置，你通常不需要先理解 `Base URL`。

只有手动配置时，才需要继续看下面两个值：

- API Key：你刚创建出来的 `sk-...`
- 你要接的工作台走哪种 Base URL

如果你走的是 `Codex` 这类 OpenAI-compatible 路径，用的是：

- `{{API_BASE_URL}}`

如果你走的是 `Claude Code` 这类 Anthropic-compatible 路径，用的是：

- `{{ANTHROPIC_BASE_URL}}`

有些 runtime 的字段名看起来不像 API Key，不要被名字带偏。

比如在 `Claude Code` 里，字段名叫 `ANTHROPIC_AUTH_TOKEN`，但里面填的仍然是同一个 `sk-...`。

## 安全要求

- 不要提交到代码仓库
- 不要发到公共群
- 不要直接写进长期可见的 shell history
- 泄露后立即废弃重建

## 下一步

- 想直接开始用 Codex：去 [Runtime / Codex](/docs/runtime/codex)
- 想直接开始用 Claude Code：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 不清楚工具和模型关系：去 [Platform / 工具与模型](/docs/platform/runtime-models)
- 想先做最小验证：去 [Platform / 首条请求](/docs/platform/first-request)
- 想少碰终端：去 [工具 / CC-Switch](/docs/tools/cc-switch)
