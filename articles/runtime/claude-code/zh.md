---
title: Claude Code
slug: claude-code
order: 2
summary: 先认识 Claude Code，再准备 API Key，完成一键安装，然后直接开始用。
section: runtime
section_title: Runtime
section_order: 10
---

# Claude Code

如果你想在本地直接让模型帮你读项目、改代码、执行命令，这页就是最短路径。

对第一次接触这类工具的人来说，先把链路跑通最重要。不要先去研究配置文件，也不用先学一堆终端命令。

<h2 id="what-is-claude-code">Claude Code 是什么</h2>

- `Claude Code` 是一个面向代码工作的终端 runtime / agent
- 它可以读项目、改文件、执行命令，也可以直接回答代码问题
- 在 SorryCode 里，你要做的是把它接到 `{{ANTHROPIC_BASE_URL}}`，再填入你自己的 API Key

第一次接入时，不需要先理解 `settings.json` 或各种环境变量。先走一键安装就够了。

参考：[Claude Code 官方文档](https://code.claude.com/docs/en/overview)

> 小白先记住：`Claude Code` 是 runtime，不是模型。它默认适合 Claude / Anthropic-compatible 路径。不要为了追新 GPT 模型就把 `gpt-5.4` 直接塞进 Claude Code；缓存命中和 API 消耗可能很不划算。先看 [Platform / 工具不是模型](/docs/platform/tools-and-models)。

<h2 id="prepare-api-key">先准备 API Key</h2>

一键安装会在流程里要求你输入 API Key，所以开始之前先做这一步：

1. 登录 SorryCode 控制台
2. 在控制台里找到 `API 密钥`
3. 如果还没有，就创建一个新的 `sk-...`
4. 把它先留在手边，安装时会马上用到

快速入口是 `https://sorrycode.com/keys`，但更重要的是记住它在控制台里的位置。

如果你还没做这一步，可以先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="one-click-install">一键安装</h2>

这是默认主路径。安装器会把 `Claude Code` 接到 `{{ANTHROPIC_BASE_URL}}`，写好本地配置。安装后可以用 `Claude Desktop` 或你熟悉的开发工具打开。

### macOS / Linux

一键安装会自动处理 Claude Code 主安装需要的依赖。macOS 会准备 `Node.js 22 LTS` 和 `Claude Code`，不要求你先学会 Homebrew 或 Git。

先打开终端：按住 `Command` + `空格`，输入 `Terminal`，按回车。

然后复制下面这整段命令，回到终端输入窗口，按 `Command` + `V` 粘贴，再按一次回车。

```bash
curl -fsSL -o /tmp/sorrycode-claude.sh {{INSTALL_CLAUDE_SH_URL}} && bash /tmp/sorrycode-claude.sh --base-url "{{ANTHROPIC_BASE_URL}}" --source sorrycode-docs
```

### Windows

按 `Win` 键，输入 `PowerShell` 或 `Terminal`，打开后直接粘贴这一条。如果你不知道 PowerShell 是什么，先看 [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)。

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-claude.bat {{INSTALL_CLAUDE_BAT_URL}} && %TEMP%\sorrycode-claude.bat --base-url {{ANTHROPIC_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>安装器会做什么</summary>

- Windows 检查 `Git for Windows`
- 安装 `Claude Code`
- 写入 `~/.claude/settings.json`
- 写入 API Key
- 做一次最小连通性检查
- Windows 只对这次安装进程使用 `ExecutionPolicy Bypass`，不会永久修改你的 PowerShell 策略

</details>

安装器会阻塞到你填完 `sk-...` 为止。

如果最后看到“连通性检查失败”，不代表安装一定失败。更常见的原因是余额、权限或网络还没准备好。本地安装和配置写入只要完成了，下一步还是可以继续。

<h2 id="start-claude-code">安装后怎么开始用</h2>

小白优先安装 `Claude Desktop`，获得更图形化的入口。

`Claude Desktop` 官方下载入口：<https://claude.com/download>

如果你想在 Claude Desktop 里做类似开发工具配置，也可以做到。这里不展开第三方配置细节；需要协助时请联系 SorryCode 客服。

如果你暂时不用桌面应用，也可以在终端进入项目目录后运行 `claude`。

如果你更想在可视化编辑器里看项目文件和改动，也可以继续看 [工具 / VS Code](/docs/tools/vscode)。

<h2 id="first-prompt">第一句可以说什么</h2>

第一次不要上来就让它大改项目，先给一条很稳的指令：

```text
先看一下这个项目的目录结构，再告诉我应该先读哪些文件。
```

或者：

```text
先别改代码，先解释这个项目是做什么的，以及入口在哪里。
```

这样最容易先确认两件事：

- 它已经进到了对的项目目录
- 它能正常读项目并给你回应

<h2 id="install-skills-with-agent">下一步：把 Skills 交给 Claude Code 安装</h2>

Claude Code 跑起来以后，不用自己研究 `npx`、`Git` 或 `Homebrew`。把下面这段话复制给 Claude Code，让它读取当前 SorryCode Skills 文档，帮你准备环境和安装需要的 skills：

```text
请阅读 SorryCode 当前 Skills 入口：https://sorrycode.com/docs/skills/featured-skills.md?locale=zh。我的 Mac 默认什么环境都没有，请你先检查并准备必要环境，然后根据当前 Skills 文档里的分类、推荐顺序和我的使用目标，判断并安装适合我的 skills。不要使用固定旧清单；请读取当前文档后再决定。安装前告诉我你要做什么，安装后验证 Claude Code 能识别这些 skills，并报告成功、失败和下一步。
```

<h2 id="manual-install">手动安装</h2>

只有在你想自己控每一步时，才需要这一段。

1. 先准备 [环境准备 / Node.js](/docs/environment/nodejs)
2. 安装 `Claude Code`

```bash
npm install -g @anthropic-ai/claude-code@latest
```

3. 写入 `~/.claude/settings.json`

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "{{ANTHROPIC_BASE_URL}}",
    "ANTHROPIC_AUTH_TOKEN": "你的 sk-...",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0"
  }
}
```

4. 如果你是原生 Windows，且 `Claude Code` 找不到 `Git Bash`，再补一条：

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

这里有一个细节要记住：

- `ANTHROPIC_AUTH_TOKEN` 只是 Claude Code 的字段名
- 里面填的仍然是你在 SorryCode 创建的 API Key，也就是 `sk-...`

<h2 id="first-request">首条请求</h2>

如果你走的是一键安装，通常不用先手动打请求。

只有在这些场景下，再回头看 [Platform / 首条请求](/docs/platform/first-request)：

- 安装器最后的连通性检查失败了
- 你想先确认 `API Key + Base URL + 网络` 这三层都通了
- 你走的是手动安装

<h2 id="common-issues">常见问题</h2>

- 找不到 `node` 或 `npm`
  去看 [环境准备 / Node.js](/docs/environment/nodejs)
- macOS 安装时卡在 Apple 弹窗、Homebrew 或 Git
  去看 [环境准备 / Node.js](/docs/environment/nodejs#macos)
- 原生 Windows 下找不到 `Git Bash`
  把 `CLAUDE_CODE_GIT_BASH_PATH` 写进 `~/.claude/settings.json`
- `401 / 404 / 429`
  去看 [排障 / 常见问题](/docs/troubleshoot/common-errors)
- 下载慢或安装超时
  去看 [环境准备 / Node.js](/docs/environment/nodejs#network)
- 不知道 API Key 去哪里建
  去看 [Platform / 创建 API Key](/docs/platform/create-api-key)
