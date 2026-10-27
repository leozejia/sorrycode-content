---
title: Node.js
slug: nodejs
order: 1
summary: 只有安装或使用某个 Skill 明确需要 Node.js 时，才准备这个环境。
section: environment
section_title: 环境准备
section_order: 40
---

# Node.js

Magpie 和桌面 Agent 不要求你先安装 Node.js。只有某个 Skill 或工具明确需要 `node`、`npm`、`npx` 时，再按这页准备。

已经能使用 Agent 时，也可以把需要安装的 Skill 文档发给它，让它先检查环境并说明要做的改动。

<h2 id="why-nodejs">先检查是否已经安装</h2>

在终端运行：

```bash
node --version
npm --version
npx --version
```

都能显示版本号，通常就不需要重复安装。具体版本要求以正在安装的工具说明为准。

<h2 id="macos">macOS</h2>

打开 [Node.js 官网下载页](https://nodejs.org/zh-cn/download)，选择当前 LTS 的 macOS 安装包，完成安装后重新打开终端，再检查版本。

不需要为了这一步额外安装 Homebrew。如果你已经用其他方式管理 Node.js，先让 Agent 检查现有环境，不要叠加多套安装。

<h2 id="windows">Windows</h2>

在 [Node.js 官网下载页](https://nodejs.org/zh-cn/download)选择当前 LTS 的 Windows 安装包，按默认选项安装。完成后关闭并重新打开 PowerShell，再检查版本。

<h2 id="powershell">PowerShell 报错</h2>

如果 `npm` 提示脚本执行策略限制，先看 [Windows PowerShell](/docs/environment/windows-powershell#execution-policy)，不要永久放开系统策略。

<h2 id="network">下载慢或网络错误</h2>

先确认能打开工具的官方下载页和 GitHub。切换网络或检查代理后再试，不要把网络超时当成 API Key 错误，也不要反复安装不同版本。

仍然失败时，保留完整报错，把目标工具文档和错误一起交给 Agent 判断。

<h2 id="next">下一步</h2>

回到你要安装的 [Skills](/docs/skills/featured-skills)。如果还没接入 Agent，先看[用 Magpie 配置 SorryCode](/docs/agents/magpie)。
