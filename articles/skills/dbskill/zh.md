---
title: DBSkill
slug: dbskill
order: 2
summary: dontbesilent 的商业诊断与内容决策工具箱。帮你判断商业问题、找对标、做内容诊断、优化开头标题，也能处理执行力和概念混乱。
section: skills
section_title: Skills
section_order: 15
group_order: 30
group_title: 工作流
group: workflow
source_url: https://github.com/dontbesilent2025/dbskill
---

# DBSkill

`DBSkill` 是 dontbesilent 开源的商业诊断工具箱。

如果你在做产品、内容、商业项目，经常卡在“这个问题到底成不成立”“我该学谁”“内容为什么不对”“我为什么知道该做但做不动”，可以装这套 skill。

它更像一组商业问诊工具，不是普通写作助手。它的价值不是帮你多写几段话，而是帮你先判断：你是不是在错误的问题上用力。

<h2 id="what-is-it">它是什么</h2>

`DBSkill` 是一整套 skills。它把商业诊断、对标分析、内容诊断、标题开头优化、执行力诊断、概念拆解这些动作做成可触发的 agent 工作流。

你不需要记住所有子 skill。第一次使用时，先记住主入口 `dbs` 就够了。你把问题讲出来，让它判断应该进入哪条诊断路径。

<h2 id="who-is-it-for">适合谁</h2>

它适合这些人：

- 正在做产品、服务、内容账号或商业项目
- 想判断一个商业问题是不是真的成立
- 想找对标，但不知道该模仿谁
- 想诊断选题、短视频开头、小红书标题
- 明明知道该做什么，但一直拖延或绕开关键动作
- 经常被“定位、赛道、需求、增长”这类词绕晕

如果你只是想生成图片、排版文档或做网页 PPT，先看：

- [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- [Skills / Kami](/docs/skills/kami)
- [Skills / Magazine Web PPT](/docs/skills/magazine-web-ppt)

<h2 id="install">安装</h2>

先确认你已经装好了 `Codex` 或 `Claude Code`。

### Codex

```bash
npx skills add dontbesilent2025/dbskill -a codex -g -y
```

### Claude Code

```bash
npx skills add dontbesilent2025/dbskill -a claude-code -g -y
```

如果你还没装好 runtime，先回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="common-scenes">最常用的场景</h2>

### 不知道该用哪个工具

```text
请用 dbs 帮我判断一下：我现在这个项目最大的问题是什么？先帮我选择应该进入商业诊断、对标分析、内容诊断、执行力诊断，还是概念拆解。
```

### 诊断商业问题

```text
请用 dbs-diagnosis 诊断一下我的商业模式。我会先描述我在做什么，你不要急着给建议，先判断我的问题本身是否成立。
```

### 找对标

```text
请用 dbs-benchmark 帮我找对标。我想做的是：____。请先帮我排除不该模仿的对象，再告诉我真正值得学谁。
```

### 做内容判断

```text
请用 dbs-content 帮我诊断这个选题能不能做、应该怎么做。我会先贴出选题和目标平台。
```

### 知道该做但做不动

```text
请用 dbs-action 帮我诊断为什么我知道该做这件事，但一直没有开始。请直接指出我可能在逃避什么。
```

<h2 id="tool-map">工具箱怎么理解</h2>

你可以把它分成四组：

- 商业判断：`dbs`、`dbs-diagnosis`、`dbs-benchmark`
- 内容增长：`dbs-content`、`dbs-hook`、`dbs-xhs-title`、`dbs-ai-check`
- 行动与思考：`dbs-action`、`dbs-slowisfast`、`dbs-deconstruct`、`dbs-chatroom`
- Agent 工作台：`dbs-agent-migration`

第一次不要试图全部学会。先从 `dbs` 主入口开始，让 agent 帮你分流。

<h2 id="relationship">和其他 Skills 的关系</h2>

- `DBSkill`：判断商业问题、内容方向和行动卡点
- `Waza`：让 AI 编程流程更稳
- `Kami`：把内容做成成品文档、简历、作品集、PPT
- `SorryCode Image2`：生成图片、封面、海报、插图

一个自然组合是：先用 `DBSkill` 判断方向，再用 `Kami`、`Magazine Web PPT` 或 `SorryCode Image2` 做成品。

<h2 id="common-issues">常见问题</h2>

- 我是不是要记住 13 个 skill 名字
  不用。先用 `dbs` 主入口，让它判断该走哪条路径。
- 它是不是只适合创业者
  最适合创业、商业、内容和个人项目判断。普通写作、排版、图片生成不是它的主场。
- 它说话会不会比较直接
  会。它的风格偏诊断，不是情绪安慰工具。
- `dbs-action` 能不能替代心理咨询
  不能。它只能帮助你做行动卡点的自我观察，不是心理咨询、医疗或治疗建议。
- 可以商用或二次包装吗
  请先阅读上游许可证。该项目采用 `CC BY-NC 4.0`，商业用途需要联系作者授权。

<h2 id="references">参考</h2>

- 官方仓库：<https://github.com/dontbesilent2025/dbskill>
- 作者：dontbesilent
- 许可证：`CC BY-NC 4.0`
