---
title: 工具、模型、平台，别再分不清
slug: tools-models-platform
order: 7
summary: GPT、Claude、Codex、Claude Code、Cursor、DeepSeek、豆包、Kimi——这些名字分三层：模型是大脑，工作台是身体，平台是后勤。别追模型名字，先想清楚你在哪里产出工作，就选那里的 Agent。
section: concepts
section_title: 核心概念
section_order: 5
---

# 工具、模型、平台，别再分不清

你可能已经被这些名字搞晕了：

```text
GPT、Claude、DeepSeek、Qwen、豆包、Kimi、Gemini
Codex、Claude Code、Cursor、Copilot
SorryCode、OpenAI、Anthropic、硅基流动
```

这些名字放在一起，看起来像同一类东西。

它们不是。

<h2 id="three-layers">三层架构</h2>

把这些名字分成三层，立刻清楚：

```text
底层：模型（大脑）
  GPT、Claude、DeepSeek、Qwen、豆包、Kimi、Gemini
  负责：理解、推理、生成内容

中层：工作台 / Runtime（身体）
  Codex、Claude Code、Cursor、Copilot
  负责：读文件、执行命令、组织上下文、调用工具

顶层：平台（后勤）
  SorryCode、OpenAI 官网、Anthropic 官网、硅基流动
  负责：API 接入、计费、Key 管理
```

用买车来理解：

```text
模型 = 引擎（大众/丰田/本田造的）
工作台 = 车身（不同车厂用同一款引擎造不同的车）
平台 = 加油站（你从哪加油、怎么付钱）
```

引擎好不代表车好开。车身好不代表省油。加油站方便不代表车跑得快。

三层各管各的。

<h2 id="why-layers-matter">为什么必须分清这三层</h2>

因为普通人最容易犯的错误是：**追着模型名字跑。**

"GPT-5 出了！我要用 GPT-5！"
"Claude Opus 评分最高！我要换 Claude！"
"DeepSeek 便宜！全切 DeepSeek！"

追模型名字就像追引擎型号。引擎好是重要，但如果你把它塞在一辆不适合你的车身上，好引擎也白搭。

```text
同一个模型，挂在不同工作台上，表现可以完全不同。
```

为什么？因为工作台决定了：
- 模型能看到什么上下文
- 模型能调用什么工具
- 上下文怎么组织、缓存怎么管理
- 会话怎么保持、历史怎么压缩

这些"工作台做的事"对最终体验的影响，很多时候比"模型本身"更大。

```text
选工作台，比选模型更重要。
```

<h2 id="how-to-choose">怎么选：先选工作台，再选模型</h2>

默认规则很简单：

```text
你主要用 GPT 系列 → 工作台选 Codex
你主要用 Claude 系列 → 工作台选 Claude Code
你主要用国产模型 → 看对应厂商有没有推出自己的 Agent 客户端
```

为什么这样配？因为每个工作台在设计和优化时，首要适配的是"自家"模型。上下文组织方式、缓存策略、提示词格式，都是围绕自家模型调过的。

混搭能跑，但不一定划算。

```text
Codex + Claude 能跑。
但上下文复用、缓存命中、消耗控制——这些可能不如原生组合。
新手先走默认路径，熟了再玩混搭。
```

<h2 id="convergence">所有人都在做 Agent</h2>

你可能注意到了：模型厂商都在推自己的 Agent。

OpenAI 有 Codex。Anthropic 有 Claude Code。Google 有 Gemini 的各种集成。国内的 DeepSeek、Qwen、豆包、Kimi——每个都在做自己的 Agent 方案。

这不是巧合。

```text
模型厂商比任何人都清楚：
只会聊天的 AI 是 Demo。
能干活、能操作电脑的 AI 才是产品。
```

对普通用户来说，这意味着什么？

意味着你不用追。不管你选哪家模型，它大概率已经有了或即将有对应的 Agent 工作台。你需要的不是"选最厉害的模型"，而是"选一个工作台，把一件事跑通。"

<h2 id="dont-chase">不要做的事</h2>

三件事，新手最容易踩坑：

**1. 不要追模型排行榜**

今天这个评分高，明天那个评分高。评分是实验室数据，跟你的实际任务不一定相关。一个在数学推理上多 2 分的模型，帮你写会议纪要不会更好。

**2. 不要同时试太多工具**

装完 Codex 又装 Cursor，装完又换 Claude Code，三天换了四个工具——每个都没跑通一个完整任务。

先选一个，先把一个任务从头跑到尾。跑通了再考虑要不要换。

**3. 不要看了两篇文章就混搭**

网上有教程教你怎么把 GPT 挂到 Claude Code 上，怎么把 DeepSeek 挂到 Cursor 上。能跑，但对新手来说——先把默认路径走通，再玩进阶配置。

<h2 id="map">一张地图</h2>

| 你现在的状态 | 建议 |
| --- | --- |
| 我什么都不知道 | 先看 [AI 到底是什么](/docs/concepts/what-is-ai) |
| 我想试试，不知道装什么 | 装 Codex，它是当前最简单的新手入口 |
| 我主要用 GPT | [Runtime / Codex](/docs/runtime/codex) |
| 我主要用 Claude | [Runtime / Claude Code](/docs/runtime/claude-code) |
| 我用国产模型 | 看对应厂商的 Agent 客户端，安装逻辑类似 |
| 我想一次接入多个模型 | 用 SorryCode 做统一 API 入口，按需切换 |
| 我已经在用了，想管得更好 | [Agent 进阶](/docs/agent-memory/overview) |

<h2 id="remember">记住一件事</h2>

```text
模型是大脑，工作台是身体，平台是后勤。
别追模型名字。
先选工作台——你工作在哪里产出，AI 就在哪里叠 buff。
```

<h2 id="next">下一步</h2>

概念都讲完了。最后一章：到底从哪里开始？

[从哪开始](/docs/concepts/where-to-start)
