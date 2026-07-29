# WorkBuddy 内容维护策略

更新时间：2026-07-29

这份文档定义 SorryCode 如何长期维护 WorkBuddy 相关公开内容。它是
`sorrycode-content` 的内部治理文档，不进入线上 docs。

## 核心判断

WorkBuddy 是一个会持续扩展的桌面 Agent 生态，不应被压缩成单篇安装教程。SorryCode
公开文档负责讲清通过 SorryCode 使用 WorkBuddy 的闭环、边界和常见问题，不负责搬运
WorkBuddy 官方完整手册，也不应因为上游出现一个新菜单就立即增加页面。

当前采用“系列入口 + 专题页面”的结构。每篇只解决一个稳定问题，后续按真实用户需求和
实测结果增加专题。

## 当前公开页面

| 页面 | 职责 |
| --- | --- |
| `WorkBuddy 快速开始` | 安装、接入分流、工作空间和第一个低风险文件任务 |
| `WorkBuddy 接入 SorryCode` | 自定义模型字段、专用 Key、模型 ID、能力开关和连接排障 |
| `WorkBuddy 的权限与工作空间` | 默认权限、完全访问、工作空间隔离、备份和凭证边界 |

对应路径：

```text
articles/runtime/workbuddy/
articles/runtime/workbuddy-sorrycode/
articles/runtime/workbuddy-permissions/
```

## 当前证据状态

首批内容基于 2026-07-29 可见的 WorkBuddy `5.3.5` 桌面界面、官方文档和公开网站。

| 事实 | 证据 | 当前结论 |
| --- | --- | --- |
| WorkBuddy 支持自定义模型 | 桌面界面和用户提供的截图 | 已确认存在 `自定义 / Custom` 提供商 |
| 自定义模型使用 OpenAI-compatible API | 桌面界面和官方模型文档 | 当前表单要求填写接口地址、API Key 和模型名称 |
| 能力开关 | 桌面界面 | 当前可见工具调用、图片输入、思考模式和自定义协议 |
| 本地配置位置 | 桌面界面 | 当前界面指向 `~/.workbuddy/models.json` |
| 工作空间和权限 | 桌面界面和官方权限文档 | 当前有默认权限、工作空间边界和完全访问开关 |
| SorryCode 真实端到端请求 | 尚未使用真实 Key 执行 | 普通对话和文件创建仍需做正式 smoke test |

公开截图位于：

```text
articles/runtime/workbuddy-sorrycode/custom-provider.png
```

不要把“界面和协议推导成立”写成“端到端已经实测成功”。完成真实 smoke test 后，才能在
公开文档或内部结论中使用“已验证可用”的表述。

## 稳定接入原则

下面这些是 SorryCode 当前的长期表达，不随 WorkBuddy 菜单位置变化：

- 为 WorkBuddy 创建独立的 SorryCode 分组 Key，不与 Codex、Claude Code、Grok 或
  Image2 共用一把 Key。
- 先请求 `/v1/models`，再填写返回结果中的准确模型 ID，不根据展示名称猜 ID。
- 当前 WorkBuddy 表单填写完整的 `https://sorrycode.com/v1/chat/completions` 地址；如果
  上游以后改为 Base URL 字段，必须重新实测，不能机械保留完整路径。
- 办公 Agent 任务默认开启工具调用；图片输入和思考模式只在模型、分组和客户端同时支持时
  开启。
- 自定义协议默认关闭，输入和输出参数第一次使用提供商默认值。
- 第一次验证使用空工作空间和默认权限，先验证普通回复，再验证创建一个指定文件。
- 图形界面是公开配置主路径。`models.json` 只作为本地存储事实和排障入口。

## 证据优先级

遇到界面、官方文档和历史文章不一致时，按以下顺序判断：

1. 当前桌面版中的实际行为和真实请求结果
2. WorkBuddy 当前官方文档和官方下载页
3. 当前版本的界面截图
4. 搜索摘要、旧文章和社区转述

搜索摘要只能帮助找到入口，不能单独支撑公开结论。官方文档目前可能分布在
`workbuddy.cn` 和 `codebuddy.cn`，域名本身不能替代对页面内容和更新时间的检查。

## 容易漂移的内容

