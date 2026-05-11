---
title: Hermes Agent
slug: hermes-agent
order: 4
summary: 用 Hermes Agent 的 Custom endpoint 把它接到 SorryCode。macOS / Linux 直接走官方安装，Windows 当前按 WSL2 主路径处理。
section: runtime
section_title: Runtime
section_order: 10
---

# Hermes Agent

如果你想把 `Hermes Agent` 接到 SorryCode，这页给你当前最稳的接法。

先把两个前提讲清楚：

- `macOS / Linux` 路径最短
- `Windows` 当前按官方 `WSL2` 路线走

更重要的是：这页是进阶自定义接入，不是小白默认主路径。如果你的目标是用 GPT 模型获得最好的缓存、上下文和成本表现，优先用 [Runtime / Codex](/docs/runtime/codex)。`Hermes Agent` 可以接 OpenAI-compatible 网关，但不要默认认为它跑 GPT 的 API 消耗一定和 Codex 一样划算。

SorryCode 这边可以接住 `Hermes Agent`，但不把原生 `PowerShell` 路径写成“已经验证完成”的默认方案。

<h2 id="what-is-hermes-agent">Hermes Agent 是什么</h2>

- `Hermes Agent` 是 Nous Research 提供的终端 agent / runtime
- 它支持 provider runtime，也支持自定义 endpoint
- SorryCode 当前推荐通过 `Custom endpoint` 把它接到 OpenAI-compatible 网关

第一次接入时，你真正要填的还是这 3 个值：

- Base URL：`{{API_BASE_URL}}`
- Model：`gpt-5.4`
- API Key：你的 `sk-...`

参考：

- [Hermes Agent Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation)
- [Provider Runtime](https://hermes-agent.nousresearch.com/docs/developer-guide/provider-runtime/)
- [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration/)

<h2 id="recommended-path">当前推荐路径</h2>

第一次接入时，按这 4 步走最稳：

1. 先按官方文档完成安装，Windows 走 `WSL2`
2. 在 SorryCode 控制台创建 API Key
3. 运行 `hermes model`，选择 `Custom endpoint`
4. 填入 `Base URL / Model / API Key`，再做一次最小验证

如果你已经装好了 `Hermes Agent`，可以直接跳到下面“接到 SorryCode”。

<h2 id="install-hermes-agent">安装 Hermes Agent</h2>

### macOS / Linux

安装方式以官方文档为准：

- [Hermes Agent Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation)

装完后先确认 CLI 已经可用：

```bash
hermes --version
```

### Windows

当前推荐按官方 `WSL2` 路线安装。

原因不是 SorryCode 不支持 Windows，而是 `Hermes Agent` 上游当前更偏 Linux 环境。如果你的目标只是尽快跑通一条稳定链路，这里不要硬把原生 `PowerShell` 当默认路径。

<h2 id="connect-sorrycode">接到 SorryCode</h2>

最短路径是运行：

```bash
hermes model
```

然后在向导里选择 `Custom endpoint`，再填这 4 项：

- Base URL：`{{API_BASE_URL}}`
- Model：`gpt-5.4`
- API Key：你的 `sk-...`
- Context length：先留空，走自动探测

对第一次接入来说，这条路径比手改配置更稳。

### 如果你更想手动写配置

也可以按官方配置模型，写成：

```yaml
model:
  provider: custom
  default: gpt-5.4
  base_url: {{API_BASE_URL}}
  api_key: 你的 sk-...
```

如果你后面要维护多个自定义 endpoint，再用官方 `custom_providers` 写法扩展就够了。第一次接入不用先把这块配复杂。

<h2 id="create-api-key">创建 API Key</h2>

如果你还没有 `sk-...`，先补这 3 步：

1. 登录 `https://sorrycode.com/login`
2. 进入 `https://sorrycode.com/keys`
3. 创建新的 `sk-...` 并安全保存

完整说明看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="minimal-verification">最小验证</h2>

更稳的做法还是先打一条最小请求，把这几层一起确认掉：

- API Key 可用
- `{{API_BASE_URL}}` 可达
- OpenAI-compatible 路径正常

最小请求直接看 [Platform / 首条请求](/docs/platform/first-request) 里的 OpenAI-compatible 示例。

如果这一步已经通过，再回到你的项目目录里启动 `Hermes Agent` 就够了。

<h2 id="next">下一步</h2>

- 想看 API Key 细节：去 [Platform / 创建 API Key](/docs/platform/create-api-key)
- 想先做网关验证：去 [Platform / 首条请求](/docs/platform/first-request)
- 想查共性报错：去 [排障 / 常见问题](/docs/troubleshoot/common-errors)
