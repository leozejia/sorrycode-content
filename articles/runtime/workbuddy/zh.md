---
title: WorkBuddy
slug: workbuddy
order: 1
summary: 安装 WorkBuddy，接入包括 Gemini 3.7 Flash 和 Claude Opus 在内的 SorryCode 自定义聊天模型，并在默认权限下完成第一个本地文件任务。
section: runtime
section_title: 模型与工作台
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy

WorkBuddy 是一个桌面 Agent，可以读取资料、调用工具并把结果写入本地文件。下面的步骤会把它接到 SorryCode，并用一个空文件夹验证模型和文件写入。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="install">安装 WorkBuddy</h2>

从 [WorkBuddy 官网](https://www.workbuddy.cn/) 下载 macOS 或 Windows 版本，安装后按界面提示登录。不要从非官方站点下载安装包。

<h2 id="prepare-key">准备 API Key</h2>

WorkBuddy 使用 OpenAI-compatible 的 `/v1/chat/completions` 接口。在 [SorryCode API Key 页面](https://sorrycode.com/keys) 选择一把所属分组支持目标模型和这个接口的 Key。下面的 Gemini 示例使用 Gemini 分组 Key。已有符合条件的 Key 可以直接复用，不必为 WorkBuddy 单独创建；如果你想分开统计用量、设置限额或轮换凭证，再按用途新建一把 Key。

WorkBuddy 需要准确的模型 ID。模型名称以当前 Key 请求 `/v1/models` 返回的 `id` 为准，不要根据展示名称猜测。

```bash
curl https://sorrycode.com/v1/models -H "Authorization: Bearer <WORKBUDDY_API_KEY>"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <WORKBUDDY_API_KEY>"
```

<h2 id="connect">添加 SorryCode 自定义模型</h2>

在 WorkBuddy 中打开：

```text
左下角账户菜单 → 设置 → 模型 → 添加模型 → 自定义 / Custom
```

按下面填写：

| 配置项 | 设置 |
| --- | --- |
| 提供商 | `自定义 / Custom` |
| 接口地址 | `https://sorrycode.com/v1/chat/completions` |
| API Key | 可访问目标模型和 OpenAI-compatible 接口的 SorryCode Key |
| 模型名称 | `/v1/models` 返回的准确模型 ID |
| 工具调用 | 开启 |
| 图片输入 | 仅在模型和分组支持图片时开启 |
| 思考模式 | 仅在模型支持推理模式时开启 |
| 自定义协议 | 关闭 |
| 输入 / 输出 | 保持提供商默认值 |

这里需要填写完整的 `/v1/chat/completions` 地址。保存后，新模型会出现在“自定义模型”分组中。

<h2 id="claude-opus">使用 Claude Opus</h2>

WorkBuddy 可以通过同一套自定义模型配置使用 `claude-opus-5` 和 `claude-opus-4-6`。先确认 Claude 分组 Key 的 `/v1/models` 返回这两个 ID，再分别添加两个模型：

- 接口地址都使用 `https://sorrycode.com/v1/chat/completions`
- API Key 都使用同一把 Claude 分组 Key
- 模型名称分别填写 `claude-opus-5` 和 `claude-opus-4-6`
- “工具调用”开启，“自定义协议”关闭

两个模型需要分别保存，之后会同时出现在“自定义模型”分组中。本页只说明文本和工具调用所需的配置，图片输入和思考模式需要按当前 WorkBuddy 版本与分组能力另行验证。

<h2 id="gemini-flash">使用 Gemini Flash</h2>

使用 `gemini-3.7-flash` 时，选择 Gemini 分组 Key，并按下面填写自定义模型：

- 接口地址：`https://sorrycode.com/v1/chat/completions`
- API Key：Gemini 分组的 SorryCode Key
- 模型名称：`gemini-3.7-flash`
- “工具调用”：只有当前模型和分组支持时才开启
- “自定义协议”：关闭

账号完成模型同步后，同一把 Gemini 分组 Key 也可以用于 `gemini-3.8-flash`。先确认 `/v1/models` 返回准确的模型 ID，再用相同的接口地址和 Key 单独添加一个自定义模型。在该响应列出 3.8 之前，不要把它保存为可用模型。

<h2 id="add-more-models">添加更多模型</h2>

WorkBuddy 不会自动导入当前 Key 返回的全部模型。要使用同一分组里的多个模型，先通过 `/v1/models` 查到准确 ID，再为每个模型重复一次“添加模型”。接口地址和 API Key 可以保持不变，只需填写对应的模型 ID。保存后，这些模型会一起出现在“自定义模型”分组中。

这不代表 WorkBuddy 可以使用 SorryCode 的所有模型。自定义模型目前需要兼容 OpenAI Chat Completions；图片生成、视频生成等非聊天模型不能作为 WorkBuddy 主模型。文件操作等 Agent 任务还要求模型支持工具调用，图片输入和思考模式也只能在模型明确支持时开启。

<h2 id="verify">完成第一个文件任务</h2>

新建一个空文件夹，例如 `WorkBuddy-Test`，在“新建任务”中把它设为工作空间，并保持“默认权限”。选择刚添加的模型，然后输入：

```text
请在当前工作空间创建 hello-workbuddy.md，写入今天的日期和一句“SorryCode 连接测试完成”。不要修改其他文件。完成后告诉我保存路径。
```

收到正常回复，并在测试文件夹中找到 `hello-workbuddy.md`，说明模型连接、工具调用和工作空间写入已经可用。

<h2 id="experts">Expert 和 Expert Team</h2>

WorkBuddy 的 Expert 会把角色、方法和工具组合起来，处理一类明确的问题。Expert Team 适合需要多个专业角色协作的复杂任务，由负责人拆分任务并汇总结果。

Expert 不是新的模型，也不会绕过文件权限。它仍然使用当前模型，并通过已配置的 Skills、MCP 或工具工作。第一次使用时先完成上面的普通文件任务；需要固定专业角色时再选择 Expert，需要多人协作时再选择 Expert Team。

这些机制的关系见 [Agent 能力是怎么扩展的](/docs/runtime/agent-capabilities)。WorkBuddy 的具体设置以 [Expert 中心](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center) 为准。

<h2 id="permissions">文件权限</h2>

- 第一次使用只选择空测试目录，不要选择桌面、下载目录、个人主目录或生产项目
- 保持默认权限，涉及删除、覆盖、批量移动或执行脚本时先查看操作内容
- 重要文件使用副本，让 WorkBuddy 写入新文件，不覆盖唯一原件
- API Key 只保存在模型设置中，不要放进提示词、项目文件或截图
- 不要在包含客户资料、财务资料或凭证的目录中开启完全访问

<h2 id="common-issues">常见问题</h2>

| 现象 | 检查什么 |
| --- | --- |
| `401` 或 Key 无效 | Key 是否完整、仍然启用，并且所属分组支持当前模型 |
| `404` 或 model not found | 接口是否包含 `/v1/chat/completions`，模型名是否为 `/v1/models` 返回的准确 ID |
| 能聊天但不能创建文件 | “工具调用”是否开启，模型是否支持 OpenAI-compatible tool calls |
| 图片无法识别 | 模型、分组和“图片输入”是否同时支持图片 |
| `429` 或余额不足 | SorryCode 余额、Key 限额和请求频率 |

更多共性错误见 [常见错误](/docs/troubleshoot/common-errors)。上游参考：[WorkBuddy 第一个任务](https://www.workbuddy.cn/docs/workbuddy/FirstTask)、[模型配置](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model) 和 [权限模式](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes)。
