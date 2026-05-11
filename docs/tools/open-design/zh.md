---
title: Open Design
slug: open-design
order: 4
summary: 一个开源设计工作台。把本地 agent CLI、Skills、DESIGN.md 设计系统和 artifact preview 组织成完整设计生产链路。
section: tools
section_title: 工具
section_order: 28
source_url: https://github.com/nexu-io/open-design
---

# Open Design

`Open Design` 是一个开源设计工作台。

它不是单个 skill，也不是 SorryCode 的默认新手入口。它更像一个完整设计环境：把本地 agent CLI、skills、`DESIGN.md` 设计系统、项目文件和 artifact preview 组织到一起。

如果你已经熟悉 `Codex / Claude Code + Skills`，想研究 AI 设计生产链路，`Open Design` 很值得看。

<h2 id="what-is-it">它是什么</h2>

Open Design 的核心思路是：

```text
agent runtime + SKILL.md + DESIGN.md + artifact preview = 设计工作台
```

它会检测本地已安装的 agent CLI，例如 Codex、Claude Code、Gemini CLI、OpenCode 等，然后让这些 agent 在一个设计任务环境里生成网页、原型、deck、海报、动效等 artifact。

它还内置 design systems 和 skills，能够把“选一个设计系统 + 选一个任务 skill + 输入一句需求”组合成一次设计生成。

<h2 id="why-recommend">为什么推荐</h2>

我们推荐它，不是因为它适合所有小白第一天安装，而是因为它展示了 AI 设计工作台的完整方向：

- 用 `DESIGN.md` 管设计上下文
- 用 `SKILL.md` 管任务工作流
- 用本地 agent CLI 执行真实文件操作
- 用预览窗口查看 artifact
- 用项目目录保存结果，方便继续修改

这对理解 `创作与设计` 很有价值。

<h2 id="requirements">使用前提</h2>

Open Design 当前更适合愿意折腾本地环境的人。

上游 Quickstart 写明：

- Node.js：`~24`
- pnpm：`10.33.x`
- macOS、Linux、WSL2 是主要路径
- 可选本地 agent CLI：Codex、Claude Code、Gemini CLI 等

这和 SorryCode 当前一键安装默认的 Node 22 LTS 路径不同，所以我们不把它作为小白默认第一步。

<h2 id="how-to-start">怎么开始</h2>

如果你要自己研究，按上游说明来：

```bash
corepack enable
pnpm install
pnpm tools-dev run web
```

打开终端输出的本地地址后，选择 skill、design system 和 agent，再输入设计需求。

具体命令以官方仓库为准：<https://github.com/nexu-io/open-design>

<h2 id="relationship">和 SorryCode 的关系</h2>

- `SorryCode`：帮你创建 API Key，把 runtime 和模型链路跑起来。
- `Skills / 创作与设计`：推荐可以直接安装使用的设计类 skills。
- `Agent 基建 / DESIGN.md`：解释设计上下文文件。
- `Open Design`：展示这些概念如何组合成一个完整设计工作台。

如果你只是想先生成图片、做一页纸或做 PPT，优先看 [Skills / 创作与设计](/docs/skills/creation-design)。
