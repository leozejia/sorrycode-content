---
title: Skills 是什么
slug: skills
order: 8
summary: Skill 是给 Agent 复用的工作说明。按需选择，不必先装一套推荐清单。
section: concepts
section_title: 核心概念
section_order: 5
---

# Skills 是什么

当你反复让 Agent 按同一套步骤做事，可以把这套方法保存成 Skill，下次需要时再读取。

一个 Skill 通常以 `SKILL.md` 为主说明，还可以附带参考资料、脚本和模板。它告诉 Agent 这类任务怎么做，不是另一个模型。

<h2 id="when-to-use">什么时候需要</h2>

先直接让 Agent 完成任务。已有能力够用，就不必额外安装 Skill。

当你需要复用某种工作流程、输出格式或检查标准时，再选适合自己的 Skill。不同人的任务和偏好不同，没有必须先装的通用清单。

<h2 id="use">怎么用</h2>

1. 选择可信来源，读清用途、依赖和权限要求。
2. 按所用 Agent 的说明安装，确认它能识别。不同客户端的安装位置和管理方式可能不同。
3. 在任务里点名 Skill，说清输入、目标和输出位置。

比如，已经安装一个整理报告的 Skill 后，可以说：

```text
请用我安装的「报告整理」Skill 处理 notes.md，输出到 outputs/report.md。缺少材料先问我，不要编造数据。
```

「报告整理」只是示例名称，替换成你实际安装的 Skill。安装脚本可能执行命令或访问文件，不要直接运行不明来源的内容。

<h2 id="make">能做自己的 Skill 吗</h2>

可以。把反复使用的步骤、示例和验收标准交给 Agent，让它按当前客户端支持的格式整理成 Skill，再用真实任务测试。只保留确实有用的流程，不用把每个临时要求都写进去。

<h2 id="relationship">和项目规则、MCP 有什么区别</h2>

- `AGENTS.md / CLAUDE.md`：项目长期规则，见[项目规则说明](/docs/agent-memory/remember-rules)。
- `DESIGN.md`：项目的视觉要求，见[设计风格说明](/docs/agent-memory/remember-design)。
- Skill：某类任务按需读取的工作方法。
- MCP：连接工具和数据的协议，不是工作方法本身。

Skill 不自动提供工具、API Key 或额外权限，也不保证结果正确。Magpie 负责模型接入，这和安装 Skill 是两件事；外部服务仍需单独配置和授权，重要产物仍需检查。
