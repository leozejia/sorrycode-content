---
title: Grok Build
slug: grok-build
order: 4
summary: 安装 Grok Build，并用自定义模型配置接到 SorryCode。
section: runtime
section_title: Runtime
section_order: 10
---

# Grok Build

如果你想用 xAI 的 `Grok Build` 在本地跑 agent，同时让请求走 SorryCode，这页就是最短路径。

当前 SorryCode 控制台的 `接入工具` 可能还没有 Grok Build 专用入口。先按本文手动配置：安装官方 CLI，写入自定义模型配置，再用 SorryCode API Key 启动。

<h2 id="prepare-api-key">先准备 API Key</h2>

1. 登录 SorryCode 控制台
2. 在控制台里找到 `API 密钥`
3. 如果还没有，就创建一个新的 `sk-...`
4. 确认这把 key 可以使用 Grok 分组

快速入口是 `https://sorrycode.com/keys`。

如果你还不知道怎么创建 API Key，先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="install">安装 Grok Build</h2>

macOS / Linux / WSL：

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Windows PowerShell：

```powershell
irm https://x.ai/cli/install.ps1 | iex
```

安装完成后，重新打开终端，确认 `grok` 命令可用。

<h2 id="connect-sorrycode">接到 SorryCode</h2>

macOS / Linux / WSL：

```bash
mkdir -p ~/.grok
cat > ~/.grok/config.toml <<'EOF'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "https://api.sorrycode.com/v1"
name = "SorryCode Grok"
env_key = "SORRYCODE_API_KEY"

[models]
default = "sorrycode-grok"
EOF

export SORRYCODE_API_KEY="sk-your-sorrycode-key"
grok
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.grok" | Out-Null

$config = @'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "https://api.sorrycode.com/v1"
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

$env:SORRYCODE_API_KEY = "sk-your-sorrycode-key"
grok
```

把 `sk-your-sorrycode-key` 换成你自己的 SorryCode API Key。

<h2 id="start">启动方式</h2>

如果已经把 `sorrycode-grok` 写成默认模型，直接运行：

```bash
grok
```

如果你还保留了其他 Grok Build 配置，也可以显式指定：

```bash
grok -m sorrycode-grok
```

<h2 id="notes">注意</h2>

- `base_url` 填 `https://api.sorrycode.com/v1`，不是 xAI 官方 API 地址。
- `SORRYCODE_API_KEY` 填 SorryCode 的 `sk-...`，不要填 xAI 账号凭据。
- `model` 固定写 `grok-4.5`。
- 不要走 xAI 浏览器登录路径来接 SorryCode。SorryCode 走的是 API Key 和自定义模型配置。
