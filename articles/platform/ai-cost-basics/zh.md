---
title: AI 成本怎么计算
slug: ai-cost-basics
order: 2
summary: 不要按回复字数判断成本。先理解 input、output、cache，再看网页、API 和 agent runtime 怎么触发消耗。
section: platform
section_title: Platform
section_order: 8
---

# AI 成本怎么计算

很多人第一次看 AI 用量，都会有同一个疑问：

```text
AI 明明没写几个字，为什么消耗这么多？
```

原因是：AI 成本不是按你肉眼看到的字数算的。

底层模型消耗通常要看三类：

```text
input：模型读了多少
output：模型生成了多少
cache：模型复用了多少，或者为了复用写入了多少
```

你最后看到的付款方式可能是余额、订阅、额度或账单，但模型资源消耗大致都会落回这三类。

## token 不是字数

模型不是按“汉字个数”或“单词个数”直接处理文本。

它处理的是 `token`。

你可以先把 token 理解成模型内部处理文字的小片段。英文里常见的粗略估算是：一个 token 大约等于 4 个字符，或者 0.75 个单词。

但这只是经验值。

中文、代码、标点、空格、路径、JSON、Markdown 表格，都会让 token 变得不直观。

所以不要用肉眼判断：

```text
它才回了 200 个字，怎么会贵？
```

你看到的是输出，但模型可能还读了很多输入。

## 1. input：模型读了多少

input 是模型读进去的内容。

它不只是你刚发的那句话。

还可能包括：

- 系统提示词
- 历史对话
- 文件内容
- 工具返回
- 报错日志
- 项目规则
- 你上传的文档或图片说明

所以 AI 只回了两句话，不代表它只处理了两句话。

它可能为了回这两句话，先读了一大堆上下文。

## 2. output：模型生成了多少

output 是模型生成出来的内容。

回复一段话、生成一段代码、写一份总结，都是 output。

很多模型的 output 单价会比 input 贵。

但 output 也不一定等于你肉眼看到的最终文字。

推理模型可能会产生内部 reasoning / thinking tokens。这些内部推理不一定完整显示在最终回复里，但通常会落在 output 侧计费。

所以“它没写几个字”有时是错觉。

它可能没有写很多给你看，但在内部想了很久。

## 3. cache：模型复用了什么

cache 是为了处理重复上下文。

如果一段稳定内容后面会反复用，系统可能把它缓存起来。

命中缓存时，cached input / cache read 通常比普通 input 便宜。

但便宜不是免费。

而且有些模型供应商会区分：

- cache read：读取已经缓存的内容
- cache write：第一次把内容写入缓存

第一次写入缓存，也可能要花钱。

所以不要听到“缓存命中”就自动理解成免费。

cache 解决的是重复输入的成本，不是让模型免费工作。

## 网页聊天怎么触发消耗

你以为自己只发了一句话。

但网页产品可能还带着：

- 历史对话
- 系统规则
- 文件和图片
- 搜索结果
- 工具返回

这些主要变成 input。

模型回你的内容，变成 output。

稳定上下文如果被产品缓存，可能走 cache。

## API 调用怎么触发消耗

API 最容易理解。

你传进去的 `prompt / messages / tools / files` 是 input。

模型返回的 `response` 是 output。

重复前缀、系统提示词、长上下文，可能命中 cache。

如果你自己写 API 请求，这是最应该先看懂的三类。

## Agent runtime 怎么触发消耗

`Codex`、`Claude Code` 这类 agent runtime 最容易让人误判成本。

因为 agent 不是一问一答。

它会读文件、跑命令、看报错、调用工具、多轮规划，再把结果塞回上下文。

这些会不断触发 input。

每次让模型分析、决策、总结、改写，都会触发 output。

如果 runtime 把稳定上下文组织得好，可能命中 cache。

如果组织得不好，就会反复读、反复写、反复消耗。

## 看用量时先问三句话

不要先问：

```text
它写了多少字？
```

先问：

```text
它读了多少 input？
```

```text
它生成了多少 output？
```

```text
它有没有命中 cache？
```

这三件事看完，再判断贵不贵。

## 和 SorryCode 有什么关系

SorryCode 给你的是统一入口和余额。

你可以用一份余额接 Codex、Claude Code、Skills、图片接口和其他工具。

但不管你从哪个入口调用模型，底层消耗都离不开 input、output、cache。

理解这三类，才能知道为什么同样是“问 AI 一句话”，网页、API 和 agent runtime 的消耗可能完全不同。

## 下一步

- 不知道自己适不适合用 SorryCode：看 [Platform / SorryCode 适合谁](/docs/platform/who-is-sorrycode-for)
- 不知道工具和模型怎么分：看 [Platform / 工具不是模型](/docs/platform/tools-and-models)
- 想直接开始：看 [Platform / 创建 API Key](/docs/platform/create-api-key)
- 想走 GPT 路径：看 [Runtime / Codex](/docs/runtime/codex)
- 想走 Claude 路径：看 [Runtime / Claude Code](/docs/runtime/claude-code)
