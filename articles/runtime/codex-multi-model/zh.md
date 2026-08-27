---
title: 在 ChatGPT / Codex 中使用其他模型
slug: codex-multi-model
order: 2
summary: 通过 SorryCode 的 Responses 接口，在 ChatGPT 桌面 App 或 Codex CLI 中使用 Grok、DeepSeek 等第三方模型。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# 在 ChatGPT / Codex 中使用其他模型

ChatGPT 桌面 App 与 Codex CLI 共用 `~/.codex/config.toml`。Codex 官方允许接入支持 Responses 或 Chat Completions 的其他模型和提供方，其中 Chat Completions 已进入弃用阶段，因此 SorryCode 的第三方模型优先走 Responses。

Grok 不属于 GPT 系列，但可以在同一个 ChatGPT / Codex 工作台中使用。`grok-4.6` 已于 2026 年 8 月 17 日通过 SorryCode 的非流式和流式 Responses 连通验证。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="prepare">先选对 Key 和模型</h2>

打开 [API Key 页面](https://sorrycode.com/keys)，选择一把所属分组包含目标模型的 Key。模型和 Key 必须匹配：

- 使用 `grok-4.6` 时，选择包含该模型的 Grok 分组 Key
- 使用 DeepSeek 时，选择包含目标 DeepSeek 模型的分组 Key
- SorryCode Image2 复用 Codex Key；Grok 仍使用 Grok 分组 Key，不要仅凭 Key 都以 `sk-` 开头就认为可以互换

如果当前 ChatGPT / Codex 已经接入 SorryCode，但保存的是另一分组的 Key，请在目标 Key 右侧点击`接入工具`，选择 `Codex` 和当前系统，再运行生成的命令。安装器会保存这把 Key，不需要设置公开环境变量。以后切回另一分组时，用对应 Key 重新生成一次接入命令即可。

模型 ID 以当前 Key 的分组为准。可以先查询：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 SorryCode API Key>"
```

Windows PowerShell 使用：

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <你的 SorryCode API Key>"
```

本页当前示例：

```text
grok-4.6
deepseek-v4-flash
deepseek-v4-pro
```

模型出现在列表中，表示这把 Key 可以路由到它。本文验证的是接入和响应链路，不承诺不同模型在提示理解、工具选择或输出风格上完全一致。

<h2 id="cli">在 Codex CLI 中使用 Grok</h2>

启动时直接指定模型：

```bash
codex -m grok-4.6
```

进入会话后运行 `/status`，可以确认当前模型和 provider。非交互任务也可以指定模型：

```bash
codex exec -m grok-4.6 "只读检查当前项目，并告诉我入口文件"
```

`/model` 只显示 Codex 当前内置目录中的模型，不能输入任意模型 ID。如果选择器里没有 Grok，继续使用 `-m grok-4.6` 即可。

经常使用 Grok 时，可以新建 `~/.codex/grok.config.toml`：

```toml
model = "grok-4.6"
```

以后运行：

```bash
codex --profile grok
```

这个 profile 只覆盖模型。保留现有 `model_provider`，不要从其他用户的配置中复制 provider 名称。

使用 DeepSeek 时，命令和 profile 的规则相同，只需要把模型 ID 换成当前 Key 实际开放的名称。

<h2 id="app">在 ChatGPT App 中使用 Grok</h2>

ChatGPT App 的模型选择器可能过滤第三方模型。即使 `grok-4.6` 已经可以通过当前 Key 使用，选择器也可能只显示 GPT 模型，或者把当前模型显示为 `Custom`。

1. 在 macOS 菜单栏选择 `ChatGPT` > `设置`

   ![从 macOS 菜单栏打开 ChatGPT 设置](./codex-app-open-settings.png)

2. 在设置窗口左侧打开`配置`

   ![在设置窗口左侧选择配置](./codex-app-configuration-nav.png)

3. 点击`打开 config.toml`

   ![在配置页打开 config.toml](./codex-app-open-config.png)

4. 找到顶层的 `model`
5. 记下原来的值，只把这一项改为 `grok-4.6`
6. 如果同时看到 `model_provider`，保持原值
7. 保存后完全退出 App，macOS 使用 `Command-Q`
8. 重新打开 App，并新建任务验证

相关配置应当类似：

```toml
model = "grok-4.6"
```

如果文件里已经有 `model`，请修改原值，不要重复添加。`model` 必须放在顶层，不能写进 `[model_providers.*]` 配置段。

切回 GPT 或其他模型时，先确认 ChatGPT / Codex 当前保存的是对应分组的 Key，再恢复原来的 `model`，完全退出并重开 App。已经打开的旧任务可能保留原模型，因此要用新任务验证。

App 显示 `Custom` 时，不要询问模型身份。到 SorryCode 用量记录中查看这次请求的实际模型 ID。

<h2 id="related">Grok 的其他能力</h2>

本页只讲 Grok 文字模型在 ChatGPT / Codex 中的使用。其他入口分别维护：

- xAI 自己的终端工作台：[Grok Build](/docs/runtime/grok-build)
- 图片接口：[Grok 图片生成](/docs/runtime/grok-image)
- 视频和异步轮询：[Grok 视频生成](/docs/runtime/grok-video)

<h2 id="troubleshoot">模型不能使用</h2>

- `401`：确认 ChatGPT / Codex 当前保存的是目标分组的完整 Key
- `404` 或模型不存在：重新查询 `/v1/models`，使用返回结果中的准确 ID
- CLI 找不到模型：直接使用 `-m`，不要依赖 `/model` 列表
- App 仍使用原模型：完全退出 App，重开后新建任务
- App 显示 `Custom`：到 SorryCode 用量记录核对实际模型
- 切换后旧会话看不到：检查是否误改了 `model_provider`，恢复修改前的原值

参考：[OpenAI Codex 的其他模型说明](https://learn.chatgpt.com/docs/models#other-models)与 [Codex 配置说明](https://learn.chatgpt.com/docs/config-file/config-reference)。
