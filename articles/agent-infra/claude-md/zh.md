---
title: CLAUDE.md
slug: claude-md
order: 3
summary: Claude Code 读取的 memory / instruction 文件。适合写项目背景、常用命令和长期协作规则。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# CLAUDE.md

`CLAUDE.md` 是 Claude Code 读取的 memory / instruction 文件。

它适合保存项目背景、常用命令、长期偏好和协作规则。和 `AGENTS.md` 类似，它的目标是减少每次重新解释。

这是 Claude Code 官方支持的记忆机制，不是 SorryCode 自己发明的约定。

<h2 id="who-reads-it">谁会读取它</h2>

Claude Code 会读取适用范围内的 `CLAUDE.md`。

常见位置包括：

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
your-project/apps/web/CLAUDE.md
```

具体加载规则以 Claude Code 官方文档为准。公开文档只建议一个稳定做法：项目根目录放一份 `CLAUDE.md`，长期维护。

<h2 id="where">放在哪里</h2>

最稳的做法是先放在项目根目录：

```text
your-project/
  CLAUDE.md
  README.md
```

如果你想写个人长期偏好，可以使用用户级 memory；如果你想写项目规则，优先放项目里的 `CLAUDE.md`。

<h2 id="how-it-works">如何生效</h2>

Claude Code 会在会话中加载可用 memory。你可以在第一次进入项目时显式确认：

```text
请先读取 CLAUDE.md，再告诉我这个项目的常用命令和注意事项。
```

如果你修改了 `CLAUDE.md`，后续会话应该以新内容为准。当前会话里不确定是否已经刷新时，直接让 Claude Code 重新读取它。

<h2 id="what-to-write">应该写什么</h2>

适合写：

- 项目是什么
- 常用开发、测试、构建命令
- 代码风格和目录约定
- 常见坑和不要做的事
- 重要业务规则
- 团队协作偏好

<h2 id="avoid">不应该写什么</h2>

不要写：

- API Key、token、密码
- 一次性任务和临时 TODO
- 已经过期的命令
- 过长的会议纪要
- 和 agent 工作无关的信息

<h2 id="template">最小模板</h2>

```md
# CLAUDE.md

## Project Context

This project is ...

## Common Commands

- Test:
- Build:

## Working Rules

- ...

## Avoid

- ...
```

<h2 id="relationship">和 AGENTS.md 的关系</h2>

如果你同时使用 Codex 和 Claude Code，可以同时维护 `AGENTS.md` 和 `CLAUDE.md`。

原则是：两份文件写同一套事实，不要互相矛盾。可以把更通用的项目规则放进两边，把 runtime 专属规则放在对应文件里。

<h2 id="reference">参考</h2>

- Claude Code / Memory：<https://code.claude.com/docs/en/memory>
