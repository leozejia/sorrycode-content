---
title: Pi + DeepSeek
slug: pi-deepseek
order: 1
summary: 安装 Pi Coding Agent，接入 SorryCode DeepSeek 分组，并完成文本和文件工具验证。
section: runtime
section_title: 模型与工作台
section_order: 10
group: deepseek
group_title: DeepSeek
group_order: 23
---

# Pi + DeepSeek

Pi 是 [earendil-works/pi](https://github.com/earendil-works/pi) 提供的终端 Coding Agent，可以读项目、改文件和执行命令。这页把 Pi 接到 SorryCode，并使用分组内的 DeepSeek 模型完成第一次 Agent 任务。

这里说的是 [pi.dev](https://pi.dev/) 对应的 Pi，不是其他同名项目。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="prepare-key">准备 API Key</h2>

Pi 通过 SorryCode 的 OpenAI-compatible Responses API 调用 DeepSeek。在 [SorryCode API Key 页面](https://sorrycode.com/keys) 选择一把所属分组支持 DeepSeek 的 Key。已有符合条件的 Key 可以直接复用；只有需要分开统计用量、设置限额或轮换凭证时，才需要新建一把。

先查询这把 Key 实际开放的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 DeepSeek API Key>"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <你的 DeepSeek API Key>"
```

后续配置必须使用返回结果里的准确模型 ID。当前经过验证的 ID 是 `deepseek-v4-flash` 和 `deepseek-v4-pro`，实际可用范围以这把 Key 的返回结果为准。

<h2 id="install">安装 Pi</h2>

Pi 当前要求 Node.js `22.19.0` 或更高版本。先检查：

```bash
node --version
npm --version
```

如果命令不存在或版本过低，先阅读 [Node.js](/docs/environment/nodejs)。环境准备好后，使用 Pi 官方包安装：

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

macOS、Linux 和 Windows 都使用这条 npm 命令。安装后确认版本：

```bash
pi --version
```

<h2 id="configure">配置 SorryCode provider</h2>

Pi 的自定义模型配置文件是：

- macOS / Linux：`~/.pi/agent/models.json`
- Windows：`%USERPROFILE%\.pi\agent\models.json`

macOS / Linux 可以先创建目录并打开文件：

```bash
mkdir -p ~/.pi/agent
nano ~/.pi/agent/models.json
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME\.pi\agent" | Out-Null
notepad "$HOME\.pi\agent\models.json"
```

如果文件里已有其他 provider，把下面的 `sorrycode` 合并到 `providers` 中，不要覆盖原有配置：

```json
{
  "providers": {
    "sorrycode": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "deepseek-v4-flash",
          "name": "DeepSeek V4 Flash via SorryCode",
          "reasoning": true
        },
        {
          "id": "deepseek-v4-pro",
          "name": "DeepSeek V4 Pro via SorryCode",
          "reasoning": true
        }
      ]
    }
  }
}
```

如果当前 Key 只返回其中一个模型，只保留对应条目。

<h2 id="login">保存 API Key</h2>

运行 Pi：

```bash
pi
```

进入界面后输入 `/login`，选择 `sorrycode`，再粘贴这把 DeepSeek 分组 Key。Pi 会把凭证保存到自己的认证文件中，不需要设置环境变量，也不要把 Key 写进 `models.json`。

然后输入 `/model`，选择 `sorrycode/deepseek-v4-flash`。要使用其他模型时，选择当前 Key 实际开放的对应 ID。

<h2 id="verify">验证文本和工具调用</h2>

先验证最小文本响应：

```bash
pi --provider sorrycode --model deepseek-v4-flash --no-tools --no-session -p "Reply with PI_SORRYCODE_OK only."
```

看到 `PI_SORRYCODE_OK` 后，在一个空测试目录中验证文件工具：

```bash
mkdir pi-sorrycode-test
cd pi-sorrycode-test
pi --provider sorrycode --model deepseek-v4-flash --no-session -p "Create pi-check.txt containing PI_TOOL_OK and a final newline. Do not modify other files."
```

任务结束后找到 `pi-check.txt`，并确认内容是 `PI_TOOL_OK`。这说明模型连接和 Agent 工具调用都已经可用。

<h2 id="common-issues">常见问题</h2>

- `pi` 命令不存在：关闭并重新打开终端，再检查 npm 全局命令目录是否在 `PATH` 中
- `/login` 中没有 `sorrycode`：先保存 `models.json`，再重新启动 Pi
- `/model` 中没有 DeepSeek：检查 JSON 格式、认证状态和 Key 所属分组
- `401`：Key 不完整、已失效，或保存的不是当前 DeepSeek 分组 Key
- `404` 或 model not found：重新查询 `/v1/models`，使用返回结果中的准确 ID
- 能回复但不能创建文件：确认使用经过验证的模型，并检查当前任务是否允许 `write` 工具
- Windows 阻止 `pi.ps1`：阅读 [Windows PowerShell](/docs/environment/windows-powershell)

本页验证基线为 Pi `0.84.1`、`deepseek-v4-flash`，最小文本和 `write` 工具调用均已通过。

参考：[Pi 官网](https://pi.dev/)、[Pi 官方仓库](https://github.com/earendil-works/pi)、[Pi 自定义模型文档](https://pi.dev/docs/latest/models)。
