---
title: Skills 是什么
slug: featured-skills
order: 1
summary: Skill 是给 agent 读的操作说明书。装好 Codex 或 Claude Code 后，用 Skills 让 agent 稳定完成图片、排版、PPT、读项目和工程流程。
section: skills
section_title: Skills
section_order: 15
---

# Skills 是什么

Skill 是给 agent 读的操作说明书。

你不用把每一步都学会。装好 `Codex` 或 `Claude Code`，再装上合适的 skill，然后直接对 agent 说：

```text
请用 SorryCode Image2 帮我生成一张封面。
```

```text
请用 Kami 把这份内容做成一页纸。
```

```text
请用 Waza 帮我检查这次改动。
```

Skill 会告诉 agent 怎么检查前置条件、怎么做、怎么保存结果、遇到问题怎么提醒你。

<h2 id="why-skills">为什么要用 Skills</h2>

只靠“模型很聪明”还不够。

顶流模型能理解很多问题，但它不一定知道：

- 这个任务应该先检查什么
- 默认用哪个模型、接口或模板
- 结果应该保存到哪里
- 哪些错误要用小白能懂的话解释
- 哪些重复步骤应该交给脚本，而不是每次临场手写

Skill 把这些经验变成可复用的能力包。你装一次，以后就可以反复让 agent 按同一套方法做事。

<h2 id="trigger">怎么稳定触发</h2>

最不容易触发错的办法，是直接说 skill 名。

```text
请用 SorryCode Image2 编辑 ./input/product.png，把它改成官网 hero 风格，保存到 outputs/images/product-hero/。
```

```text
请用 Kami 把 notes.md 排版成一份正式的一页纸 PDF。
```

```text
请用 Waza 的 check 帮我提交前检查这次改动。
```

如果你想更稳定，句子里带上三件事：

- 用哪个 skill
- 要做什么
- 输入文件或保存位置在哪里

<h2 id="agent-install">让 Agent 帮你安装 Skills</h2>

如果你已经把 `Codex` 或 `Claude Code` 跑起来了，下一步不用自己研究 `npx`、`Git` 或 `Homebrew`。

把下面这段话复制给你当前正在使用的 agent，让它自己读取当前文档、检查环境、判断要装哪些 skills：

```text
请阅读 SorryCode 当前 Skills 入口：https://sorrycode.com/docs/skills/featured-skills.md?locale=zh。我的 Mac 默认什么环境都没有，请你先检查并准备必要环境，然后根据当前 Skills 文档里的分类、推荐顺序和我的使用目标，判断并安装适合我的 skills。不要使用固定旧清单；请读取当前文档后再决定。安装前告诉我你要做什么，安装后验证当前 agent 能识别这些 skills，并报告成功、失败和下一步。
```

这里故意使用 `.md?locale=zh` 链接。它是给 agent 读取的 Markdown 正文，比普通网页更稳定。

<h2 id="manage-skills">查看和卸载 Skills</h2>

站内大多数安装命令都带 `-g`，也就是装到全局目录。小白不要先在项目目录里猜名字，先看全局安装了什么：

```bash
npx skills list --global
```

卸载单个全局 skill：

```bash
npx skills remove --global skill-name
```

如果不知道准确名称，从 `npx skills list --global` 的结果里复制。不要凭记忆输入，尤其是 `Waza`、`DBSkill` 这类整包，它们可能会装出多个子 skill。

如果还是找不到，把这句话交给当前 agent：

```text
请帮我检查 Codex / Claude Code / agents 的 skills 安装目录，找出这个 skill 实际装在哪里。优先告诉我应该怎么用 npx skills remove 卸载；如果 CLI 处理不了，先说明目录路径和风险，等我确认后再处理。
```

**危险操作：`npx skills remove --all` 会清掉当前 CLI 能管理范围内的所有 skills。除非你明确想重置环境，否则不要运行。**

<h2 id="start">先装哪个</h2>

如果你还没装 runtime，先从这里开始：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

已经装好 runtime 后，可以按目标选：

- 第一次做 PPT、设计、图片、一页纸或封面：[Skills / 设计类 Skills 怎么用](/docs/skills/design-workflow)
- 想处理 Word / Excel / PPT / PDF：[Skills / 办公文档](/docs/skills/office-docs)
- 想生成图片、做一页纸、简历、报告或网页 PPT：[Skills / 创作与设计](/docs/skills/creation-design)
- 想诊断商业问题、找对标或判断内容方向：[Skills / DBSkill](/docs/skills/dbskill)
- 想让 AI 编程任务先想清楚再动手：[Skills / Waza](/docs/skills/waza)

如果你想理解 `AGENTS.md / CLAUDE.md / DESIGN.md / MCP / Skills` 这些标准文件、协议和能力包，去 [Agent 基建](/docs/agent-infra/overview)。

<h2 id="deeper">想多了解一点：Skills 为什么特殊</h2>

普通提示词是一次性的。Skill 是可以安装、复用、分发和迭代的能力包。

一个 skill 通常包含：

- `SKILL.md`：agent 触发后会读的说明
- `description`：帮助 agent 判断什么时候该用它
- `references`：需要时再读的参考资料
- `scripts`：稳定执行某些操作的脚本
- `assets`：模板、字体、样式或示例文件

所以 skill 不是“更长的提示词”，而是把一套工作流交给 agent。

<h2 id="mechanism">Skill 是怎么触发的</h2>

最重要的是 `SKILL.md` 顶部的 `description`。

你可以把它理解成 skill 的“使用说明标签”。agent 会根据用户的话和 `description` 判断要不要加载这个 skill。

不稳定的写法：

```text
Useful assistant tool.
```

更稳定的写法：

```text
Generate or edit images. Use when the user asks for covers, posters, product visuals, avatars, game sprites, or restyling an existing image.
```

对普通用户来说，不需要先学这些规则。你只要在请求里直接点名 skill，就已经是最稳定的触发方式。

<h2 id="skill-creator">用 Skill Creator 做自己的 Skills</h2>

当你发现自己反复对 agent 说同一套要求，就可以考虑做一个自己的 skill。

这在设计、PPT、图片和写作类任务里尤其重要。稳定出现的风格偏好、修改意见和验收标准，可以沉淀到自己的 `DESIGN.md`、references 或 skill，让 agent 下次更快接近你要的方向。

`Skill Creator` 做的不是帮你写一条更长的 prompt，而是把工作流变成可复用能力：

1. 收集真实使用场景
2. 写清楚什么时候应该触发
3. 把稳定流程写进 `SKILL.md`
4. 把长资料放进 `references`
5. 把容易出错的重复操作做成 `scripts`
6. 用真实任务测试，再继续迭代

如果你已经装好了 Codex，可以直接对它说：

```text
请用 Skill Creator 帮我把这套重复工作流做成一个 skill。先问我三个关键问题，再给出 skill 的结构草案。
```

<h2 id="runtime-plus-skills">为什么是 Runtime + Skills</h2>

`Codex` / `Claude Code` 解决的是 agent 在哪里工作：读项目、改文件、执行命令、持续对话。

`Skills` 解决的是 agent 应该怎么做某类任务：检查什么、调用什么、保存到哪里、用什么标准判断完成。

你可以这样理解：

```text
Runtime = agent 的工作台
Skills = agent 的专业操作手册
```

这也是 SorryCode 主张大家学会 `Codex / Claude Code + Skills` 的原因。你不是只学一个工具，而是在搭建一套可以长期复用的 AI 工作方式。
