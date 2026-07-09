---
title: 第一次使用 SorryCode
slug: first-step
order: 1
summary: 创建 API Key、选择并安装工作台、跑通第一个任务——三步完成 SorryCode 上手，10 分钟内让 AI 开始替你干活。
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

如果创建过程遇到问题，看 [创建 API Key](/docs/platform/create-api-key) 的详细说明。

<h2 id="step-2">第 2 步：选择并安装工作台</h2>

工作台是 AI 在你电脑上干活的地方。它负责读文件、写文件、执行命令、调用工具。

### 选哪个工作台？

SorryCode 支持两个主流工作台：

| 工作台 | 适合谁 | 去哪里 |
|--------|--------|--------|
| **Codex** | 主要用 GPT 模型，或不确定用什么 | [安装 Codex](/docs/runtime/codex) |
| **Claude Code** | 主要用 Claude 模型 | [安装 Claude Code](/docs/runtime/claude-code) |

**不确定？装 Codex。** 它是最简单的新手入口，有可视化 App，也支持命令行。

### 快速安装

两个工作台都支持一键安装：

1. 回到 `https://sorrycode.com/keys`
2. 找到你刚创建的那把 key，点右侧的 `接入工具`
3. 在弹窗里选择 `Codex` 或 `Claude Code`，再选择你的系统
4. 复制出来的命令已经带着当前 API Key

然后打开你电脑的终端：

- Mac：按 `Command + 空格`，输入 `Terminal`，回车
- Windows：按 `Win`，输入 `PowerShell` 或 `Terminal`，回车

把刚复制的整条命令粘贴进去，按回车。

**安装完成后：**

- **Codex 用户：** 下载并打开 [Codex App](https://developers.openai.com/codex/app)，或在终端输入 `codex` 命令
- **Claude Code 用户：** 在终端输入 `claude` 命令启动

### 详细安装和使用指南

如果一键安装遇到问题，或想了解更多使用方法：

- **Codex 用户：** 看 [Runtime / Codex](/docs/runtime/codex) 
  - 包含：安装、启动 Codex App、命令行使用、插件配置
- **Claude Code 用户：** 看 [Runtime / Claude Code](/docs/runtime/claude-code)
  - 包含：安装、命令行使用、插件配置

**Windows 用户注意：** 如果安装时提示权限问题，先看 [Windows PowerShell](/docs/environment/windows-powershell)。

<h2 id="step-3">第 3 步：启动工作台并跑通第一个任务</h2>

装完了。现在让它干活。

### 启动工作台

**Codex 用户：**

方式 1（推荐新手）：
1. 打开 Codex App
2. 选择你要操作的项目文件夹
3. 在输入框输入任务

方式 2（命令行）：
1. 在终端进入项目文件夹
2. 输入 `codex` 启动
3. 输入任务

**Claude Code 用户：**

1. 在终端进入项目文件夹
2. 输入 `claude` 启动
3. 输入任务

### 第一个任务

不要一上来就让它改重要文件。先跑一个小任务验证一切正常。

**如果你有代码项目：**

```text
先别改代码。看一下这个项目，告诉我它是做什么的，我应该先读哪些文件。
```

**如果你没有代码项目：**

在桌面建一个"AI 工作台"文件夹，进入这个文件夹后启动工作台，然后说：

```text
帮我在当前文件夹里写一份个人介绍草稿。先问我 5 个必要问题，不要直接生成最终稿。
```

**如果你想生成图片：**

先装图片 Skill：

```bash
npx skills add linxiverse/sorrycode-image2 -g -y
```

然后重启工作台，说：

```text
请用 SorryCode Image2 生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。先检查 API Key，如果没设置就告诉我怎么设置。
```

**任务跑通了？** 你已经比 90% 的人更会用了。

<h2 id="step-4">第 4 步：按任务选择 Skill</h2>

Skill 是给工作台装的能力包。不同 skill 的安装方式会随 Codex、Claude Code 和上游仓库变化；新手页不写固定命令，避免复制到过时地址。

| 你想做什么 | 从这里开始 |
| --- | --- |
| 处理 Word / Excel / PPT / PDF | [办公文档](/docs/skills/office-docs) |
| 做一页纸、简历、作品集、长文 | [Kami](/docs/skills/kami) |
| 生成图片、海报、封面 | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| 做网页 PPT | [藏师傅的 PPT Skill](/docs/skills/magazine-web-ppt) |

进入对应页面后，按你正在用的工作台选择 Codex 或 Claude Code 的安装命令。安装 Skill 后需要重启工作台。

更多 Skill 看 [Skills / 精选 Skills](/docs/skills/featured-skills)。

<h2 id="common-issues">常见问题</h2>

### 安装后找不到命令

**Codex：** 
- 检查是否已经安装：`which codex`
- 如果没有，重新运行一键安装命令
- 或者直接用 Codex App（不需要命令行）

**Claude Code：**
- 检查是否已经安装：`which claude`
- 如果没有，重新运行一键安装命令

### API Key 报错

检查：
1. 是否正确复制了 `sk-...` 开头的完整密钥
2. 账号是否有可用余额
3. 密钥是否在安装时正确配置

详细排障看 [Codex 常见问题](/docs/runtime/codex#common-issues) 或 [Claude Code 常见问题](/docs/runtime/claude-code#common-issues)。

### 不知道用 Codex 还是 Claude Code

- **用 GPT 模型（如 GPT-4、o1）：** 用 Codex
- **用 Claude 模型（如 Claude 3.5 Sonnet）：** 用 Claude Code
- **不确定：** 装 Codex，它更适合新手

两个都装也可以，它们可以共存。

<h2 id="what-next">接下来做什么</h2>

按你的目标走：

### 想深入了解工作台

- Codex 用户：[Runtime / Codex](/docs/runtime/codex)
  - 学习 Codex App 使用、插件管理、命令行技巧
- Claude Code 用户：[Runtime / Claude Code](/docs/runtime/claude-code)
  - 学习命令行使用、插件管理、高级功能

### 想了解 Plugins 和 Skills

- [Plugins 和 Skills 有什么区别](/docs/runtime/plugins-vs-skills)
  - Plugins 给工具，Skills 教方法
- [Skills / 精选 Skills](/docs/skills/featured-skills)
  - 浏览所有可用的 Skills

### 想系统学习

- [核心概念 / AI 到底是什么](/docs/concepts/what-is-ai) - 从头理解 AI
- [让 AI 记住你的要求](/docs/agent-memory/overview) - 长期上下文管理
- [AI 成本怎么计算](/docs/platform/ai-cost-basics) - 理解计费

### 遇到问题

- [Codex 文档](/docs/runtime/codex) - Codex 完整指南
- [Claude Code 文档](/docs/runtime/claude-code) - Claude Code 完整指南
- [排障 / 常见错误](/docs/troubleshoot/common-errors) - 通用排障

<h2 id="remember">记住这些就够了</h2>

- **API Key** 是钥匙，创建后复制保存
- **Codex / Claude Code** 是工作台，选一个装
- **Codex App** 或 `codex` / `claude` 命令启动工作台
- **Skill** 是能力包，做什么任务装什么
- 先跑通一个小任务，比看完十篇教程有用

**卡住了？** 直接看对应工作台的详细文档：
- [Codex 完整指南](/docs/runtime/codex)
- [Claude Code 完整指南](/docs/runtime/claude-code)
