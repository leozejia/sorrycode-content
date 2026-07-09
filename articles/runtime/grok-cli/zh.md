---
title: Grok
slug: grok-cli
order: 4
summary: 先认识 Grok，再准备 API Key，完成一键安装，然后直接开始用。
section: runtime
section_title: Runtime
section_order: 10
---

# Grok

如果你想在本地用 Grok 帮你读项目、改代码、执行命令，同时让请求走 SorryCode，这页就是最短路径。

对第一次接触这类工具的人来说，先把链路跑通最重要。不要先去研究配置文件，也不用先学一堆终端命令。

> **你走哪条路？**
>
> **→ 一键安装（推荐）：** 在 API Key 页面点 `接入工具` → 复制命令 → 粘贴到本机终端 → 完成。适合绝大多数人。
>
> **→ 手动安装：** 自己安装 Grok、写配置文件。适合想控每一步的进阶用户。
>
> 下面默认按一键安装展开。

<h2 id="what-is-grok">Grok 是什么</h2>

- `Grok` 是 xAI 提供的本地命令行 runtime / agent
- 它可以在终端里和你协作，读取项目、回答问题，也可以执行本地任务
- 在 SorryCode 里，你要做的是把它接到 `{{API_BASE_URL}}`，再填入你自己的 API Key

第一次接入时，不需要先理解 `~/.grok/config.toml` 或环境变量。先走一键安装就够了。

