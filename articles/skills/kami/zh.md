---
title: Kami
slug: kami
order: 3
summary: 一个面向成品文档的设计型 skill。适合做一页纸、长文、简历、作品集，也适合直接做演讲幻灯片。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/tw93/kami
---

# Kami

如果你不想再看到“像普通 markdown 一样平”的结果，而是想直接拿到更像成品的文档、简历、作品集或幻灯片，`Kami` 是当前最值得先装的一个 skill。

它特别适合第一次接触这类能力的人，因为它不要求你先学设计，也不要求你先学排版术语。你只要把目标说清楚，它就会按一套稳定的纸面设计语言来出结果。

<h2 id="what-is-kami">Kami 是什么</h2>

- `Kami` 是一个面向成品文档的设计型 skill
- 它覆盖一页纸、长文、正式信件、作品集、简历和演讲幻灯片
- 它同时支持中文、英文，也提供日文 best-effort 路径
- 它还能在文档里直接嵌入柱状图、折线图、环形图、时间线、树图、瀑布图等 SVG 图表

更重要的是，它不是“随便排版一下”。它背后有一套统一的视觉约束，所以连续生成多份材料时，风格会比较稳定。

参考：[Kami 官方仓库](https://github.com/tw93/kami)

<h2 id="what-is-good-for">它适合做什么</h2>

你可以优先把它用在这些场景：

- 把你的产品介绍整理成一页纸
- 把研究笔记或长文章整理成正式文档
- 做一份更像成品的个人简历
- 做一份项目作品集
- 按提纲快速生成一套演讲幻灯片
- 做 changelog、equity report 这类更结构化的专业文档

如果你现在想做 PPT，也先走这页就够了。当前这条能力先直接复用 `Kami` 的幻灯片能力，不额外拆第二个 skill。

<h2 id="one-click-install">一键安装</h2>

这是我们验证过的上游安装命令。

当前我们先验证这两条主路径：

### Codex

```bash
npx skills add tw93/kami -a codex -g -y
```

### Claude Code

```bash
npx skills add tw93/kami -a claude-code -g -y
```

如果你还没装好 runtime，请先回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

如果不想继续使用，先运行 `npx skills list --global` 确认名称，再用 `npx skills remove --global kami` 卸载。

安装完成后，不需要记 slash 命令。`Kami` 会在你描述需求时自动触发。

<h2 id="how-to-use">安装后怎么触发</h2>

触发方式尽量按自然语言来写，不要先想着“我要调哪个参数”。

最好的方式是直接说：

- 你要做什么成品
- 面向谁
- 用什么语言
- 有没有固定结构
- 如果是幻灯片，有没有页数或提纲

如果你需要图表，也直接把数据和图表类型说进去。

<h2 id="first-prompts">第一句可以说什么</h2>

如果你想先试文档：

```text
帮我把这段产品介绍整理成一页纸，面向第一次了解我们的客户，中文，风格克制一点。
```

如果你想先试 PPT：

```text
帮我根据下面这份提纲做一套 6 页的中文演讲幻灯片，适合现场分享，语气专业但不要太硬。
```

如果你想先试图表：

```text
帮我整理成一份长文档，并加一个营收结构环形图和一个用户增长折线图。
```

<h2 id="common-issues">常见问题</h2>

- 提示 `npx` 或 `node` 找不到
  先去看 [环境准备 / Node.js](/docs/environment/nodejs)
- 提示 `npm` 找不到
  先去看 [环境准备 / Node.js](/docs/environment/nodejs)
- 我已经装了，但不知道怎么调用
  直接用自然语言描述目标，`Kami` 会自动触发
- 我想做 PPT，是不是还要装第二个 skill
  当前不用，先直接用 `Kami`
- 我用的是 OpenClaw / Hermes Agent
  `Kami` 官方也提供 generic agents 路径，但站内当前先只验证 `Codex / Claude Code`

<h2 id="references">参考</h2>

- 官方仓库：<https://github.com/tw93/kami>
- 官方说明里明确支持：
  - 一页纸
  - 长文
  - 正式信件
  - 作品集
  - 简历
  - 幻灯片
  - changelog
  - equity report
  - 多种 SVG 图表
