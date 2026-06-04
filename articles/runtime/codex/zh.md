---
title: Codex
slug: codex
order: 1
summary: 先认识 Codex，再准备 API Key，完成一键安装，然后直接开始用。
section: runtime
section_title: Runtime
section_order: 10
---

# Codex

如果你想在本地直接让模型帮你读项目、改代码、执行命令，这页就是最短路径。

对第一次接触这类工具的人来说，先把链路跑通最重要。不要先去研究配置文件，也不用先学一堆终端命令。

<h2 id="what-is-codex">Codex 是什么</h2>

- `Codex` 是一个面向代码工作的终端 runtime / agent
- 它可以读项目、改文件、执行命令，也可以直接回答代码问题
- 在 SorryCode 里，你要做的是把它接到 `{{API_BASE_URL}}`，再填入你自己的 API Key

第一次接入时，不需要先理解 `config.toml`、`auth.json` 或各种环境变量。先走一键安装就够了。

参考：[OpenAI Codex 官方仓库](https://github.com/openai/codex)

> 小白先记住：`Codex` 是 runtime，不是模型。它默认适合 GPT / OpenAI-compatible 路径。不要把 Claude 模型随手塞进 Codex；如果你不确定，先看 [Platform / 工具不是模型](/docs/concepts/tools-models-platform)。

<h2 id="prepare-api-key">先准备 API Key</h2>

一键安装会在流程里要求你输入 API Key，所以开始之前先做这一步：

1. 登录 SorryCode 控制台
2. 在控制台里找到 `API 密钥`
3. 如果还没有，就创建一个新的 `sk-...`
4. 把它先留在手边，安装时会马上用到

快速入口是 `https://sorrycode.com/keys`，但更重要的是记住它在控制台里的位置。

如果你还没做这一步，可以先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

如果你也准备使用 Claude Code，建议另外创建一把 API Key 给 Claude Code。两把 key 仍然消耗同一份余额，但记录、分组和限额可以分开管理。

<h2 id="one-click-install">一键安装</h2>

这是默认主路径。安装器会把 `Codex` 接到 `{{API_BASE_URL}}`，写好本地配置。安装后建议用 `Codex App` 打开项目。

### macOS / Linux

一键安装会自动处理 Codex 主安装需要的依赖。macOS 会准备 `Node.js 22 LTS` 和 `Codex CLI`，不要求你先学会 Homebrew 或 Git。

先打开终端：按住 `Command` + `空格`，输入 `Terminal`，按回车。

然后复制下面这整段命令，回到终端输入窗口，按 `Command` + `V` 粘贴，再按一次回车。

```bash
curl -fsSL -o /tmp/sorrycode-codex.sh {{INSTALL_SH_URL}} && bash /tmp/sorrycode-codex.sh --base-url "{{API_BASE_URL}}" --source sorrycode-docs
```

### Windows

按 `Win` 键，输入 `PowerShell` 或 `Terminal`，打开后直接粘贴这一条。如果你不知道 PowerShell 是什么，先看 [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)。

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-codex.bat {{INSTALL_BAT_URL}} && %TEMP%\sorrycode-codex.bat --base-url {{API_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>安装器会做什么</summary>

- 检查 `Node.js / npm`
- 安装 `Codex CLI`
- 写入 `~/.codex/config.toml`
- 写入 `~/.codex/auth.json`
- 做一次最小连通性检查
- Windows 只对这次安装进程使用 `ExecutionPolicy Bypass`，不会永久修改你的 PowerShell 策略

</details>

安装器会阻塞到你填完 `sk-...` 为止。

如果最后看到“连通性检查失败”，不代表安装一定失败。更常见的原因是余额、权限或网络还没准备好。本地安装和配置写入只要完成了，下一步还是可以继续。

<h2 id="start-codex">安装后怎么开始用</h2>

小白默认用 `Codex App`。

直接按这个顺序来：

1. 先完成本页的一键安装
2. 打开 Codex App 官方页面：<https://developers.openai.com/codex/app>
3. 下载并安装 `Codex App`
4. 打开 `Codex App`
5. 选择你要操作的项目文件夹
6. 输入第一句话

如果你更想在可视化编辑器里看项目文件和改动，也可以继续看 [工具 / VS Code](/docs/tools/vscode)。

如果你打开 Codex App 后发现插件入口是灰色的，或者 `/plugins` 找不到 Chrome、Computer Use、Browser、HyperFrames，继续看 [Codex App 插件配置](/docs/runtime/codex-plugins)。

<h2 id="cli-fallback">备用：继续用终端</h2>

如果你不用 `Codex App`，也可以自己在终端进入项目目录，再运行 Codex 命令。

进阶用户可以记住三个命令：

```bash
codex
```

新开一个 Codex 会话。

```bash
codex resume
```

打开可恢复会话列表。

```bash
codex resume --last
```

直接恢复最近一次会话。

如果 Codex 还没内置最新发布的模型名，可以手动指定模型启动：

```bash
codex -m gpt-5.5
```

这里的 `gpt-5.5` 只是示例。实际可用模型以 [Platform / 工具不是模型](/docs/concepts/tools-models-platform) 和控制台开放情况为准。

<h2 id="first-prompt">第一句可以说什么</h2>

第一次不要上来就让它大改项目，先让它看清楚项目入口：

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

<h2 id="install-skills-with-agent">下一步：把 Skills 交给 Codex 管理</h2>

Codex 跑起来以后，不用自己研究 `npx`、`Git` 或 `Homebrew`。把下面这段话复制给 Codex，让它读取当前 SorryCode Skills 文档，帮你准备环境，并按你的目标安装、查看或卸载需要的 skills：

```text
请阅读 SorryCode 当前 Skills 入口：https://sorrycode.com/docs/skills/featured-skills.md?locale=zh。我的 Mac 默认什么环境都没有，请你先检查并准备必要环境，然后根据当前 Skills 文档里的分类、推荐顺序和我的使用目标，判断并安装适合我的 skills。不要使用固定旧清单；请读取当前文档后再决定。安装、查看或卸载前先告诉我你要做什么；安装后验证 Codex 能识别这些 skills；卸载前先用 npx skills list --global 确认准确名称，并报告成功、失败和下一步。
```

<h2 id="manual-install">手动安装</h2>

只有在你想自己控每一步时，才需要这一段。

1. 先准备 [环境准备 / Node.js](/docs/environment/nodejs)
2. 安装 `Codex CLI`

```bash
npm install -g @openai/codex@latest
```

3. 写入 `~/.codex/config.toml`

```toml
model_provider = "OpenAI"
model = "gpt-5.4"
review_model = "gpt-5.4"
model_reasoning_effort = "xhigh"
disable_response_storage = true
network_access = "enabled"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "{{API_BASE_URL}}"
wire_api = "responses"
requires_openai_auth = true
```

4. 写入 `~/.codex/auth.json`

```json
{
  "OPENAI_API_KEY": "你的 sk-..."
}
```

<h2 id="first-request">首条请求</h2>

如果你走的是一键安装，通常不用先手动打请求。

只有在这些场景下，再回头看 [Platform / 首条请求](/docs/platform/create-api-key)：

- 安装器最后的连通性检查失败了
- 你想先确认 `API Key + Base URL + 网络` 这三层都通了
- 你走的是手动安装

<h2 id="common-issues">常见问题</h2>

- 找不到 `node` 或 `npm`
  去看 [环境准备 / Node.js](/docs/environment/nodejs)
- macOS 安装时卡在 Apple 弹窗、Homebrew 或 Git
  去看 [环境准备 / Node.js](/docs/environment/nodejs#macos)
- `401 / 404 / 429`
  去看 [排障 / 常见问题](/docs/platform/create-api-key)
- 下载慢或安装超时
  去看 [环境准备 / Node.js](/docs/environment/nodejs#network)
- 不知道 API Key 去哪里建
  去看 [Platform / 创建 API Key](/docs/platform/create-api-key)