参考：[xAI Grok 官方安装器](https://x.ai/cli/install.sh)

> 小白先记住：`Grok` 是 runtime，不是模型。它默认适合 Grok / xAI-compatible 路径。不要把 GPT 或 Claude 模型随手塞进 Grok；如果你不确定，先看 [Platform / 工具不是模型](/docs/concepts/tools-models-platform)。

<h2 id="prepare-api-key">先准备 API Key</h2>

一键安装命令需要绑定你的 API Key，所以开始之前先做这一步：

1. 登录 SorryCode 控制台
2. 在控制台里找到 `API 密钥`
3. 如果还没有，就创建一个新的 `sk-...`
4. 确认这把 key 可以使用 Grok 分组
5. 回到列表，准备点击这把 key 右侧的 `接入工具`

快速入口是 `https://sorrycode.com/keys`，但更重要的是记住它在控制台里的位置。

如果你还没做这一步，可以先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

如果你也准备使用 Codex 或 Claude Code，建议另外创建一把 API Key 给它们。多把 key 仍然消耗同一份余额，但记录、分组和限额可以分开管理。

<h2 id="one-click-install">⚡ 一键安装（推荐）</h2>

这是默认主路径。控制台会用当前 API Key 生成一条安装命令。你把这条命令粘贴到自己电脑的终端里运行，安装器会把 `Grok` 接到 `{{API_BASE_URL}}`，写好本地配置，并把默认模型设为 `grok-4.5`。安装完成后，重新打开终端运行 `grok` 就可以开始用。

### 第一步：在控制台复制命令

1. 打开 `https://sorrycode.com/keys`
2. 找到给 Grok 准备的那把 API Key
3. 点击右侧的 `接入工具`
4. 选择 `Grok`
5. 选择你的系统
6. 点击 `复制`

弹窗里复制出来的是完整安装命令，已经带着当前 API Key。

### 第二步：粘贴到你电脑的终端

- Mac：按住 `Command + 空格`，输入 `Terminal`，回车
- Windows：按 `Win` 键，输入 `PowerShell` 或 `Terminal`，回车

打开终端后，把刚复制的整条命令粘贴进去，再按一次回车。

一键安装会调用 xAI 官方安装器安装 Grok，然后写入 `~/.grok/config.toml` 和 `SORRYCODE_API_KEY`。Windows 会使用适合 Windows 的安装脚本。如果你不知道 PowerShell 是什么，先看 [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)。

### 备用：手动复制通用命令

如果你暂时打不开 `接入工具` 弹窗，也可以用下面的通用命令。它不会自动带入你的 API Key，安装时会停下来让你粘贴 `sk-...`。

macOS / Linux：

```bash
curl -fsSL https://sorrycode.com/install/sorrycode-grok.sh | bash -s -- --base-url "{{API_BASE_URL}}" --source sorrycode-docs
```

Windows：

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-grok.bat https://sorrycode.com/install/sorrycode-grok.bat && %TEMP%\sorrycode-grok.bat --base-url {{API_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>安装器会做什么</summary>

- 检查本机是否已有 `grok`
- 如果没有，调用 xAI 官方安装器安装 Grok
- 备份已有的 `~/.grok/config.toml`
- 写入 SorryCode 的 `~/.grok/config.toml`
- 把默认模型设为 `grok-4.5`
- 写入 `SORRYCODE_API_KEY`
- Windows 只对这次安装进程使用 `ExecutionPolicy Bypass`，不会永久修改你的 PowerShell 策略

</details>

如果你从 `接入工具` 复制命令，安装器通常不需要再问你 API Key。如果你用的是上面的通用命令，安装器会阻塞到你填完 `sk-...` 为止。

如果安装结束后当前终端还找不到 `grok`，先关闭终端再重新打开一次。很多安装器会把命令写进新的 shell 路径里，旧窗口不一定能马上看到。

<h2 id="start-grok">安装后怎么开始用</h2>

进入你要操作的项目目录，然后运行：

```bash
grok
```

如果你保留了多个 Grok 配置，也可以显式指定 SorryCode 这一路：

```bash
grok -m sorrycode-grok
```

如果你更想在可视化编辑器里看项目文件和改动，也可以继续看 [工具 / VS Code](/docs/tools/vscode)。

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

<h2 id="manual-install">手动安装（进阶）</h2>

只有在你想自己控每一步时，才需要这一段。

1. 安装 Grok

macOS / Linux / WSL：

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Windows PowerShell：

```powershell
irm https://x.ai/cli/install.ps1 | iex
```

2. 写入 `~/.grok/config.toml`

macOS / Linux / WSL：

```bash
mkdir -p ~/.grok
cat > ~/.grok/config.toml <<'EOF'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "{{API_BASE_URL}}"
name = "SorryCode Grok"
env_key = "SORRYCODE_API_KEY"

[models]
default = "sorrycode-grok"
EOF
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.grok" | Out-Null

$config = @'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "{{API_BASE_URL}}"
name = "SorryCode Grok"
env_key = "SORRYCODE_API_KEY"

[models]
default = "sorrycode-grok"
'@

[System.IO.File]::WriteAllText(
  "$env:USERPROFILE\.grok\config.toml",
  $config,
  [System.Text.UTF8Encoding]::new($false)
)
```

3. 设置 API Key

macOS / Linux / WSL：

```bash
export SORRYCODE_API_KEY="你的 sk-..."
grok
```

Windows PowerShell：

```powershell
[System.Environment]::SetEnvironmentVariable("SORRYCODE_API_KEY", "你的 sk-...", "User")
$env:SORRYCODE_API_KEY = "你的 sk-..."
grok
```

这里有两个细节要记住：

- `base_url` 填 `{{API_BASE_URL}}`，不是 xAI 官方 API 地址
- `SORRYCODE_API_KEY` 填 SorryCode 的 `sk-...`，不要填 xAI 账号凭据

<h2 id="first-request">首条请求</h2>

如果你走的是一键安装，通常不用先手动打请求。

只有在这些场景下，再回头看 [Platform / 首条请求](/docs/platform/first-request)：

- 安装后 `grok` 无法正常回应
- 你想先确认 `API Key + Base URL + 网络` 这三层都通了
- 你走的是手动安装

<h2 id="common-issues">常见问题</h2>

- 找不到 `grok`
  关闭终端后重新打开，再运行 `grok`
- `401 / 404 / 429`
  去看 [排障 / 常见问题](/docs/troubleshoot/common-errors)
- 不知道 API Key 去哪里建
  去看 [Platform / 创建 API Key](/docs/platform/create-api-key)
- 不确定 Grok、Codex、Claude Code 应该怎么选
  去看 [Platform / 工具不是模型](/docs/concepts/tools-models-platform)
