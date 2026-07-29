---
title: WorkBuddy 接入 SorryCode
slug: workbuddy-sorrycode
order: 2
summary: 在 WorkBuddy 里添加 SorryCode 自定义模型，正确填写接口、API Key、模型 ID 和能力开关。
section: runtime
section_title: 模型与工作台
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy 接入 SorryCode

WorkBuddy 支持 OpenAI 兼容的自定义 API。你不需要设置环境变量，也不需要先编辑 `models.json`；直接在 WorkBuddy 的模型设置里填写 SorryCode 接口、专用 API Key 和准确模型 ID。

本文按 WorkBuddy `5.3.5` 的界面编写。界面以后可能调整，但配置含义不变。

<h2 id="prepare-key">准备一把专用 API Key</h2>

1. 打开 <https://sorrycode.com/keys>
2. 创建一把新的 API Key
3. 为它选择支持你准备使用的模型的分组
4. 单独保存这把 Key，不要和 Codex、Claude Code、Grok 或 Image2 的 Key 混用

先查询这把 Key 实际开放的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <你的 WorkBuddy 专用 API Key>"
```

后面填写的“模型名称”必须使用返回结果中的准确 `id`。不要根据宣传名称猜模型 ID。

<h2 id="open-settings">打开自定义模型</h2>

在 WorkBuddy 左下角点击账户名称，然后依次打开：

```text
设置 → 模型 → 添加模型
```

在“提供商”列表的最下方选择：

```text
自定义 / Custom
```

![在 WorkBuddy 中选择自定义模型提供商](./custom-provider.png)

<h2 id="fields">填写 SorryCode 配置</h2>

按下面填写：

| 配置项 | 填什么 |
| --- | --- |
| 提供商 | `自定义 / Custom` |
| 接口地址 | `https://sorrycode.com/v1/chat/completions` |
| API Key | 你的 WorkBuddy 专用 SorryCode API Key |
| 模型名称 | `/v1/models` 返回的准确模型 ID |
| 工具调用 | 开启 |
| 图片输入 | 只有模型和当前分组明确支持图片输入时才开启 |
| 思考模式 | 只有模型明确支持推理模式时才开启 |
| 自定义协议 | 关闭 |
| 输入 / 输出 | 第一次保持“使用提供商默认值” |

WorkBuddy 这里要求填写完整接口地址，所以要包含 `/v1/chat/completions`。不要只填 `https://sorrycode.com`，也不要把接口写成 `/responses` 或 `/messages`。

“工具调用”决定模型能否要求 WorkBuddy 创建文件、执行受控操作或调用技能。只想聊天时它不是必需的，但 WorkBuddy 的核心办公任务依赖它，默认应开启。

填完后点击“保存”。WorkBuddy 会把配置写入本机 `~/.workbuddy/models.json`，并在模型选择器中增加“自定义模型”分组。公开接入仍以图形界面为主，不建议手动修改这个文件。

<h2 id="verify">验证连接</h2>

关闭设置，回到“新建任务”，从模型选择器中选中刚才保存的模型。

先验证普通回复：

```text
只回复：workbuddy-sorrycode-ok
```

再选择一个空测试文件夹作为工作空间，验证工具调用：

```text
请在当前工作空间创建 connection-test.md，只写一行：WorkBuddy 已通过 SorryCode 完成工具调用。不要修改其他文件。完成后告诉我保存路径。
```

看到文字回复并找到 `connection-test.md`，才算基础链路完整。只有第一步成功、第二步没有生成文件，说明模型连接正常，但工具调用还没有跑通。

<h2 id="security">Key 存在哪里</h2>

WorkBuddy 会把自定义模型配置保存在本机：

```text
~/.workbuddy/models.json
```

这个文件可能包含明文 API Key：

- 不要提交到 Git
- 不要上传到网盘或聊天群
- 截图时遮住整个 API Key 输入框
- 不再使用时，从 WorkBuddy 的模型设置中删除该模型，并在 SorryCode 控制台删除或轮换对应 Key

<h2 id="common-issues">常见问题</h2>

### `401` 或提示 API Key 无效

重新复制 WorkBuddy 专用 Key，检查是否带入空格，并确认 Key 没有被删除或禁用。

### `404` 或 model not found

确认接口地址完整写成：

```text
https://sorrycode.com/v1/chat/completions
```

然后重新请求 `/v1/models`，把模型名称改成返回结果中的准确 ID。

### 能回复，但不能创建文件

检查“工具调用”是否开启。若已经开启，换用明确支持 OpenAI-compatible tool calls 的模型，并在一个空工作空间里重新测试。

### 图片无法识别

只有模型、分组和 WorkBuddy 配置同时支持图片输入时才开启“图片输入”。开启复选框不会让纯文本模型自动获得看图能力。

### `429`、余额不足或请求过多

检查 SorryCode 余额、API Key 分组和限额。复杂办公任务可能连续调用模型，不要只根据一次对话估算完整任务成本。

更多共性错误见 [排障 / 常见问题](/docs/troubleshoot/common-errors)。上游参考：[WorkBuddy 模型配置](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model)。
