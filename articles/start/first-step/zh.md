---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 创建 API Key、安装工作台、跑通第一个任务——三步完成 SorryCode 上手，10 分钟内让 AI 开始替你干活。
section: start
section_title: 开始使用
section_order: 1
---

# 第一次使用 SorryCode

这篇文章只做一件事：让你在 10 分钟内，从"没听说过 SorryCode"到"AI 帮你干完第一件活"。

<h2 id="before">开始之前</h2>

你需要一个 SorryCode 账号。如果没有，先去 [sorrycode.com](https://sorrycode.com) 注册。

SorryCode 是一个 API 平台。你在这里充值、创建密钥，然后把密钥交给 AI 工具，工具就能用你的余额调用模型。

简单理解：

```text
一份余额 + 按工具分开的 API Key + 多个 AI 工具入口
```

想知道适不适合你？[SorryCode 适合谁](/docs/platform/who-is-sorrycode-for)。想理解成本和定价？[AI 成本怎么计算](/docs/platform/ai-cost-basics)。

<h2 id="step-1">第 1 步：创建 API Key</h2>

API Key 是你的钥匙。没有它，工具进不了 SorryCode。

1. 打开 [sorrycode.com/keys](https://sorrycode.com/keys)
2. 点"创建 API Key"
3. 名称填你要用的工具，比如"Codex"或"Claude Code"
4. 分组选"默认分组"
5. 其他保持默认
6. 点创建，复制那个 `sk-...` 开头的字符串

**密钥只显示一次，现在复制保存好。**

建议 Codex 和 Claude Code 各创建一把。余额是同一份，但记录分开，方便管理和排障。

如果创建过程遇到问题，看[创建 API Key](/docs/platform/create-api-key)的详细说明。

<h2 id="step-2">第 2 步：安装工作台</h2>

工作台是 AI 在你电脑上干活的地方。它负责读文件、写文件、执行命令、调用工具。

**选哪个？**

```text
你主要用 GPT 模型 → 装 Codex
你主要用 Claude 模型 → 装 Claude Code
不确定 → 装 Codex，它是最简单的新手入口
```

**安装命令：**

打开终端（Mac 搜"Terminal"，Windows 搜"PowerShell"），复制粘贴，回车：

```bash
# macOS / Linux 装 Codex
curl -fsSL https://sorrycode.com/install/codex.sh | bash
```

```bash
# macOS / Linux 装 Claude Code
curl -fsSL https://sorrycode.com/install/claude-code.sh | bash
```

安装完按提示输入 API Key，工作台就接上了。

如果安装卡住了，看 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code) 的详细说明。Windows 用户先看 [Windows PowerShell](/docs/environment/windows-powershell)。

<h2 id="step-3">第 3 步：跑通第一个任务</h2>

装完了。现在让它干活。

不要一上来就让它改重要文件。先跑一个小任务验证一切正常。

**如果你有代码项目：**

在终端进入你的项目文件夹，启动工作台，复制这句话：

```text
先别改代码。看一下这个项目，告诉我它是做什么的，我应该先读哪些文件。
```

**如果你没有代码项目：**

在桌面建一个"AI 工作台"文件夹，在终端进入这个文件夹，启动工作台，复制这句话：

```text
帮我在当前文件夹里写一份个人介绍草稿。先问我 5 个必要问题，不要直接生成最终稿。
```

**如果你想生成图片：**

先装图片 Skill：

```bash
npx skills add linxiverse/sorrycode-image2 -g -y
```

然后说：

```text
请用 SorryCode Image2 生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。先检查 API Key，如果没设置就告诉我怎么设置。
```

任务跑通了？你已经比 90% 的人更会用了。

<h2 id="step-4">第 4 步：装对应的 Skill</h2>

Skill 是给工作台装的能力包。你需要什么能力，就装什么 Skill。

| 你想做什么 | 装哪个 | 命令 |
| --- | --- | --- |
| 处理 Word / Excel / PPT / PDF | 办公文档 | `npx skills add linxiverse/office-docs -g -y` |
| 做一页纸、简历、作品集、长文 | Kami | `npx skills add tw93/kami -g -y` |
| 生成图片、海报、封面 | Image2 | `npx skills add linxiverse/sorrycode-image2 -g -y` |
| 做网页 PPT | 藏师傅 PPT | `npx skills add op7418/guizang-ppt-skill -g -y` |

更多 Skill 看 [Skills 是什么](/docs/skills/featured-skills) 和 [创作与设计](/docs/skills/creation-design)。

<h2 id="what-next">接下来做什么</h2>

按你的目标走：

- 想系统性理解 AI 怎么用：[核心概念](/docs/concepts/what-is-ai)从头读
- 想把 AI 用得更深：[Agent 进阶](/docs/agent-infra/overview)学项目规则和上下文管理
- 想知道钱花在哪了：[AI 成本怎么计算](/docs/platform/ai-cost-basics)
- 遇到报错了：[Codex 常见问题](/docs/runtime/codex)或 [Claude Code 常见问题](/docs/runtime/claude-code)

<h2 id="remember">记住这些就够了</h2>

- API Key 是钥匙，创建后复制保存
- Codex / Claude Code 是工作台，一个命令装好
- Skill 是能力包，做什么任务装什么
- 先跑通一个小任务，比看完十篇教程有用
