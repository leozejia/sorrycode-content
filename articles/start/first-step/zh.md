---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 第一次使用 SorryCode，先理解它能帮你把 Codex、Claude Code、Skills 和模型接起来，再按目标选择下一步。
section: start
section_title: 开始使用
section_order: 1
---

# 第一次使用 SorryCode

你来 SorryCode，多半不是为了研究 API，也不是为了看一堆模型名字。

你可能只是想让 AI 帮你做一件具体的事：读懂项目、改文件、生成图片、整理文章、做 PPT，或者把一个想法变成方案。

SorryCode 负责把这些工具接到模型上。你在这里创建一把钥匙，把它交给 `Codex`、`Claude Code` 或某个 `Skill`，工具就能用你的 SorryCode 账号额度调用模型。

这把钥匙叫 `API Key`，通常长这样：`sk-...`。你可以先把它理解成门禁卡：没有它，工具进不了 SorryCode；有了它，工具才能开始干活。

<h2 id="three-words">先理解三个词</h2>

不用一次学完整套概念，先记住这张表：

| 词 | 小白先这样理解 |
| --- | --- |
| `API` | 工具和模型说话的通道 |
| `API Key` | 证明这是你的账号在用的钥匙 |
| `SorryCode` | 创建钥匙，并把工具接到模型上的地方 |

你平时和 AI 聊天，是打开网页，在输入框里打字。

`Codex`、`Claude Code`、`Skills` 这些工具不会像人一样点网页。它们需要用软件之间的方式去请求模型，这种方式就叫 `API`。

新手阶段不用先学会写 API 请求。先创建 API Key，把它交给工具，剩下的让 agent 帮你做。

<h2 id="runtime-skills">工作台和能力包</h2>

你可以把 `Codex`、`Claude Code` 理解成 AI 的工作台。模型负责思考，工作台负责帮你读文件、改文件、运行命令、持续完成任务。

`Skills` 是装进工作台里的能力包。比如图片 Skill、办公文档 Skill、PPT Skill，本质上是在告诉 agent：遇到这类任务时，应该按什么流程做、用哪些工具、产物保存在哪里。

所以新手阶段先做三件事：

```text
创建 API Key → 装一个工作台 → 按任务安装对应 Skill
```

<h2 id="step-1">第 1 步：创建 API Key</h2>

你要做的是：

1. 打开控制台里的 `API 密钥`
2. 创建一个新的 `sk-...`
3. 复制它，先留在手边

如果你找不到入口，直接打开：`https://sorrycode.com/keys`

更详细的说明在 [Platform / 创建 API Key](/docs/platform/create-api-key)。第一次不用先读完那篇，先把 `sk-...` 创建出来就行。

<h2 id="step-2">第 2 步：选择你要用的入口</h2>

不同用户的第一步不一样。先按你的目标选：

| 你想做什么 | 建议先去哪里 |
| --- | --- |
| 让 AI 读项目、改文件、执行命令 | [Runtime / Codex](/docs/runtime/codex) |
| 想用 Claude 路径做项目任务 | [Runtime / Claude Code](/docs/runtime/claude-code) |
| 生成或编辑图片 | 先装 runtime，再看 [Skills / SorryCode Image2](/docs/skills/sorrycode-image2) |
| 处理 Word、Excel、PPT、PDF | 先装 runtime，再看 [Skills / 办公文档](/docs/skills/office-docs) |
| 直接写 HTTP 请求 | [Platform / 首条请求](/docs/platform/first-request) |
| 想要更可视化地看文件和改动 | [工具 / VS Code](/docs/tools/vscode) |

如果你完全不知道选哪个，先选 `Codex`。它是当前 GPT 路径最直接的新手入口。

<h2 id="step-3">第 3 步：选对工具和模型</h2>

`Codex`、`Claude Code` 不是模型，它们是工作台。`GPT`、`Claude` 才是模型。

小白默认按这两条走：

```text
用 GPT 模型，优先走 Codex。
```

```text
用 Claude 模型，优先走 Claude Code。
```

不要为了追一个新模型名，就随手把它塞到另一个工作台里。这样可能能跑，但缓存和 API 消耗不一定划算。

更详细的解释在 [Platform / 工具与模型](/docs/platform/runtime-models)。

<h2 id="step-4">第 4 步：按你的电脑安装</h2>

这篇不复制安装命令。安装命令只放在对应 runtime 页，避免你复制到过期版本。

按你的选择继续：

- 想走 GPT / Codex 路径：去 [Runtime / Codex](/docs/runtime/codex)
- 想走 Claude Code 路径：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 想确认 Windows 终端怎么打开：去 [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)
- 想手动准备 Node.js：去 [环境准备 / Node.js](/docs/environment/nodejs)

<h2 id="step-5">第 5 步：跑通第一个任务</h2>

安装完成后，不要一上来就让 agent 大改东西。先用一个小任务确认它真的能工作。

如果你有代码项目，复制这句：

```text
先别改代码，先看一下这个项目，告诉我它是做什么的，以及我应该先读哪些文件。
```

如果你没有代码项目，可以先在桌面建一个 `AI 工作台` 文件夹，然后复制这句：

```text
请在当前文件夹里帮我整理一份个人介绍草稿。先问我 5 个必要问题，不要直接生成最终稿。
```

如果你想生成图片，先安装 [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)，然后复制这句：

```text
请用 SorryCode Image2 帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。先检查 API Key，如果没设置就告诉我怎么设置。
```

<h2 id="what-next">接下来做什么</h2>

按目标继续：

- 想读懂项目：去 [新手村 / 读懂一个项目](/docs/village/read-project)
- 想改第一个文件：去 [新手村 / 修改第一个文件](/docs/village/edit-first-file)
- 想生成图片：去 [新手村 / 生成第一张图片](/docs/village/first-image)
- 想做产品介绍：去 [新手村 / 做一份产品介绍](/docs/village/product-intro)
- 想处理办公文件：去 [Skills / 办公文档](/docs/skills/office-docs)
- 想了解工具和模型区别：去 [Platform / 工具与模型](/docs/platform/runtime-models)
- 想理解 `AGENTS.md / CLAUDE.md / DESIGN.md / MCP / Skills`：去 [Agent 基建](/docs/agent-infra/overview)

<h2 id="remember">最后只记住这几件事</h2>

- `API` 是通道
- `API Key` 是钥匙
- `Codex / Claude Code` 是工作台
- `Skills` 是能力包
- `SorryCode` 负责把这些工具接到模型上
