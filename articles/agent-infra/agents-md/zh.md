---
title: AGENTS.md
slug: agents-md
order: 3
summary: Codex 读取的项目指令文件。用它保存稳定规则，不要把聊天记录、临时任务和废弃结论塞进去。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# AGENTS.md

`AGENTS.md` 是 Codex 读取的项目指令文件。

它不是更长的 prompt，也不是聊天记录垃圾桶。

它应该保存 Codex 每次进项目都需要知道的稳定规则：项目结构、常用命令、代码风格、工作边界和验收要求。

如果你正在处理长会话、缓存和 handoff，先看 [长期上下文怎么管理](/docs/agent-infra/context-management)。这页只讲 `AGENTS.md` 本身怎么维护。

<h2 id="who-reads-it">谁会读取它</h2>

Codex 会读取适用范围内的 `AGENTS.md`。

常见位置包括：

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

越靠近当前工作目录的文件，约束越具体。子目录里的 `AGENTS.md` 适合写这个子项目自己的规则，例如前端、后端、脚本或文档目录的特殊要求。

Codex 官方文档也提到，`AGENTS.md` 可以有替代文件名和 override 机制。普通用户第一天不用先学这些。先把项目根目录的一份维护好，已经能解决大多数问题。

<h2 id="where">放在哪里</h2>

推荐先放在项目根目录：

```text
your-project/
  AGENTS.md
  README.md
  package.json
```

如果某个子目录规则明显不同，再在子目录补一份：

```text
your-project/
  AGENTS.md
  frontend/
    AGENTS.md
```

不要一开始就到处放很多份。文件越多，越容易互相矛盾。

<h2 id="what-to-write">应该写什么</h2>

适合写：

- 项目是做什么的
- 目录结构
- 开发、测试、构建命令
- 代码风格和命名约定
- 不要改哪些文件
- 提交前必须跑哪些检查
- Windows、macOS、编码、路径等环境注意事项
- 这个项目里经常踩的坑

写法要具体。不要写“代码要优雅”。要写“改 API schema 后必须同步更新 generated types，并运行 pnpm test:types”。

<h2 id="when-update">什么时候该改它</h2>

`AGENTS.md` 不是写完就不动。

这些时候应该更新：

- 项目目录变了
- 测试、构建或发布命令变了
- 团队决定了新的代码规则
- 某个坑反复出现，需要让 Codex 以后避开
- 一次 handoff 里出现了应该长期保留的事实

但不要把 handoff 原文整段搬进去。只沉淀稳定规则。

<h2 id="handoff">从 handoff 里沉淀什么</h2>

handoff 通常会包含很多临时状态。你只需要挑能长期复用的部分。

适合进 `AGENTS.md`：

```text
这个仓库的真源文件在哪里
常用命令是什么
哪些目录不要碰
哪个旧方案已经明确废弃
完成前必须跑什么检查
```

不适合进 `AGENTS.md`：

```text
今天做到第几步
这次报错的完整日志
临时讨论过但没有采用的想法
某个 agent 的长篇自我总结
```

<h2 id="avoid">不应该写什么</h2>

不要写：

- API Key、密码、token
- 一次性任务
- 临时 TODO
- 大段错误日志
- 已经过期的路径或命令
- 不能验证的抽象要求
- 和当前目录无关的长篇背景

一句话如果不能帮助下一次 Codex 工作更稳定，就不要放进去。

<h2 id="template">最小模板</h2>

可以从这份开始：

```md
# AGENTS.md

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

把文件放好后，可以这样开场：

```text
请先读取 AGENTS.md。

先不要改文件。请告诉我：
- 这个项目是什么
- 常用命令是什么
- 哪些文件或目录不能乱改
- 完成任务前要跑哪些检查
```

确认它理解对了，再让它开始做任务。

<h2 id="claude">和 CLAUDE.md 的关系</h2>

如果你同时使用 Codex 和 Claude Code，可以同时维护 `AGENTS.md` 和 [CLAUDE.md](/docs/agent-infra/claude-md)。

原则是：两份文件写同一套事实，不要互相矛盾。

也可以在 Claude Code 的 memory 里引用现有 `AGENTS.md`，具体做法以 Claude Code 官方文档为准。对新手来说，先保证两边事实一致，比追求高级配置更重要。

<h2 id="reference">参考</h2>

- OpenAI Codex / AGENTS.md：<https://developers.openai.com/codex/guides/agents-md>
