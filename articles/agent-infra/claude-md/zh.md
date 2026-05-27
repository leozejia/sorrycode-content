---
title: CLAUDE.md
slug: claude-md
order: 4
summary: Claude Code 读取的 memory / instruction 文件。用它保存项目长期事实，不要把临时会话状态写成永久记忆。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# CLAUDE.md

`CLAUDE.md` 是 Claude Code 读取的 memory / instruction 文件。

它的作用很简单：让 Claude Code 进入项目时，不用每次从零理解你是谁、项目是什么、怎么测试、哪些坑不能踩。

但它也很容易被写坏。

`CLAUDE.md` 不是临时任务清单，也不是旧会话垃圾桶。它应该保存项目长期事实和稳定协作规则。

如果你正在处理长会话、缓存和 handoff，先看 [长期上下文怎么管理](/docs/agent-infra/context-management)。这页只讲 `CLAUDE.md` 本身怎么维护。

<h2 id="who-reads-it">谁会读取它</h2>

Claude Code 会读取适用范围内的 memory。

常见位置包括：

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
your-project/apps/web/CLAUDE.md
```

具体加载规则以 Claude Code 官方文档为准。新手可以先在项目根目录维护一份 `CLAUDE.md`。

<h2 id="where">放在哪里</h2>

项目规则优先放项目里：

```text
your-project/
  CLAUDE.md
  README.md
```

个人长期偏好可以放用户级 memory。项目事实不要只放在个人 memory 里，否则换人、换机器、换环境后很容易丢。

<h2 id="what-to-write">应该写什么</h2>

适合写：

- 项目是什么
- 常用开发、测试、构建命令
- 代码风格和目录约定
- 常见坑和不要做的事
- 重要业务规则
- 团队协作偏好
- 交付前必须检查什么

写法要能执行。不要写“认真一点”。要写“修改支付流程后，必须检查 tests/payments 目录里的回归测试”。

<h2 id="when-update">什么时候该改它</h2>

这些情况应该更新 `CLAUDE.md`：

- 项目结构变化
- 常用命令变化
- Claude Code 反复误解同一个项目事实
- handoff 里出现了应该长期保留的规则
- 团队协作方式变了

不要因为一次临时任务就改长期 memory。任务结束后就不会再用的信息，留在会话或 handoff 里就够了。

<h2 id="handoff">从 handoff 里沉淀什么</h2>

handoff 是交接，`CLAUDE.md` 是长期记忆。

适合从 handoff 沉淀到 `CLAUDE.md`：

```text
项目真源文件在哪里
哪些旧方案已经废弃
哪个命令才是当前有效命令
哪些目录需要小心
完成任务前必须检查什么
```

不适合沉淀：

```text
这次会话的完整过程
报错日志原文
临时猜测
短期 TODO
已经不再采用的方案细节
```

<h2 id="avoid">不应该写什么</h2>

不要写：

- API Key、token、密码
- 一次性任务和临时 TODO
- 已经过期的命令
- 大段会议纪要
- 大段错误日志
- 和 agent 工作无关的信息

如果一句话会让未来的 Claude Code 带着错误旧背景继续工作，就不要写。

<h2 id="template">最小模板</h2>

```md
# CLAUDE.md

## Project Context

This project is ...

## Common Commands

- Test:
- Build:

## Source of Truth

- ...

## Working Rules

- ...

## Avoid

- ...
```

<h2 id="first-prompt">第一次怎么用</h2>

可以这样开始：

```text
请先读取 CLAUDE.md。

先不要改文件。请告诉我：
- 这个项目是什么
- 常用命令是什么
- 哪些规则必须遵守
- 哪些旧方向不要再用
```

如果它理解错了，先纠正，再继续。

<h2 id="agents">和 AGENTS.md 的关系</h2>

如果你同时使用 Codex 和 Claude Code，可以同时维护 [AGENTS.md](/docs/agent-infra/agents-md) 和 `CLAUDE.md`。

原则是：事实一致，表达可以按 runtime 调整。

Claude Code 官方文档支持在 memory 中导入其他文件。也就是说，你可以让 `CLAUDE.md` 引用已有的 `AGENTS.md`，减少重复维护。具体写法以 Claude Code 官方文档为准。

<h2 id="reference">参考</h2>

- Claude Code / Memory：<https://docs.anthropic.com/en/docs/claude-code/memory>
