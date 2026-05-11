---
title: OpenClaw
slug: openclaw
order: 3
summary: 用 OpenClaw 的自定义 API 路径把它接到 SorryCode，先装 CLI，再把 Base URL、模型和 API Key 一次写进去。
section: runtime
section_title: Runtime
section_order: 10
---

# OpenClaw

如果你已经决定用 `OpenClaw`，这页给你一条够短也够稳的接入路径。

当前这页定位是进阶自定义接入，不是小白默认主路径。

如果你的目标是用 GPT 模型获得最好的缓存、上下文和成本表现，优先用 [Runtime / Codex](/docs/runtime/codex)。`OpenClaw` 可以接 OpenAI-compatible 网关，但不要默认认为它跑 GPT 的 API 消耗一定和 Codex 一样划算。

当前推荐做法很简单：

- 先按 OpenClaw 官方文档把 CLI 装好
- 再用 OpenClaw 自带的 onboarding，把默认模型入口改到 SorryCode
- 最后做一次最小验证

<h2 id="what-is-openclaw">OpenClaw 是什么</h2>

- `OpenClaw` 是一个面向代码工作的终端 agent / runtime
- 它可以读项目、改文件、执行命令，也支持接入自定义模型提供方
- SorryCode 当前推荐通过 OpenAI-compatible 网关接这条链路

第一次接入时，你真正要填的只有 3 个值：

- Base URL：`{{API_BASE_URL}}`
- Model：`gpt-5.4`
- API Key：你的 `sk-...`

参考：

- [OpenClaw Installation](https://docs.openclaw.ai/install)
- [OpenClaw Onboarding](https://docs.openclaw.ai/cli/onboard)
- [Configuration Reference](https://docs.openclaw.ai/gateway/configuration-reference)

<h2 id="recommended-path">当前推荐路径</h2>

第一次接入时，按这 4 步走最稳：

1. 先按官方安装文档把 `OpenClaw` 装好
2. 在 SorryCode 控制台创建 API Key
3. 用 `openclaw onboard` 把 `Base URL / Model / API Key` 一次写进去
4. 做一次最小验证

如果你本机已经在用 `OpenClaw`，可以直接跳到下面“接到 SorryCode”。

<h2 id="install-openclaw">安装 OpenClaw</h2>

安装方式以 OpenClaw 官方文档为准：

- [OpenClaw Installation](https://docs.openclaw.ai/install)

装完后，先确认 CLI 已经可用：

```bash
openclaw --version
```

如果这一步都还没通，不要急着改模型配置，先把 CLI 本身装稳。

<h2 id="connect-sorrycode">接到 SorryCode</h2>

最短路径是直接用 OpenClaw 官方的 onboarding，把自定义 API 信息一次写进去。

### 直接写入 SorryCode 配置

```bash
openclaw onboard \
  --non-interactive \
  --auth-choice custom-api-key \
  --custom-base-url "{{API_BASE_URL}}" \
  --custom-model-id "gpt-5.4" \
  --custom-api-key "你的 sk-..." \
  --secret-input-mode plaintext \
  --custom-compatibility openai
```

这条命令做完之后，OpenClaw 就会把默认模型入口切到 SorryCode。

### 如果你更想交互式完成

也可以先跑：

```bash
openclaw onboard --install-daemon
```

然后在向导里填这 3 个值：

- Base URL：`{{API_BASE_URL}}`
- Model ID：`gpt-5.4`
- API Key：你的 `sk-...`

如果向导继续问兼容协议，选 `OpenAI`。

### 如果你已经在维护自己的 provider 配置

OpenClaw 也支持手动改配置。更常见的是：

- `~/.openclaw/openclaw.json`
- `~/.openclaw/agents/<agentId>/agent/models.json`

第一次接入不建议从这里开始。先把 onboarding 跑通，再决定要不要自己维护 provider 树。具体字段参考官方 [Configuration Reference](https://docs.openclaw.ai/gateway/configuration-reference)。

<h2 id="create-api-key">创建 API Key</h2>

如果你还没有 `sk-...`，先补这 3 步：

1. 登录 `https://sorrycode.com/login`
2. 进入 `https://sorrycode.com/keys`
3. 创建新的 `sk-...` 并安全保存

完整说明看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="minimal-verification">最小验证</h2>

更稳的做法不是直接进大项目，而是先打一条最小请求，确认这 3 层都没问题：

- API Key 可用
- `{{API_BASE_URL}}` 可达
- OpenAI-compatible 路径正常

最小请求直接看 [Platform / 首条请求](/docs/platform/first-request) 里的 OpenAI-compatible 示例。

如果这一步已经通过，再回到你的项目目录里启动 OpenClaw 就够了。

<h2 id="next">下一步</h2>

- 想看 API Key 细节：去 [Platform / 创建 API Key](/docs/platform/create-api-key)
- 想先做网关验证：去 [Platform / 首条请求](/docs/platform/first-request)
- 想查共性报错：去 [排障 / 常见问题](/docs/troubleshoot/common-errors)
