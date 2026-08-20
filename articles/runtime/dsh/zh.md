---
title: DSH
slug: dsh
order: 1
summary: 启动 DeepSeek Harness Web UI，通过自定义 Responses 提供方接入 SorryCode，并完成首条模型请求。
section: runtime
section_title: 模型与工作台
section_order: 10
group: deepseek
group_title: DeepSeek
group_order: 22
---

# DSH

DSH 是 DeepSeek 开源的 Agent Harness，全名是 DeepSeek Harness。它提供 Web UI，可以选择工作目录、管理模型，并让 Agent 读取文件、执行命令和完成任务。

DSH 不只支持 DeepSeek 模型。它可以添加自定义 OpenAI 兼容提供方，因此也能通过 SorryCode 使用 `grok-4.6` 等 Responses 模型。

DSH 目前仍处于开发者预览阶段，界面和配置可能出现不兼容变更。本页只维护官方 Web UI 的公开配置路径，不要求用户手动维护内部配置文件。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="prepare">准备 Node.js 和 API Key</h2>

先检查本机是否有 Node.js 和 npm：

```bash
node --version
npm --version
```

如果命令不存在，先阅读 [Node.js](/docs/environment/nodejs)。

然后打开 [API Key 页面](https://sorrycode.com/keys)，选择一把所属分组包含目标模型的 Key。本文用 `grok-4.6` 演示，因此需要选择包含该模型的 Grok 分组 Key。同一 Key 分组可以开放多个模型；目标模型属于其他分组时，再准备对应分组的 Key。

<h2 id="start">启动 DSH Web UI</h2>

在准备交给 DSH 的项目目录中运行官方命令：

```bash
npx @deepseek-ai/dsh web
```

命令启动后会打印 Web UI 地址，默认是：

```text
http://127.0.0.1:3080
```

在浏览器中打开这个地址。第一次启动时，DSH 还没有选中工作目录，稍后需要在界面中添加。

<h2 id="configure">添加 SorryCode 提供方</h2>

在 DSH Web UI 中打开 `设置` > `模型`，选择 `添加自定义提供方`。按下面填写：

| 字段 | 值 |
| --- | --- |
| Provider ID | `sorrycode-grok` |
| 显示名称 | `SorryCode Grok` |
| 基础 URL | `https://sorrycode.com/v1` |
| API 协议 | `openai-responses` |
| API 密钥 | 当前目标分组的 SorryCode Key |

Provider ID 需要使用小写，并且会写入会话和模型记录。每把独立 Key 使用唯一的 Provider ID，并在显示名称中标明分组；同一 Key 分组返回的多个模型可以放在同一提供方下，目标模型属于其他分组时新增提供方，不要覆盖已有 Key。需要另一个协议时也应新增 Provider ID。

点击 `获取可用模型`，DSH 会使用当前基础 URL 和 Key 查询 `/models`。从返回结果中选择 `grok-4.6`，再保存提供方。如果模型发现失败，但 Key 和基础 URL 已确认正确，也可以手动添加准确的模型 ID。

模型发现主要确认当前 Key 可以使用哪些模型 ID，不代表图片输入、上下文容量和思考档位已经配置。先用纯文本完成下方连通验证；需要图片或自定义思考档位时，按 DSH 当前[模型配置指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.zh.md)补充能力，并分别发送最小请求验证，不要根据模型名称推断。

DSH 会把密钥存入自己的凭据文件，设置页面只读取脱敏后的描述。公开接入不需要设置环境变量，也不要把 Key 写进普通配置字段或聊天记录。

<h2 id="workspace">选择模型和工作目录</h2>

保存提供方后：

1. 在模型选择器中选择 `sorrycode-grok / grok-4.6`
2. 点击 `选择工作区`
3. 添加并选中启动 DSH 时所在的项目目录
4. 新建会话

如果没有选择工作区，DSH 会禁用会话输入框。

<h2 id="verify">验证连接</h2>

先发一条不修改文件的最小请求：

```text
Reply with exactly DSH_SORRYCODE_OK. Do not modify files.
```

收到模型回复，就说明 `DSH + SorryCode Key + openai-responses + grok-4.6` 这条链路已经连通。模型的具体提示理解、工具选择和输出风格由模型及 DSH 自身负责，不属于 SorryCode 的接入承诺。

<h2 id="other-models">使用其他模型</h2>

DSH 的自定义提供方不绑定 Grok。要使用其他 Responses 模型：

1. 先确认当前 Key 分组是否包含目标模型
2. 同一分组的模型可以加入现有提供方
3. 其他分组使用对应 Key 新建 Provider ID，不覆盖现有提供方
4. 保持基础 URL 为 `https://sorrycode.com/v1`
5. 保持 API 协议为 `openai-responses`
6. 从 `获取可用模型` 的结果中选择准确模型 ID

一个提供方 route 只能使用一种 API 协议。如果以后必须使用 Chat Completions，请新建另一个 Provider ID，不要把两种协议混在同一路由中。

<h2 id="common-issues">常见问题</h2>

- `npx` 不存在：先安装 Node.js，再重新打开终端
- Web UI 打不开：确认启动 DSH 的终端仍在运行，并使用终端打印的实际地址
- `401`：检查 Key 是否完整、有效，并且属于目标模型分组
- 获取模型返回 `401 / 403`：检查 Base URL 和 Key，不要先手动增加未知模型
- 找不到 `grok-4.6`：重新查询模型，确认当前 Key 所属分组包含该模型
- 切换模型后旧模型消失：不要用另一分组的 Key 覆盖现有提供方，为新分组新增 Provider ID
- 图片在发送前被拒绝：模型发现只确认了 ID；按当前模型配置指南补充图片能力并开启新会话
- 输入框不可用：先选择工作区和模型
- 更新后界面或字段变化：DSH 仍处于开发者预览期，以官方当前界面为准

参考：[DeepSeek Harness 官方仓库](https://github.com/deepseek-ai/deepseek-harness)、[Web UI 指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.zh.md)与[模型配置指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.zh.md)。
