---
title: AGENTS.md
slug: agents-md
order: 2
summary: Codex 读取的项目指令文件。适合写项目结构、测试命令、代码规范和工作约束。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# AGENTS.md

`AGENTS.md` 是 Codex 读取的项目指令文件。

它适合放项目规则、测试命令、代码风格、目录说明和工作约束。你可以把它理解成写给 Codex 的项目说明书。

这是 Codex 官方支持的机制，不是 SorryCode 自己发明的约定。

<h2 id="who-reads-it">谁会读取它</h2>

Codex 会读取适用范围内的 `AGENTS.md`。

常见位置包括：

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

越靠近当前工作目录的 `AGENTS.md`，约束越具体。子目录里的规则可以补充或覆盖上层规则。

如果一个任务涉及多个目录，Codex 会按实际工作目录和文件范围读取对应规则。更深层目录里的 `AGENTS.md` 适合写这个子项目自己的规则，例如前端、后端、脚本或文档目录的特殊约束。

<h2 id="where">放在哪里</h2>

推荐先放在项目根目录：

```text
your-project/
  AGENTS.md
  README.md
  package.json
```

如果某个子目录有不同规则，再在子目录补一份：

```text
your-project/
  AGENTS.md
  frontend/
    AGENTS.md
```

不要一开始就到处放很多份。先维护根目录一份，等真的出现不同规则再拆。

<h2 id="how-it-works">如何生效</h2>

把 `AGENTS.md` 放进项目后，Codex 在这个项目里工作时会读取它。你不需要每次都把整份文件复制进提示词。

但第一次使用时，可以显式提醒：

```text
请先读取 AGENTS.md，再告诉我这个项目的开发和测试规则。
```

<h2 id="what-to-write">应该写什么</h2>

适合写：

- 项目目录结构
- 开发、测试、构建命令
- 代码风格和命名约定
- 不要改哪些文件
- 提交前必须跑哪些检查
- Windows、macOS、编码、路径等环境注意事项

<h2 id="avoid">不应该写什么</h2>

不要写：

- API Key、密码、token
- 一次性任务
- 已经过期的路径或命令
- 不能验证的抽象要求
- 和当前目录无关的长篇背景

<h2 id="template">最小模板</h2>

```md
# AGENTS.md

## Project

This project is ...

## Commands

- Install:
- Test:
- Build:

## Code Style

- ...

## Do Not

- Do not ...
```

<h2 id="reference">参考</h2>

- OpenAI Codex / AGENTS.md：<https://developers.openai.com/codex/guides/agents-md>
