---
title: 在 Codex 中使用其他模型
slug: codex-multi-model
order: 2
summary: 通过 SorryCode 的 OpenAI 兼容接口，在 Codex CLI 或 App 中使用 DeepSeek 等模型。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# 在 Codex 中使用其他模型

完成 [Codex 接入](/docs/runtime/codex) 后，Codex CLI 和 App 会共用 `~/.codex/config.toml` 以及当前已有的 provider 和认证配置。在当前 API Key 分组内切换模型时，只需要改模型 ID。不要修改 `model_provider`，也不需要重新安装或登录。

CLI 可以为每次启动单独指定模型。Codex App 当前无法在界面中可靠地显示和切换 DeepSeek，需要修改配置中的默认模型并重启 App。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="prepare">确认 Key 和模型 ID</h2>

打开 [API Key 页面](https://sorrycode.com/keys)，确认当前 Key 所属分组包含目标模型。已有符合条件的 Key 可以继续使用；只有需要分开统计用量、设置限额或轮换凭证时，才需要新建一把 Key。

模型 ID 以当前分组显示的名称为准。比如分组开放了下面两个模型，后续命令就直接使用这些名称。模型出现在分组中，只表示 Key 可以路由到它；在 Codex 中能否稳定使用，还取决于模型对 Responses、流式输出和工具调用的兼容性。

```text
deepseek-v4-flash
deepseek-v4-pro
```

<h2 id="cli">在 Codex CLI 中切换</h2>

启动 Codex 时使用 `-m` 指定模型：

```bash
codex -m deepseek-v4-flash
```

进入会话后运行 `/status`，可以确认当前模型和 provider。非交互任务也可以指定模型：

```bash
codex exec -m deepseek-v4-flash "检查当前代码变更"
```

如果模型已经出现在 Codex 内置模型目录中，也可以在会话里输入 `/model`，再从列表中选择。`/model` 只显示当前目录中的模型，不能用来输入任意模型 ID。DeepSeek 当前不在 Codex 内置模型目录中，所以请直接使用 `-m`。

经常使用同一个模型时，可以创建 Codex 官方 profile。新建 `~/.codex/deepseek.config.toml`：

```toml
model = "deepseek-v4-flash"
```

以后使用下面的命令启动：

```bash
codex --profile deepseek
```

这个 profile 只覆盖模型。provider 和认证会继承当前的全局配置，无论现有 provider 叫什么，都不要为了切换模型修改它。

<h2 id="app">在 Codex App 中切换</h2>

截至 2026 年 8 月，Codex App 的模型选择器可能会过滤第三方模型。即使 DeepSeek 已经可以通过当前 Key 使用，选择器也可能只显示 GPT 模型，或者把当前模型显示为 `Custom`。

新任务需要使用 DeepSeek 时，按下面的步骤修改默认模型。截图使用 macOS 中文界面；其他系统从 App 设置进入`配置`页面后，修改方法相同。

1. 在 macOS 菜单栏选择 `ChatGPT` > `设置`

   ![从 macOS 菜单栏打开 ChatGPT 设置](./codex-app-open-settings.png)

2. 在设置窗口左侧打开`配置`

   ![在设置窗口左侧选择配置](./codex-app-configuration-nav.png)

3. 点击`打开 config.toml`

   ![在配置页打开 config.toml](./codex-app-open-config.png)

4. 找到顶层的 `model`
5. 记下原来的 `model` 值，只把这一项改成目标模型。如果同时看到 `model_provider`，保持它原来的值
6. 保存文件后完全退出 App，再重新打开。macOS 使用 `Command-Q`，不能只关闭窗口
7. 新建任务，不要用已经打开的旧任务验证切换结果

切换到 DeepSeek 后，相关配置应当类似下面这样：

```toml
model = "deepseek-v4-flash"
```

如果文件里已经有 `model`，请修改原来的值，不要重复添加；如果没有，就在顶层新增这一项。不要新增、删除或修改 `model_provider`。`model` 不能写进任何 `[model_providers.*]` 配置段。

想切回 GPT 时，把 `model` 恢复为切换前记下的值，再完全退出并重开 App。不要照抄其他用户的 GPT 模型 ID，不同分组和版本提供的模型可能不同。

Codex App 当前一次使用一个全局默认模型，不能把 DeepSeek 和 GPT 同时放进模型选择器后按任务切换。模型目录在 App 启动时读取，只关闭窗口不会刷新配置。已经打开的任务也可能保留原来的模型或运行配置。

App 显示 `Custom` 时，不要通过询问模型身份来判断是否切换成功。到 SorryCode 用量记录中查看这次请求的实际模型 ID。

切换模型时只改 `model`。Codex 的历史会话带有 provider 信息，老用户如果把原来的 `model_provider` 改成 `sorrycode`，原 provider 下的旧会话会全部从当前列表中消失，看起来像被清空。这不代表会话数据已被删除，恢复 `model_provider` 原值后应会重新出现。不要照抄本文或其他用户的 provider 值，也不要修改 provider 配置段、认证文件、`CODEX_HOME` 或会话目录。

<h2 id="troubleshoot">模型不能使用</h2>

- CLI 提示模型不存在：确认模型 ID 与分组提供的名称完全一致，并检查 Key 所属分组
- App 仍然使用原模型：确认已经完全退出 App，macOS 需要按 `Command-Q`，重开后再新建任务
- App 显示 `Custom`：这是当前版本使用自定义模型时可能出现的名称，到 SorryCode 用量记录核对实际模型 ID
- 可以开始回复，但工具调用失败：换回已验证模型，并把模型 ID 和错误信息提交给 SorryCode
- 切换后旧会话全部不见：检查是否误改了 `model_provider`，把它恢复为修改前的原值；不要先重跑安装器
- 切换后行为和旧任务不一致：新建任务再验证，不要修改或迁移历史任务

参考：[Codex 配置说明](https://developers.openai.com/codex/config-reference/)、[DeepSeek 的 Codex 接入说明](https://api-docs.deepseek.com/quick_start/agent_integrations/codex/)、[Codex App 自定义模型问题](https://github.com/openai/codex/issues/19694)。
