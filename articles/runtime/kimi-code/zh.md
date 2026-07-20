---
title: Kimi Code
slug: kimi-code
order: 1
summary: 为 Kimi Code 配置 SorryCode Kimi 分组 Key，使用 K3 或分组内的其他 Kimi 模型。
section: runtime
section_title: 模型与工作台
section_order: 10
group: kimi
group_title: Kimi
group_order: 25
---

# Kimi Code

Kimi Code 是一个运行在终端里的 coding agent，可以读项目、改文件、执行命令，也可以用单条命令完成非交互任务。

这页配置的是 Kimi Code 的模型 provider。API Key 来自 SorryCode，模型请求走 SorryCode；Kimi 官方账号和 `/login` 流程不参与这条链路。

参考：[Kimi Code 官方入门文档](https://www.kimi.com/code/docs/kimi-code-cli/guides/getting-started.html)

<h2 id="prepare-api-key">准备 Kimi 分组 Key</h2>

1. 打开 `https://sorrycode.com/keys`
2. 创建一把新的 API Key
3. 为这把 Key 选择支持 Kimi 的分组
4. 单独保存这把 Key，不要和 Codex、Claude Code、Grok 或 Image2 的 Key 混用

可以先查询这把 Key 实际开放的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 Kimi 分组 API Key>"
```

后面的 `model` 必须使用返回结果里的准确 ID。当前常见 ID 包括 `k3`、`kimi-for-coding` 和 `kimi-for-coding-highspeed`，实际可用范围以这把 Key 的返回结果为准。

<h2 id="install">安装 Kimi Code</h2>

macOS / Linux：

```bash
curl -fsSL https://code.kimi.com/kimi-code/install.sh | bash
```

Windows PowerShell：

```powershell
irm https://code.kimi.com/kimi-code/install.ps1 | iex
```

安装后确认命令可用：

```bash
kimi --version
```

<h2 id="configure">写入 SorryCode provider</h2>

配置文件位置：

- macOS / Linux：`~/.kimi-code/config.toml`
- Windows：`%USERPROFILE%\.kimi-code\config.toml`

如果文件里已经有其他 provider，把下面内容合并进去，不要覆盖原有配置。`api_key` 填刚才创建的 Kimi 分组 Key：

```toml
default_model = "sorrycode/kimi"

[providers.sorrycode-kimi]
type = "kimi"
base_url = "https://sorrycode.com/v1"
api_key = "<你的 Kimi 分组 API Key>"

[models."sorrycode/kimi"]
provider = "sorrycode-kimi"
model = "k3"
max_context_size = 1048576
capabilities = ["thinking", "always_thinking", "image_in", "video_in", "tool_use"]
display_name = "K3 via SorryCode"
support_efforts = ["max"]
default_effort = "max"
```

`sorrycode/kimi` 是本机别名，可以自己改。`model = "k3"` 才是发给 SorryCode 的模型 ID。如果分组没有 `k3`，把它换成 `/v1/models` 返回的模型，并按模型实际规格调整 `max_context_size` 和 capabilities。

Kimi Code 会把 `api_key` 以明文写在本机配置中。不要把这个文件提交到 Git，也不要发送包含 Key 的截图。macOS / Linux 可以把权限收紧为：

```bash
chmod 600 ~/.kimi-code/config.toml
```

<h2 id="verify">验证配置</h2>

先检查配置格式和 provider：

```bash
kimi doctor
kimi provider list
```

然后发送一条最小请求：

```bash
kimi -m "sorrycode/kimi" -p "只回复 sorrycode-kimi-ok"
```

看到模型返回内容后，说明 Kimi Code、SorryCode API Key、分组和模型已经连通。

<h2 id="start">开始使用</h2>

进入项目目录后运行：

```bash
cd <你的项目目录>
kimi
```

第一次可以先说：

```text
先看一下这个项目的目录结构，不要修改文件。告诉我项目入口和应该先读哪些文件。
```

需要临时指定模型时使用 `-m`，进入交互界面后也可以用 `/model` 切换已经配置的模型。

<h2 id="boundaries">配置边界</h2>

- 不要用 `/login` 配置 SorryCode。`/login` 面向 Kimi 官方 OAuth 和官方平台 Key。
- 不要只在终端里设置 `KIMI_API_KEY`。普通 provider 不会自动读取这个 Shell 环境变量。
- 不要把 `KIMI_CODE_BASE_URL` 指向 SorryCode。它属于 Kimi 官方 OAuth managed service。
- 不要给 SorryCode 配置 Kimi 官方的 `/search` 或 `/fetch` 服务地址。这页只配置模型 provider。

<h2 id="common-issues">常见问题</h2>

- `401`：检查 Key 是否完整，以及它是否仍然有效
- `404` 或 model not found：重新查询 `/v1/models`，确认 `model` 使用准确 ID
- `missing credentials`：确认 `api_key` 写在 `[providers.sorrycode-kimi]` 下
- 没有可用账号或分组：回到 API Key 页面，为这把 Key 选择支持 Kimi 的分组
- 配置文件解析失败：运行 `kimi doctor`，检查是否重复声明同一个 TOML 字段

更多共性错误见 [排障 / 常见问题](/docs/troubleshoot/common-errors)。
