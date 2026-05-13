---
title: Skills
slug: skills
order: 7
summary: Skills 是 agent 可安装、可复用的能力包。它用 SKILL.md、参考资料、脚本和资产把工作流交给 agent。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# Skills

`Skills` 是 agent 可安装、可复用的能力包。

如果说 runtime 解决“agent 在哪里工作”，skills 解决的是“agent 遇到某类任务时应该怎么做”。

它不是 SorryCode 私有概念。Codex 官方文档已经把 skills 写成可复用工作流的 authoring format，并说明它基于 open agent skills standard。不同 agent runtime 对安装位置和加载细节会不同，但核心心智一致：把一类任务的做法沉淀成可复用能力包，让 agent 在合适的时候读取。

<h2 id="what-is-it">它是什么</h2>

一个 skill 通常包含：

- `SKILL.md`：agent 读取的主说明
- `description`：帮助 agent 判断什么时候触发
- `references`：按需读取的长资料
- `scripts`：稳定执行重复操作的脚本
- `assets`：模板、字体、图片、示例文件
- `agents/openai.yaml`：可选，给 Codex App 提供展示、调用策略和依赖声明

所以 skill 不是一条更长的 prompt，而是一套可复用工作流。

Codex 会先把 skill 的 `name / description / 文件路径` 放进上下文，用来判断是否需要这个 skill。只有当它决定使用某个 skill 时，才读取完整 `SKILL.md`。这就是 progressive disclosure：先看短描述，需要时再加载完整说明，避免所有 skill 一开始就挤满上下文。

<h2 id="who-reads-it">谁会读取它</h2>

读取者是支持 skills 的 agent runtime，比如 Codex、Claude Code 或其他兼容工作台。

用户通常不需要背 skill 的内部内容。更好的用法是直接点名：

```text
请用 Kami 把这段内容做成一页纸。
```

<h2 id="trigger">如何触发</h2>

稳定触发 skill 的方法很简单：

- 直接点名 skill，例如“请用 Kami”；在 Codex CLI / IDE 里也可以用 `/skills` 或 `$` 选择 skill
- 描述任务类型，例如“帮我把这段内容做成一页纸”
- 提供输入材料、目标受众和输出位置
- 如果有项目规则，要求 agent 先读 `AGENTS.md / CLAUDE.md / DESIGN.md`

不要只说“帮我优化一下”。任务越像 skill 描述里的场景，越容易稳定触发。

<h2 id="how-to-make">如何制作 skill</h2>

制作 skill 的核心不是把 prompt 写长，而是把工作流拆清楚：

1. 写清楚这个 skill 适合什么任务。
2. 在 `SKILL.md` 里写 agent 执行步骤。
3. 把长参考资料放进 `references/`，让 agent 按需读取。
4. 把重复、易错、需要稳定执行的动作写成 `scripts/`。
5. 把模板、字体、示例文件放进 `assets/`。
6. 用真实任务测试触发是否稳定。

如果你经常重复同一类工作，可以用 `Skill Creator` 把它做成自己的 skill。

<h2 id="where">放在哪里</h2>

Codex 会从多个位置读取 skills。对普通用户来说，最常见的是：

- 仓库内：`.agents/skills`
- 用户级：`~/.agents/skills`
- Codex 内置：系统自带 skills，例如 `skill-creator`

仓库里的 skills 适合团队共用，用户级 skills 适合你自己跨项目使用。公开 docs 推荐的一键安装命令，通常就是把 skill 安装到用户级位置。

如果新安装的 skill 没出现，先重启 runtime。

<h2 id="problem">它解决什么问题</h2>

没有 skill 时，agent 每次都要临场判断：

- 该先检查什么
- 用哪个工具
- 文件保存在哪里
- 失败时怎么解释
- 结果怎么验证

Skill 把这些经验写下来，让同类任务更稳定。

<h2 id="relationship">和 AGENTS.md / MCP 的区别</h2>

- `AGENTS.md / CLAUDE.md`：项目级长期规则
- `DESIGN.md`：设计上下文
- `MCP`：工具和数据连接协议
- `Skills`：某类任务的工作流能力包

它们可以组合。比如一个图片 skill 可以读取 `DESIGN.md`，再调用图片 API 或 MCP 工具。

<h2 id="where-next">下一步</h2>

如果你想安装具体 skills，去 [Skills / Skills 是什么](/docs/skills/featured-skills)。

<h2 id="reference">参考</h2>

- OpenAI Codex / Skills：<https://developers.openai.com/codex/skills>
