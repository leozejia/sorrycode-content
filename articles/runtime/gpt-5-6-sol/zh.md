---
title: GPT-5.6 Sol 怎么用
slug: gpt-5-6-sol
order: 2
summary: 用 GPT-5.6 Sol 处理复杂专业任务，正确选择 reasoning effort，并用代表性任务验证精简提示词的效果。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# GPT-5.6 Sol 怎么用

`gpt-5.6-sol` 是 GPT-5.6 系列中的前沿模型，适合复杂专业工作、长上下文和多步骤 Agent 任务。`gpt-5.6` 别名也会路由到 Sol。

如果你还没有接入 Codex，先完成[模型与工作台 / Codex](/docs/runtime/codex)。这页不重复安装和 API Key 配置，只讲怎样选择 Sol、控制推理预算和整理提示词。

<h2 id="when-to-use">什么时候选 Sol</h2>

| 任务 | 建议 |
| --- | --- |
| 复杂编码、研究、调试和专业知识工作 | 适合 |
| 需要长上下文、多轮工具调用和持续验证 | 适合 |
| 很看重最终质量，成本和延迟可以接受 | 适合 |
| 高并发、成本敏感、简单重复任务 | 先比较 Terra 或 Luna |
| 一次简单格式转换或短问答 | 不必默认使用最高档模型 |

Sol 有 105 万 Token 上下文窗口和最高 128,000 Token 输出。更大的窗口解决的是“装不下”，不会自动判断哪些历史信息还值得保留。

<h2 id="first-run">最短使用路径</h2>

1. 完成 Codex 接入，并确认 API Key 和网络链路正常。
2. 选择 `gpt-5.6-sol`。
3. 从 `medium` reasoning effort 开始。
4. 写清目标、事实来源、授权边界、证据和完成标准。
5. 用真实任务比较质量、Token、延迟和成本，再决定是否升到 `high`、`xhigh` 或 `max`。

第一次可以复制这段：

```text
目标：完成 [具体交付物]。

背景：
- [为什么做]
- [使用者是谁]

真源：
- [必须读取的文件、页面或数据]

权限：
- 可以执行 [本地、可逆动作]
- 遇到 [外部写入、破坏性动作、真实范围变化] 时停下确认

完成标准：
- [可检查结果]
- [测试、引用或浏览器验证]

先完成范围内的工作，再报告结果。没有验证的内容明确标为未验证。
```

<h2 id="reasoning-effort">怎么选 reasoning effort</h2>

GPT-5.6 支持 `none`、`low`、`medium`、`high`、`xhigh` 和 `max`。

| 等级 | 适合什么任务 |
| --- | --- |
| `none` | 只看延迟的基线，任务不依赖推理或工具 |
| `low` | 延迟敏感、边界清楚的工作 |
| `medium` | 默认平衡起点 |
| `high` / `xhigh` | 真实评测证明更多推理能提高质量 |
| `max` | 最难、质量优先、允许更高延迟和成本的任务 |

从旧模型迁移时，先保留原来的 effort，再比较同一级和低一级。GPT-5.6 的 Token 效率更高，低一级也可能保持或提高质量。

<h2 id="max-pro-ultra">Max、Pro 和 Ultra 不是一回事</h2>

| 名称 | 它控制什么 |
| --- | --- |
| `max` | 单个 GPT-5.6 实例的 reasoning effort |
| Pro mode | 同一个 GPT-5.6 模型投入更多计算，API 使用 `reasoning.mode: "pro"` |
| Ultra | Codex 中的多 Agent 协作设置，默认协调 4 个 Agent 并行工作 |

Ultra 不是 `reasoning.effort` 的一个等级，也不是名为 `gpt-5.6-sol-ultra` 的模型。OpenAI API 提供 multi-agent beta，用来构建类似 Ultra 的体验；是否能在当前客户端或账户中直接看到 Ultra，以产品实际开放情况为准。

不要在提示词里写“请使用 Pro”或“请更努力思考”。运行模式通过产品设置或 API 参数选择，提示词继续描述目标、上下文、约束、证据和输出格式。

<h2 id="lean-prompts">精简提示词要做对照实验</h2>

OpenAI 在一组内部编码 Agent 评测中发现，删除重复指令和示例、缩短工具说明后：

- 评测分数约提高 10% 到 15%
- 总 Token 减少 41% 到 66%
- 成本减少 33% 到 67%

这些数字只代表内部样本里的方向，不是所有项目都能复现。

正确的精简方法：

1. 从一套已经能工作的提示词和工具集开始。
2. 每次只删除一组指令、示例或工具。
3. 重跑完全相同的代表性任务。
4. 比较成功率、完整性、证据、Token、延迟和成本。
5. 保留确实承载产品要求或修复过可测缺口的规则。

不要把几百行直接删到几十行，再用 Token 下降证明改动成功。完整方法见[强模型的项目规则怎么写](/docs/agent-memory/strong-model-project-rules)。

<h2 id="autonomy">用一份紧凑策略定义自治边界</h2>

Sol 在多步骤任务里更主动。把授权按动作风险分层：

- 回答、解释、审查、诊断和规划，只读材料并报告。
- 修改、构建和修复，可以完成范围内的本地改动与非破坏性验证。
- 外部写入、破坏性动作、付费操作和明显扩大范围，需要用户确认。

这份策略集中写一次就够。反复写“先问我”和“不要修改”，可能让模型在读取文件、检查日志和运行测试前也不断停下。

<h2 id="tools">什么时候用程序化工具调用</h2>

程序化工具调用（Programmatic Tool Calling）允许 GPT-5.6 在托管运行时中写 JavaScript，批量调用符合条件的工具，并压缩中间结果。

适合：

- 过滤、连接、排序和去重
- 聚合大量结构相同的结果
- 有明确输入输出结构的批量验证

不适合：

- 一次普通工具调用就能完成
- 每个中间结果都会改变下一步判断
- 动作需要人工审批
- 最终结果必须保留原始文件或引用

同时使用普通调用和程序化调用时，只设一次交接。写清程序化阶段可以使用哪些工具、输出结构、并发和重试上限、停止条件，以及哪些判断必须回到普通调用完成。

<h2 id="context">长上下文也要控制重复</h2>

GPT-5.6 支持持久化推理和显式 Prompt caching。只有目标、假设和优先级跨轮次保持稳定时，才值得复用以前的推理。

方向已经改变，早期推理就不再相关。继续保留只会把旧结论带进下一轮。需要判断什么时候清理、交接或开新会话时，继续看[会话太长怎么办](/docs/agent-memory/context-management)。

<h2 id="checklist">完成前检查</h2>

```text
目标是否已经交付
每条完成声明是否有工具结果支持
测试失败和跳过步骤是否如实报告
提示词里是否有重复指令
当前任务是否暴露了无关工具
提高 effort 后的质量增益是否值得 Token、延迟和成本
```

<h2 id="next">下一步</h2>

- 接入 Codex：[模型与工作台 / Codex](/docs/runtime/codex)
- 管理长会话：[Agent 基建 / 会话太长怎么办](/docs/agent-memory/context-management)
- 审计项目规则：[Agent 基建 / 强模型的项目规则怎么写](/docs/agent-memory/strong-model-project-rules)

<h2 id="reference">参考</h2>

- OpenAI / GPT-5.6 模型指南：<https://developers.openai.com/api/docs/guides/latest-model>
- OpenAI / GPT-5.6 Sol 模型页：<https://developers.openai.com/api/docs/models/gpt-5.6-sol>
- OpenAI / GPT-5.6 发布说明：<https://openai.com/index/gpt-5-6/>
