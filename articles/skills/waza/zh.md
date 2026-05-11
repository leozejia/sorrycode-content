---
title: Waza
slug: waza
order: 1
summary: 一整套工程习惯包。让你在做功能、查 bug、写界面、读资料、改文案、提交前检查时，都有更稳的协作路径。
section: skills
section_title: Skills
section_order: 15
group_order: 30
group_title: 工作流
group: workflow
source_url: https://github.com/tw93/Waza
---

# Waza

`Waza` 不是某一个工具，而是一整套工程习惯包。

如果 `Kami` 帮你把材料做成成品，`SorryCode Image2` 帮你生成图片，`Waza` 解决的是更底层的问题：你怎么和 agent 一起把事情做稳。

<h2 id="what-is-waza">Waza 是什么</h2>

用了 AI 之后，很多人会更快，但不一定更稳。

常见问题是：

- 想做功能，但一开始没想清楚边界
- 出 bug 后让 AI 直接乱改，结果越改越乱
- 做 UI 时没有明确审美方向，最后像默认模板
- 看资料时只是在复制摘要，没有形成自己的理解
- 改完代码后没有自检，问题留到上线前才暴露

`Waza` 把这些工程动作整理成一组可以反复调用的 skills。它帮你在关键节点停一下，按更靠谱的流程推进。

<h2 id="why-recommend">为什么推荐整包安装</h2>

我们推荐 `Waza`，不是因为它“很多”，而是因为这一整包刚好覆盖了 AI 协作里最容易掉坑的环节。

它让你逐渐形成几种习惯：

- 开始前先想清楚，不急着动手
- debug 先找根因，不靠猜
- UI 先定方向，不做默认 AI 风
- 读资料要变成输出，不只是收藏链接
- 写完之后要检查，不把 review 全交给别人

对新手来说，这比“多知道一个模型参数”更重要。模型会变，但这些习惯会一直有用。

<h2 id="what-changes">装了之后会改变什么</h2>

你不需要记住每个 skill 的细节。先记住这些场景就够：

- 做新功能前，让 Waza 帮你想清楚方案
- 遇到 bug 时，让 Waza 先带你查根因
- 做页面时，让 Waza 帮你建立设计方向
- 读长资料时，让 Waza 帮你整理成可输出的理解
- 任务完成后，让 Waza 帮你做一轮检查

它的价值不是替你多写几行代码，而是让你少走弯路。

<h2 id="install">安装</h2>

先确认你已经装好了 `Codex` 或 `Claude Code`。

### Codex

```bash
npx skills add tw93/Waza -a codex -g -y
```

### Claude Code

```bash
npx skills add tw93/Waza -a claude-code -g -y
```

如果你还没装好 runtime，先回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="common-scenes">最常用的 5 个场景</h2>

### 做功能前

```text
用 Waza 的 think 方式帮我先过一遍这个功能方案。先不要写代码，先找边界、风险和最小实现路径。
```

### 查 bug

```text
用 Waza 的 hunt 方式帮我定位这个问题。先找根因，不要急着改代码。
```

### 做界面

```text
用 Waza 的 design 方式帮我设计这个页面。请先给一个明确的视觉方向，再进入实现。
```

### 读资料

```text
用 Waza 的 read / learn 方式帮我读这篇资料，整理出重点、脉络和我可以直接用的结论。
```

### 提交前检查

```text
用 Waza 的 check 方式帮我检查这次改动，重点看有没有跑偏、遗漏、风险和需要补验证的地方。
```

<h2 id="first-prompt">第一句可以说什么</h2>

如果你不知道从哪里开始，可以直接说：

```text
我想用 Waza 帮我把这个任务推进得更稳。请先判断现在应该用 think、hunt、design、read、learn、write 还是 check，然后告诉我下一步怎么做。
```

<h2 id="relationship">和其他 Skills 的关系</h2>

- `Kami`：把内容做成成品文档、简历、作品集、PPT
- `SorryCode Image2`：生成图片、封面、海报、插图
- `Waza`：帮你建立工程协作流程，让任务推进更稳

它们不是互相替代的关系。更自然的组合是：先用 `Waza` 想清楚，再用 `Kami` 或 `SorryCode Image2` 做成品。

<h2 id="common-issues">常见问题</h2>

- 我是不是要记住所有 skill 名字
  不用。先记住“做前先想、出错先查、完成后检查”这三件事。
- Waza 是不是只适合工程师
  它最适合工程任务，但读资料、写作、改文案也能用。
- 我已经有 Kami，还需要 Waza 吗
  需要。`Kami` 解决成品呈现，`Waza` 解决过程质量。
- 为什么直接用上游安装
  Waza 是社区持续维护的一整包 skills，直接从上游安装更清晰，也能跟上作者更新。