| 表面 | 为什么要复查 |
| --- | --- |
| 添加模型菜单和字段名称 | 上游可能调整入口、顺序或翻译 |
| 接口地址语义 | 字段可能从完整 endpoint 改为 Base URL |
| `models.json` 路径和格式 | 本地配置位置属于客户端实现细节 |
| 工具、图片和思考开关 | 复选框存在不代表所选模型具备对应能力 |
| 默认权限和完全访问 | 沙箱边界可能随版本变化 |
| 登录、安装和系统支持 | 下载入口与平台范围会变化 |
| 自带额度和自定义模型计费 | 属于产品政策，不能长期从旧文档推断 |
| 官方文档链接 | WorkBuddy 和 CodeBuddy 文档域名可能继续调整 |

公开文章不写死非必要的按钮坐标、内部 JSON schema 或易变产品政策。只有用户完成当前任务
确实需要时，才保留版本相关细节。

## 维护节奏

### 每月轻量巡检

- 查看 WorkBuddy 当前版本和官方下载入口。
- 确认“自定义 / Custom”仍存在，字段含义没有改变。
- 检查三篇公开页面引用的官方链接是否仍可访问。
- 对照现有截图，判断它是否仍能帮助用户找到入口。
- 没有用户可见变化时，不为了刷新日期修改文章。

### 触发式完整验证

出现以下任一情况时，执行完整验证：

- WorkBuddy 更新了模型、权限、工作空间或工具调用行为。
- 用户报告 `401`、`404`、模型不可用、只能聊天或不能创建文件。
- SorryCode 调整了模型分组、模型 ID 或 OpenAI-compatible 协议入口。
- 准备新增 WorkBuddy 专题页面或更换关键截图。

完整验证使用一把可撤销的 WorkBuddy 专用 Key 和一个可删除的空目录：

1. 用该 Key 请求 `/v1/models`，记录实际可见的模型 ID。
2. 通过图形界面添加自定义模型，不手改 `models.json`。
3. 验证一次固定文本回复。
4. 在空工作空间创建一个指定 Markdown 文件，并确认没有修改其他文件。
5. 验证默认权限下的越界操作会要求确认。
6. 只有相关公开页面需要时，才额外验证图片输入、思考模式或 Skill。
7. 测试结束后删除或轮换临时 Key，并清理测试目录。

测试过程中的 Key、请求日志、账号信息和本机绝对路径不得进入仓库。

## 新页面的收录门槛

WorkBuddy 出现新功能，不等于 SorryCode 应立即增加新文章。新增页面必须同时满足：

- 它解决一个独立、稳定且能被用户说清楚的问题。
- 通过 SorryCode 的模型链路已经实测，不只是使用 WorkBuddy 自带模型。
- 它不能由现有三篇文章增加一个小节解决。
- 可以写清准备条件、最短路径、成功标志、失败边界和上游参考。

候选方向按当前优先级维护，但不是交付承诺：

1. WorkBuddy Skills：安装、来源、安全边界以及通过 SorryCode 模型调用的验证。
2. 办公任务路线：文档、表格和演示等高频交付，优先做路线图，不按每个按钮建页。
3. 微信助理和定时任务：先确认入口、持续运行条件、隐私边界和 SorryCode 请求链路。
4. MCP、知识库和外部集成：只有形成稳定配置 contract 后再公开。

不要把官方功能列表直接变成 SorryCode 的文章目录。

## 更新公开内容时

1. 先更新本文件中的当前事实或维护边界，不追加调试流水账。
2. 更新对应中文页面，再同步英文页面的事实、步骤和边界。
3. 界面实质变化时更新截图；纯视觉变化不必追图。
4. 新增或改名页面时同步 `articles/runtime/index.json` 和根 `index.json`。
5. 运行 JSON、站内链接、标点和 `git diff --check` 校验。

已完成的历史调查不在本文件持续堆叠。需要保留的只有当前结论、重新验证方法和影响未来
维护的决策。

## 上游入口

- WorkBuddy 官网：<https://www.workbuddy.cn/>
- 第一个任务：<https://www.workbuddy.cn/docs/workbuddy/FirstTask>
- 模型配置：<https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model>
- 权限模式：<https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes>
