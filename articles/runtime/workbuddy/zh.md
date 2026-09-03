---
title: WorkBuddy
slug: workbuddy
order: 1
summary: 安装 WorkBuddy，添加 SorryCode 自定义模型，并完成第一次本地文件任务。
section: runtime
section_title: 模型与工作台
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy

WorkBuddy 是桌面 Agent，可以读取资料、调用工具并写入本地文件。下面只保留接入 SorryCode 和完成第一次文件任务所需的步骤。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。不要在对话中粘贴 API Key。

<h2 id="install">安装</h2>

从 [WorkBuddy 官网](https://www.workbuddy.cn/) 下载 macOS 或 Windows 版本，安装后按界面提示登录。

<h2 id="configure">添加 SorryCode 自定义模型</h2>

在 [SorryCode API Key 页面](https://sorrycode.com/keys) 选择一把分组支持目标模型的 Key。WorkBuddy 使用 OpenAI-compatible 的 `/v1/chat/completions`，模型名称必须使用这把 Key 请求 `/v1/models` 返回的准确 `id`。

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 SorryCode API Key>"
```

在 WorkBuddy 中打开：

```text
左下角账户菜单 → 设置 → 模型 → 添加模型 → 自定义 / Custom
```

填写下面的字段：

| 配置项 | 填写内容 |
| --- | --- |
| 提供商 | `自定义 / Custom` |
| 接口地址 | `https://sorrycode.com/v1/chat/completions` |
| API Key | 支持目标模型的 SorryCode Key |
| 模型名称 | `/v1/models` 返回的准确模型 ID |
| 工具调用 | 要执行文件任务时开启，且模型必须支持 tool calls |
| 图片输入 | 仅在模型和分组明确支持图片时开启 |
| 思考模式 | 仅在模型支持 reasoning 时开启 |
| 自定义协议 | 关闭 |

**填写示例：**下面以 Gemini 分组为例。`API Key` 换成你自己的 Gemini 分组 Key，模型 ID 以这把 Key 请求 `/v1/models` 的返回结果为准；其他字段照着填写即可。

```text
添加自定义模型
提供商      自定义 / Custom
接口地址    https://sorrycode.com/v1/chat/completions
API Key     <你的 Gemini 分组 Key>
模型名称    gemini-3.7-flash
工具调用    开启
图片输入    关闭，除非你已确认该模型支持图片
思考模式    开启，档位 high
自定义协议  关闭
```

这是一份界面填写示意，不是 WorkBuddy 可以导入的配置文件。使用 Claude 时，把 API Key 换成 Claude 分组 Key，把模型名称换成该 Key 的 `/v1/models` 返回值。

同一分组的多个模型只需重复添加模型名称。比如 Gemini 分组可以添加 `gemini-3.7-flash` 和 `gemini-3.8-flash`，Claude 分组可以添加 `claude-opus-5` 和 `claude-opus-4-6`。模型是否可用只看当前 Key 的 `/v1/models` 返回结果，不要按展示名称猜 ID。Gemini 的思考档位使用 `high`，Claude 的思考模式等当前 WorkBuddy 版本和分组验证后再开启。

<h2 id="verify">完成第一次文件任务</h2>

新建一个空文件夹，例如 `WorkBuddy-Test`，在“新建任务”中选为工作空间，保持“默认权限”，选择刚添加的模型，然后输入：

```text
请在当前工作空间创建 hello-workbuddy.md，写入今天的日期和一句“SorryCode 连接测试完成”。不要修改其他文件。完成后告诉我保存路径。
```

能正常回复，并在测试文件夹中找到 `hello-workbuddy.md`，就完成了连接、工具调用和文件写入验证。首次使用不要直接选择桌面、下载目录、个人主目录或生产项目；涉及删除、覆盖和执行脚本时先查看操作内容。

<h2 id="boundaries">使用边界</h2>

WorkBuddy 的自定义模型走 Chat Completions。图片生成和视频生成不能作为 WorkBuddy 的主模型；图片输入、思考模式和文件工具都要同时满足模型、分组和客户端版本的能力要求。API Key 只保存在模型设置中，不要放进提示词、项目文件或截图。

Expert 和 Expert Team 仍使用当前模型与已有权限，不会绕过文件限制。需要这些功能时，先完成上面的普通文件任务，再参考 [Agent 能力是怎么扩展的](/docs/runtime/agent-capabilities) 和 [Expert 中心](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center)。

<h2 id="common-issues">常见问题</h2>

| 现象 | 先检查 |
| --- | --- |
| `401` 或 Key 无效 | Key 是否完整、启用，且所属分组支持当前模型 |
| `404` 或 model not found | 地址是否为完整的 `/v1/chat/completions`，模型名是否来自 `/v1/models` |
| 能聊天但不能创建文件 | 是否开启工具调用，模型是否支持 OpenAI-compatible tool calls |
| `429` 或余额不足 | SorryCode 余额、Key 限额和请求频率 |

更多错误见 [常见错误](/docs/troubleshoot/common-errors)。

官方参考：[WorkBuddy 第一个任务](https://www.workbuddy.cn/docs/workbuddy/FirstTask)、[模型配置](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model) 和 [权限模式](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes)。
