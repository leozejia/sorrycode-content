---
title: Claude Fable 5 怎么用
slug: claude-fable-5
order: 2
summary: 用 Claude Fable 5 处理长程复杂任务，正确选择 effort，并重新审查为旧模型编写的提示词和 Skills。
section: runtime
section_title: 模型与工作台
section_order: 10
group: anthropic
group_title: Anthropic
group_order: 20
---

# Claude Fable 5 怎么用

`claude-fable-5` 是 Anthropic 面向高难度推理和长程 Agent 任务的模型。它适合过去需要人工作数小时、数天，或者需要多轮交接才能完成的工作。

如果你还没有接入 Claude Code，先完成[模型与工作台 / Claude Code](/docs/runtime/claude-code)。这页不重复安装和 API Key 配置，只讲什么时候选 Fable 5，以及怎样给它任务。

<h2 id="when-to-use">什么时候选 Fable 5</h2>

| 任务 | 建议 |
| --- | --- |
| 大型重构、复杂调试、跨仓库调查 | 适合 |
| 需要持续数小时并自行验证的完整项目 | 适合 |
| 复杂代码审查、文档或企业工作流 | 适合 |
| 一次简单改字、格式转换、短问答 | 先用更轻的模型 |
| 需要进攻性网络安全或部分生命科学内容 | 可能触发安全拒绝 |

测试 Fable 5 时，不要只给它一道简单题。给它一个边界明确、过去需要多轮推进的真实任务，才能看出长程执行、验证和委派能力。

<h2 id="first-run">最短使用路径</h2>

1. 完成 Claude Code 接入，并确认 API Key 和网络链路正常。
2. 在支持模型选择的入口中选择 `claude-fable-5`。
3. 大多数任务从 `high` effort 开始。
4. 写清目标、背景、权限边界、完成标准和证据要求。
5. 让它端到端执行，再根据耗时和结果调整 effort。

第一次可以复制这段：

```text
我正在做 [项目或更大的目标]，这项工作最终要给 [使用者] 使用。

请先读取 [真源文件或目录]，完成 [具体交付物]。

你可以执行：
- [允许的本地、可逆动作]

遇到这些情况必须停下：
- [破坏性动作、外部写入、真实范围变化]

完成标准：
- [可检查结果]
- [必须通过的测试或验证]

报告进度前，请把每一条声明和本次会话中的工具结果核对。没有验证的步骤明确写出来。
```

<h2 id="effort">怎么选 effort</h2>

| effort | 适合什么任务 |
| --- | --- |
| `low` | 日常、低风险、强调交互速度的工作 |
| `medium` | 常规任务，需要一定推理但不值得长时间运行 |
| `high` | 大多数 Fable 5 任务的默认起点 |
| `xhigh` | 能力优先、验证要求高、确实困难的任务 |

更高的 effort 会带来更完整的推理和验证，也可能收集过多上下文、重复讨论已决定的问题，或者顺手做没有要求的整理。

任务正确但明显太慢，先降低 effort。不要继续往系统提示词里叠加“不要想太多”“不要过度规划”之类的补丁。

<h2 id="prompting">提示词要短，但不能空</h2>

Fable 5 的指令遵循更强，一句清楚的要求往往比一长串禁用项更稳定。

需要保留：

- 为什么做这件事
- 哪些文件或数据是真源
- 哪些动作已经授权
- 哪些动作必须确认
- 什么结果算完成
- 完成声明需要哪些证据

可以先删除：

- 同一偏好的重复表述
- 为旧模型补写的逐项禁令
- 要求模型复述完整内部推理的指令
- 和当前任务无关的工具与示例

短提示词不是少交代信息。它是一份短而完整的任务契约。

<h2 id="long-runs">长程任务怎样防止虚假进度</h2>

Anthropic 建议把进度声明绑定到本次会话里的真实工具结果。可以把这条规则放进长任务提示词：

```text
报告进度前，逐条核对本次会话中的工具结果。
只能报告有证据支持的工作。
测试失败就报告失败，步骤跳过就说明跳过，没有验证就明确写未验证。
```

这条规则约束的是完成声明，不是模型怎样思考，适合长期保留。

<h2 id="boundaries">自治边界集中写一次</h2>

Fable 5 更愿意主动推进，也可能做出没有请求的动作。把边界按请求类型写清楚：

- 问答、讨论、诊断和审查只输出判断，不自动修复。
- 明确要求修改时，可以完成范围内、可逆的本地动作。
- 删除、重启、修改外部配置、发送消息和扩大范围前，需要证据和用户确认。

不要在每个工具前重复“先问我”。集中写一份短策略，模型更容易持续推进，也更容易在真正需要确认的地方停下。

<h2 id="subagents">什么时候用子 Agent</h2>

Fable 5 更擅长并行调度子 Agent。只有任务能拆成互不依赖的工作流时才值得并行，比如：

- 分别阅读多个独立仓库
- 同时核对不同来源
- 将实现、测试和独立复核分开

主 Agent 应继续推进自己的工作，并在子 Agent 缺少上下文或偏离目标时介入。需要共享同一份频繁变化状态的任务，不适合强行并行。

<h2 id="memory">记忆只保存已验证经验</h2>

长期任务可以给 Agent 一个明确的经验目录，但不要让它到处建立状态台账。

一份经验文件只记录一条已验证经验，开头写一句摘要。仓库和聊天记录里已经存在的内容不要再抄一份；旧结论被推翻后，及时更新或删除。

需要管理长会话、缓存和 handoff 时，继续看[会话太长怎么办](/docs/agent-memory/context-management)。

<h2 id="migration">迁移旧提示词和 Skills</h2>

Anthropic 明确提醒：为旧模型编写的 Skills 可能规定得太细，并降低 Fable 5 的输出质量。

不要一次清空所有规则。按这套顺序迁移：

1. 选出 3 到 5 个真实、可重复的代表性任务。
2. 保存当前结果，记录成功率、完整性、证据、耗时和成本。
3. 每次只删除一组重复指令、旧示例或无关工具。
4. 用完全相同的任务重新测试。
5. 默认表现更好就保留删除；出现可测退步就恢复那条规则。

完整审计方法见[强模型的项目规则怎么写](/docs/agent-memory/strong-model-project-rules)。

<h2 id="refusal">遇到 refusal 怎么办</h2>

Fable 5 会对部分网络安全、生命科学和提取内部推理的请求运行安全分类器。API 可能返回 `stop_reason: "refusal"`。

先确认请求是否落在受限范围。正常业务也可能被误判，需要自动恢复的集成可以按 Anthropic 官方建议配置回退模型，例如 Claude Opus 4.8。不要把同一请求无修改地无限重试。

<h2 id="next">下一步</h2>

- 接入 Claude Code：[模型与工作台 / Claude Code](/docs/runtime/claude-code)
- 管理长会话：[Agent 基建 / 会话太长怎么办](/docs/agent-memory/context-management)
- 审计项目规则：[Agent 基建 / 强模型的项目规则怎么写](/docs/agent-memory/strong-model-project-rules)

<h2 id="reference">参考</h2>

- Anthropic / Prompting Claude Fable 5：<https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5>
- Anthropic / Introducing Claude Fable 5 and Claude Mythos 5：<https://platform.claude.com/docs/en/about-claude/models/introducing-claude-fable-5-and-claude-mythos-5>
