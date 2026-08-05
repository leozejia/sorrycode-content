---
title: WorkBuddy
slug: workbuddy
order: 1
summary: 安装 WorkBuddy，接入 SorryCode 自定义模型，并在默认权限下完成第一个本地文件任务。
section: runtime
section_title: 模型与工作台
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy

WorkBuddy 是一个桌面 Agent，可以读取资料、调用工具并把结果写入本地文件。下面的步骤会把它接到 SorryCode，并用一个空文件夹验证模型和文件写入。

<h2 id="install">安装 WorkBuddy</h2>

从 [WorkBuddy 官网](https://www.workbuddy.cn/) 下载 macOS 或 Windows 版本，安装后按界面提示登录。不要从非官方站点下载安装包。

<h2 id="prepare-key">准备 WorkBuddy Key</h2>

在 [SorryCode API Key 页面](https://sorrycode.com/keys) 为 WorkBuddy 单独创建一把 Key，并选择支持目标模型的分组。不同工具应使用各自分组的 Key，余额仍然共用。

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
| API Key | WorkBuddy 专用 SorryCode Key |
| 模型名称 | `/v1/models` 返回的准确模型 ID |
| 工具调用 | 开启 |
| 图片输入 | 仅在模型和分组支持图片时开启 |
| 思考模式 | 仅在模型支持推理模式时开启 |
| 自定义协议 | 关闭 |
| 输入 / 输出 | 保持提供商默认值 |

这里需要填写完整的 `/v1/chat/completions` 地址。保存后，新模型会出现在“自定义模型”分组中。

<h2 id="verify">完成第一个文件任务</h2>

新建一个空文件夹，例如 `WorkBuddy-Test`，在“新建任务”中把它设为工作空间，并保持“默认权限”。选择刚添加的模型，然后输入：

```text
请在当前工作空间创建 hello-workbuddy.md，写入今天的日期和一句“SorryCode 连接测试完成”。不要修改其他文件。完成后告诉我保存路径。
```

收到正常回复，并在测试文件夹中找到 `hello-workbuddy.md`，说明模型连接、工具调用和工作空间写入已经可用。

<h2 id="permissions">文件权限</h2>

- 第一次使用只选择空测试目录，不要选择桌面、下载目录、个人主目录或生产项目
- 保持默认权限，涉及删除、覆盖、批量移动或执行脚本时先查看操作内容
- 重要文件使用副本，让 WorkBuddy 写入新文件，不覆盖唯一原件
- API Key 只保存在模型设置中，不要放进提示词、项目文件或截图
- 不要在包含客户资料、财务资料或凭证的目录中开启完全访问

<h2 id="common-issues">常见问题</h2>

| 现象 | 检查什么 |
| --- | --- |
| `401` 或 Key 无效 | Key 是否完整、仍然启用，并属于 WorkBuddy 使用的分组 |
| `404` 或 model not found | 接口是否包含 `/v1/chat/completions`，模型名是否为 `/v1/models` 返回的准确 ID |
| 能聊天但不能创建文件 | “工具调用”是否开启，模型是否支持 OpenAI-compatible tool calls |
| 图片无法识别 | 模型、分组和“图片输入”是否同时支持图片 |
| `429` 或余额不足 | SorryCode 余额、Key 限额和请求频率 |

更多共性错误见 [常见错误](/docs/troubleshoot/common-errors)。上游参考：[WorkBuddy 第一个任务](https://www.workbuddy.cn/docs/workbuddy/FirstTask)、[模型配置](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model) 和 [权限模式](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes)。
