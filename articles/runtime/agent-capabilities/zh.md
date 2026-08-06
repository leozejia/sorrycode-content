---
title: Agent 能力是怎么扩展的
slug: agent-capabilities
order: 1
summary: 分清 Runtime、Expert、Skill、MCP 和 Plugin 各自解决什么问题，以及它们如何组合。
section: runtime
section_title: 模型与工作台
section_order: 10
group: general
group_title: 通用
group_order: 40
---

# Agent 能力是怎么扩展的

Codex、WorkBuddy 等工作台会出现 Expert、Skill、MCP、Plugin 等名称。它们不是同一层能力，不同产品对名称的使用也不完全相同。

先按它们解决的问题来理解：

| 机制 | 回答的问题 | 主要作用 |
| --- | --- | --- |
| Runtime / 工作台 | 在哪里工作 | 运行 agent，管理模型、会话、权限和项目 |
| Expert / Agent | 由谁来做 | 设定角色、经验、方法和协作方式 |
| Skill | 怎么做 | 提供可复用的流程、标准和任务方法 |
| MCP / Tool / Connector | 能访问什么、能执行什么 | 连接文件、浏览器、数据库或外部服务 |
| Plugin | 怎么安装和分发 | 把相关能力打包后交给某个 runtime 安装 |

<h2 id="runtime">Runtime 决定在哪里工作</h2>

Runtime 是 agent 实际运行的工作台，例如 Codex 或 WorkBuddy。它决定可选模型、项目目录、权限确认方式，以及支持哪些扩展机制。

同一个名称在不同 runtime 中可能不是同一种技术契约。看到“Plugin”时，应先确认这是哪个产品里的 Plugin，不要把另一款产品的安装方式直接照搬过来。

<h2 id="expert">Expert 决定由谁来做</h2>

WorkBuddy 的 Expert 把角色、方法和工具组合成一个面向特定问题的执行者。Expert Team 则由负责人拆分任务，让多个 Expert 协作，再汇总结果。

Expert 本身不会获得额外系统权限。它要读取文件或访问外部服务，仍然需要通过已配置的 Skill、MCP 或工具，并遵守当前工作区的授权。

其他 runtime 可能使用 Agent、子 Agent 或自定义角色表达相近概念，不一定使用 Expert 这个名称。

<h2 id="skill">Skill 决定怎么做</h2>

Skill 是可复用的工作方法。它可以告诉 agent 一类任务的步骤、判断标准、输出格式和注意事项，也可以附带脚本、参考资料或模板。

Skill 解决的是“如何稳定完成任务”，不等于它天然拥有浏览器、数据库或外部 API 的访问权。一个 Skill 可以单独安装，也可以被打包进 Plugin。

<h2 id="tools">MCP 和工具决定能访问什么</h2>

MCP、Tool 和 Connector 负责把数据或动作交给 agent，例如读取网页、查询数据库、调用业务系统或操作本地应用。

它们通常需要单独配置和授权。Skill 可以指导 agent 何时使用这些工具，但不能代替连接、凭证和权限本身。

<h2 id="plugin">Plugin 负责打包和安装</h2>

Plugin 是 runtime 的分发单元，不是“工具”的同义词。

以 Codex 为例，一个 Plugin 可以同时包含 Skills、应用或连接器映射、MCP 配置、Hooks 和资源文件。安装 Plugin 后，实际出现的能力以及调用方式，取决于它打包了什么，并不存在跨产品通用的 `@PluginName` 调用规则。

所以，看到某项能力以 Plugin 形式提供，并不表示它不能同时包含 Skill 或 MCP。Plugin 说明的是怎么交付，Skill 和 MCP 说明的是交付了什么。

<h2 id="choose">怎么选择</h2>

- 先选择 Runtime，确定在哪个工作台完成任务
- 需要固定角色或多人协作时，使用 Expert、Agent 或对应的编排机制
- 需要复用做事方法时，安装或编写 Skill
- 需要访问外部数据或执行动作时，配置 MCP、Tool 或 Connector
- 需要把多种能力一起交付给团队时，再使用 Plugin 打包和分发

例如，一个 WorkBuddy Expert 可以按某套 Skill 工作，并通过 MCP 查询资料；一个 Codex Plugin 也可以把 Skill 和 MCP 配置一起安装。它们是组合关系，不是互相替代。

<h2 id="next">继续阅读</h2>

- [WorkBuddy](/docs/runtime/workbuddy)：配置模型，并了解 Expert 和 Expert Team
- [让 AI 记住工作方法](/docs/agent-memory/remember-skills)：理解和使用 Skills
- [Codex](/docs/runtime/codex)：安装并接入 SorryCode

上游定义以 [Codex Plugin 文档](https://developers.openai.com/plugins/build/plugins) 和 [WorkBuddy Expert 中心](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center) 为准。
