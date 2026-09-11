---
title: Cursor Agent
slug: cursor
order: 1
summary: 在 Cursor 编辑器中配置 SorryCode 自定义模型，使用 Agent 完成代码和文件任务。
section: runtime
section_title: 模型与工作台
section_order: 10
group: cursor
group_title: Cursor
group_order: 15
---

# Cursor Agent

Cursor 是面向代码项目的编辑器型 Agent。它可以读取项目、修改文件、运行命令，并在编辑器里持续完成任务。

本页说的是 Cursor 桌面编辑器里的 Agent 模式，不是 `cursor-agent` 命令行工具。命令行工具使用 Cursor 自己的账号和 API 凭证，不能直接把 SorryCode API Key 当成它的登录凭证。

> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。

<h2 id="install">1. 安装 Cursor</h2>

从 [Cursor 官方下载页](https://cursor.com/downloads) 安装适合当前系统的版本，然后登录 Cursor 账号。

打开一个测试项目。第一次接入时，建议使用一个没有重要文件的目录，先完成下面的连通验证。

<h2 id="prepare-key">2. 准备匹配分组的 API Key</h2>

在 [SorryCode API Key 页面](https://sorrycode.com/keys) 选择一把 Key。它所属的分组必须开放你准备在 Cursor 中使用的模型。

先查询这把 Key 实际可以看到的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 SorryCode API Key>"
```

Windows PowerShell 使用 `curl.exe`：

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <你的 SorryCode API Key>"
```

后面的模型名称必须使用返回结果中的准确 `id`。不同分组的 Key 不要混用，哪怕它们看起来都有相同的 `sk-` 前缀。

<h2 id="configure">3. 在 Cursor 中配置 SorryCode</h2>

在 Cursor 中打开：

```text
Cursor Settings → Models → API Keys
```

在 OpenAI 配置区域填写：

| 配置项 | 填写内容 |
| --- | --- |
| OpenAI API Key | 支持目标模型的 SorryCode Key |
| Override OpenAI Base URL | 开启 |
| Base URL | `https://sorrycode.com/v1` |

保存后，在模型列表中添加或选择刚才从 `/v1/models` 查到的准确模型 ID。不要把完整模型目录复制进 Cursor，只添加你实际要用、并且已经用当前 Key 验证过的模型。

Cursor 的 OpenAI Base URL 覆盖是全局配置，不是 OpenCode 那种可以同时保存多把 Key 的 Provider 列表。当前配置通常只使用一把 SorryCode 分组 Key。切换到另一个分组时，替换 API Key 和模型；不要把另一分组的模型直接添加到现有配置里。

<h2 id="verify">4. 先验证文本，再验证 Agent 工具</h2>

在 Cursor 的 Agent 面板中选择刚添加的模型，先发送一条不会修改文件的请求：

```text
只回复 CURSOR_SORRYCODE_OK，不要修改文件。
```

收到完全一致的回复后，再在测试项目中发送：

```text
请在当前项目根目录创建 cursor-sorrycode-check.txt，内容只写 CURSOR_TOOL_OK 和一个换行符。不要修改其他文件。
```

确认文件内容正确，说明模型请求和 Agent 的文件工具都已经走通。完成测试后，可以删除这个测试文件。

<h2 id="boundaries">5. 这条接入路径的边界</h2>

- Cursor 的 BYOK 设置主要覆盖标准模型请求。Tab 补全、Background Agent 和其他 Cursor 专有能力可能继续使用 Cursor 自己的服务，本页不承诺这些能力会经过 SorryCode。
- 使用 SorryCode Key 不等于客户端直连 SorryCode。Cursor 仍可能先通过自己的后端组装请求，再把模型请求发送到配置的 Base URL。对请求必须经过 Cursor 后端这一点有要求时，不要使用这条路径。
- OpenAI Base URL 覆盖可能影响 Cursor 内置模型。要恢复 Cursor 默认模型，关闭覆盖，重新选择内置模型，并重新打开会话。
- 本页不要求设置通用环境变量，也不要把 API Key 写进项目文件、Shell 历史或聊天记录。
- Cursor 账号和订阅是 Cursor 自己的产品边界。SorryCode 只负责经过网关的模型请求和对应的用量扣费。

<h2 id="common-issues">常见问题</h2>

- `401`：检查 Key 是否完整、有效，以及是否属于目标模型分组。
- `404` 或找不到模型：重新请求 `/v1/models`，使用返回的准确模型 ID。
- 文本能回复，文件任务失败：当前模型或 Cursor 会话没有正常启用工具调用。重新开一个 Agent 会话，并用上面的最小文件任务验证。
- 添加模型后请求发到 Cursor 内置服务：检查 `Override OpenAI Base URL` 是否仍然开启，以及 Base URL 是否为 `https://sorrycode.com/v1`。
- 切换分组后旧模型消失：不要覆盖原配置。确认当前 Key 的 `/v1/models` 返回结果，再按新的分组更新模型。
- 想使用 `cursor-agent` CLI：这不是本页覆盖的接入路径。CLI 的账号和凭证体系与 Cursor 编辑器里的 OpenAI BYOK 不同。

需要手动检查网关时，可以回到 [首条请求](/docs/start/first-request)。还没有 API Key 时，先看 [创建 API Key](/docs/start/create-api-key)。
