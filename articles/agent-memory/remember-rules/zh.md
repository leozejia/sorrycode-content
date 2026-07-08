---
title: 让 AI 记住项目规则
slug: remember-rules
order: 3
summary: 写一份 AGENTS.md 或 CLAUDE.md，让 AI 记住哪些文件不能改、用什么命令、遵守什么规则。
section: agent-memory
section_title: 让 AI 记住你的要求
section_order: 15
---

# 让 AI 记住项目规则

你已经跑通了几个任务。现在每次开新会话都要重新解释项目背景——目录在哪、用什么命令、哪些文件不能碰。这不是 Agent 笨，是你没有把规则写下来。

解决方案很简单：在项目根目录放一个规则文件。Codex 读 `AGENTS.md`，Claude Code 读 `CLAUDE.md`。**两份文件的写法和维护规则完全一样**——只是文件名不同。

如果你正在处理长会话、缓存和 handoff，先看[会话太长怎么办](/docs/agent-memory/context-management)。这页只讲规则文件本身怎么维护。

<h2 id="where">放在哪里</h2>

项目根目录：

```text
your-project/
  AGENTS.md    # 给 Codex
  # 或
  CLAUDE.md    # 给 Claude Code
```

如果同时用两个工具，可以两份都放。原则是：**两份文件写同一套事实，不要互相矛盾。** Claude Code 也支持在 `CLAUDE.md` 里引用 `AGENTS.md`，减少重复维护。具体写法以 Claude Code 官方文档为准，新手先保证两边事实一致就够了。

<h2 id="what-to-write">应该写什么</h2>

- 项目是做什么的
- 目录结构
- 开发、测试、构建命令
- 代码风格和命名约定
- 不要改哪些文件
- 提交前必须跑哪些检查
- 这个项目里经常踩的坑

写法要具体。不写"代码要优雅"，写"改 API schema 后必须同步更新 generated types，并运行 pnpm test:types"。

<h2 id="avoid">不应该写什么</h2>

- API Key、密码、token
- 一次性任务
- 临时 TODO
- 大段错误日志
- 已经过期的路径或命令
- 不能验证的抽象要求

一句话如果不能帮助下一次 Agent 工作更稳定，就不要放进去。

<h2 id="when-update">什么时候更新</h2>

不是写完就不动。这些时候应该更新：

- 项目结构或常用命令变了
- Agent 反复误解同一个项目事实
- 团队决定了新的规则
- handoff 里出现了应该长期保留的事实

但不要把 handoff 原文整段搬进去。只沉淀稳定规则，不沉淀临时状态。

<h2 id="handoff">从 handoff 里沉淀什么</h2>

handoff 是交接记录，规则文件是长期记忆。

适合沉淀：

```text
真源文件在哪里
常用命令是什么
哪些目录不要碰
哪个旧方案已经明确废弃
完成前必须跑什么检查
```

不要沉淀：

```text
今天做到第几步
报错日志原文
临时讨论过但没有采用的想法
Agent 的长篇自我总结
```

<h2 id="template">最小模板</h2>

```md
# AGENTS.md  (或 CLAUDE.md)

## Project

This project is ...

## Commands

- Install:
- Test:
- Build:

## Source of Truth

- ...

## Working Rules

- ...

## Do Not

- Do not ...
```

<h2 id="first-prompt">第一次怎么用</h2>

把文件放好后，这样开场：

```text
请先读取 AGENTS.md（或 CLAUDE.md）。

先不要改文件。请告诉我：
- 这个项目是什么
- 常用命令是什么
- 哪些文件或目录不能乱改
- 完成任务前要跑哪些检查
```

确认它理解对了，再让它开始做任务。

<h2 id="codex">Codex 用户</h2>

Codex 读取 `AGENTS.md`。常见位置：

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

越靠近当前工作目录，约束越具体。子目录的 `AGENTS.md` 适合写子项目自己的规则。Codex 还支持替代文件名和 override 机制——第一天不需要学这些，先把根目录一份维护好。

<h2 id="claude">Claude Code 用户</h2>

Claude Code 读取 `CLAUDE.md`。常见位置：

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
```

项目规则优先放项目里。个人长期偏好可以放用户级 memory（`~/.claude/CLAUDE.md`），但项目事实不要只放在个人 memory——换人、换机器后就丢了。

<h2 id="reference">参考</h2>

- OpenAI Codex / AGENTS.md：<https://developers.openai.com/codex/guides/agents-md>
- Claude Code / Memory：<https://docs.anthropic.com/en/docs/claude-code/memory>
