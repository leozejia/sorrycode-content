# SorryCode Content IA

更新时间：2026-08-07

这份文档定义 `sorrycode-content` 的内容维护边界。它是内容团队内部文档，不进入线上 docs。

`sorrycode` 线上只读取：

- `index.json`
- `articles/<section>/index.json`
- `articles/<section>/<slug>/<locale>.md`
- article 同目录下的公开图片资源

`docs/` 只放内部治理文档，例如 IA、页面 contract、收录标准和维护边界。不要把 `docs/` 路径写进公开 index。

公开图片资源的具体使用规范见 `docs/public-article-assets.md`。封面、截图和正文插图都必须先满足那里定义的同目录、格式、大小和隐私边界。

## 仓库分工

```text
sorrycode-content/articles/   公开正文和公开图片资源
sorrycode-content/docs/       内容团队内部治理，不对外展示
sorrycode                     产品站、renderer、proxy、cache、安全校验和发布边界
```

`sorrycode` 不再维护公开正文，也不承载具体 skill 的长期内容策略。除非改变 renderer、后端代理、缓存、安全校验或内容源 contract，否则内容 IA 的细节先在本仓库维护。

## 一级栏目职责

| 栏目 | 回答的问题 | 写法 |
| --- | --- | --- |
| 开始使用 | SorryCode 适合谁，如何创建 Key、验证链路和理解成本 | 第一章，先给默认路径，再提供必要的平台参考 |
| 模型与工作台 | 不同供应商生态的工作台、模型和媒体能力怎么用 | 按供应商生态分组，执行路径必须闭环 |
| Skills | 装好 runtime 后，给 agent 增加什么能力 | 能力选择、安装、触发、边界 |
| 工具 | 独立工具链或工作台怎么用 | 初始化、使用、适用边界 |
| Agent 基建 | 长期上下文、AGENTS.md、CLAUDE.md、DESIGN.md、MCP、Skills 这些长期标准是什么 | 原理、标准、可长期引用 |
| 环境准备 | 多个路径共用的稳定前置 | 少量共享准备 |
| 排障 | 共性错误怎么分型和修复 | 错误现象、原因、下一步 |

交叉是正常的。比如做 PPT 会经过 `Skills`、`工具` 和 `办公文档`。治理目标不是消灭交叉，而是避免同一段解释在多个页面重复。

## 页面职责

### Skills

`Skills` 是能力选择和能力说明。它回答“我应该装哪个 skill，装完怎么触发”。

单个 skill 页只讲这个 skill：

- 它是什么
- 适合什么
- 不适合什么
- 怎么安装
- 第一话怎么说
- 常见问题
- 上游参考

如果某个任务域里有多个 skill，比如 PPT，不要把其中一个 skill 写成整个任务域。先做路线图，再写单个 skill。

Skills 安装采用 agent-first 口径：先让用户把 `Codex` 或 `Claude Code` 跑起来，再把安装环境和 skill 安装交给 agent 处理。公开文档可以给用户一段可复制的话，让 agent 读取当前机器可读 Markdown 后动态判断安装范围。

维护规则：

- 给 agent 的链接使用 `/docs/<section>/<slug>.md?locale=...` 或 `/llms.txt`，不要使用普通 SPA 页面作为唯一入口。
- 不在 `Skills 是什么` 或单个 skill 页写死“默认安装清单”；skills 会增长，推荐关系应通过当前 section index、分类页和单个文章维护。
- 单个 skill 页不重复解释 `Node.js / Git / Homebrew / PowerShell` 等共享环境。共享环境只在 runtime、环境准备或排障页按需承接。
- 如果用户不知道装什么，agent 应先读当前 Skills 分类和相关文章，再按用户目标决定，而不是凭历史记忆安装旧组合。

### Tools

`Tools` 放项目型工具链和独立工作台。判断标准是：用户第一步是不是初始化或使用一个工具，而不是安装一个全局 skill。

`Open Slide`、`HyperFrames`、`Open Design` 这类页面放在 Tools。它们可以被 Skills 页面引用，但不要伪装成普通 skill。

### 开始使用、模型与工作台和 Agent 基建

`开始使用` 同时承担第一次上手和必要的平台参考。`模型与工作台` 写具体供应商生态的
工作台、模型和媒体能力。`Agent 基建` 写长期标准和协议。

不要把某个 skill 的详细工作流写进这些栏目。

`开始使用` 作为第一章，文章保持分工，不合并成一篇长文：

- `第一次使用 SorryCode`：只做 Agent 工具分流，不重复各工具的安装和首次任务；
- `SorryCode 适合谁`：回答用户定位、余额制价值、订阅制取舍；
- `创建 API Key`：完成实际配置；
- `首条请求`：提供手动验证和排障入口；
- `AI 成本怎么计算`：解释 input、output、cache 和倍率。

`工具不是模型` 继续放在核心概念，回答工作台、模型、API Key、Base URL 的关系。
安装页和首条请求页只负责执行路径，不再承担商业定位或成本科普。

`articles/runtime/` 的公开展示名是“模型与工作台 / Models & Runtimes”，URL 保持
`/docs/runtime/*`。导航按供应商生态组织，当前文章和分组以 `articles/runtime/index.json`
为准。不要创建没有文章的空供应商分组。新增供应商页面前，先确认用户入口、模型、
接口和生产验证。

Codex 相关页面按下面分工：

- `Codex` 负责安装、API Key、Base URL 和第一次使用；
- `在 Codex CLI 和 App 中切换 SorryCode 模型` 负责说明 CLI 显式模型、官方 profile，以及 App 修改顶层默认模型并重启的当前操作方式；
- 多模型页只写 Codex 原生使用路径。provider 始终保持 `sorrycode`，不承载旧方案迁移说明。App 需要明确模型选择器的限制、完整退出要求、恢复 GPT 的方法和用量记录验证方式。

WorkBuddy 只维护一篇闭环页面，包含下载安装、SorryCode 自定义模型配置、第一个文件任务和
Expert / Expert Team 入口及必要的权限边界。不要为通用安全常识、单个菜单或尚未形成稳定用户问题的功能单独建页。
UI 是自定义模型的公开配置路径，不公开讲解本地配置文件格式。

`Pi + DeepSeek` 独立放在 DeepSeek 生态下，官方项目固定为 `pi.dev` / `earendil-works/pi`。
页面只维护 Pi 安装、SorryCode 自定义 provider、DeepSeek 模型选择和首次工具调用验证，不扩展成通用 Pi 教程。

`Agent 能力是怎么扩展的` 负责解释 Runtime、Expert / Agent、Skill、MCP / Tool / Connector
和 Plugin 的层级关系。Plugin 是特定 runtime 的打包与分发单元，不是 Tool 的同义词；
Expert 是角色与协作机制，不是权限来源。各产品的安装和配置步骤留在对应 runtime 页面，
通用概念页不维护跨产品兼容性表。

模型使用页只承接当前模型的选择、参数、提示方法和验证边界，不重复 runtime 的安装步骤：

- `GPT-5.6 Sol 怎么用`：解释模型定位、reasoning effort、精简提示词、工具调用和长上下文边界；
- `Claude Fable 5 怎么用`：解释模型定位、effort、长程任务、自治边界、子 Agent 和旧规则迁移；
- 安装、API Key 和 Base URL 继续由 `Codex`、`Claude Code` 和 `首条请求` 页面负责。

`Agent 基建 / 强模型的项目规则怎么写` 负责审计 `AGENTS.md`、`CLAUDE.md` 和常驻 Skills。
它不重复基础规则文件和 Skills 教程，只讲强模型下哪些规则应保留、哪些规则需要用同一组
代表性任务逐批删减。

图片能力按供应商页面维护，不在“开始使用”中另建图片总览：

- `GPT Image 2` 同时承接 Codex 自然语言生图、显式 Images API 和
  `SorryCode Image2` Skill 分流；
- `Grok 图片生成` 只讲经过生产验证的 xAI-compatible Images API；
- `Grok 视频生成` 只讲文生视频、图生视频和异步轮询；未采用的 edit / extension
  不进入公开文档。

`SorryCode Image2` Skill 保持独立，只负责 `gpt-image-2` 的可复现执行流程，并链接回
`模型与工作台 / GPT Image 2`。更多素材生产和视觉资产工作流仍可指向 `sorryassets.com`，
但不在 SorryCode 文档里展开其私有模型、价格或接口。

## API Key 表达规则

公开文档先讲协议和分组权限，再讲工具如何使用 Key：

- 能否复用一把 Key，取决于它所属分组是否开放目标模型，以及该工具使用的协议和接口是否兼容；不是按工具名称强制一对一分配。
- 兼容的工具可以共用一把 Key。按工具或用途分开创建 Key，是为了更清晰地统计用量、设置限额、排查问题或轮换凭证。
- Kimi Code、Grok CLI、Grok 图片、Grok 视频和 GPT Image 2 仍要分别说明所需的模型、协议和分组权限；不要把“需要匹配分组”写成“必须创建专用 Key”。
- REST API 示例直接在请求头中提供可替换的分组 Key 占位值，不要求用户先设置通用环境变量。
- runtime 一键安装器负责保存当前工具选择的 Key。公开页面不要求用户手动同步安装器内部的变量名。
- 只有具体 Skill 确实依赖环境变量时，才在该 Skill 页面公开变量名。当前 `SORRYCODE_API_KEY` 只属于 `SorryCode Image2` 的配置 contract。

不要把一个通用变量名写成 SorryCode 全局 Key，也不要仅凭 `sk-...` 判断不同分组的 Key 可以互换。

## 执行型教程的 Agent 提示

安装、终端命令、配置文件、API 接入和首次验证等执行型教程，在导语之后、第一个二级标题之前放一次统一的 Agent 提示。概念、模型介绍、成本说明和路线选择页不放。

GUI 教程只能承诺 Agent 完成可以安全执行的步骤，并列出需要用户手动确认的操作。手动步骤必须继续保留，用于核对、排障和 Agent 无法执行时的备用路径。

站点当前提供“复制 Markdown”，没有单独的“复制链接”按钮。公开正文可以提示用户发送本页链接，但不要把它写成站内按钮。

中文固定文案：

```markdown
> **交给 Agent 配置**
>
> 点击右上角的「复制 Markdown」，把内容发给你正在使用的 Agent。让它根据当前环境完成可以自动执行的配置和验证，并列出需要你手动确认的步骤。Agent 能读取网页时，也可以直接发送本页链接。不要在对话中粘贴 API Key。
```

英文固定文案：

```markdown
> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.
```

## 内容更新顺序

涉及栏目、页面定位或配置口径时，先更新本仓库 `docs/` 下的内部决议，再改中英文公开正文，最后同步 section index 和根 `index.json`。只有改动影响 renderer、内容代理、缓存、安全校验或内容源读取规则时，才需要同步修改 `sorrycode` 的架构文档。

## 命名、路径和 IA 改造策略

名称、slug、目录、栏目、导航分组或页面定位不准确时，默认硬切。删除旧路径，不保留兼容入口、重定向或隐藏保底页，站内链接和索引在同一批改完。

公开文档不是不可变 API，长期结构正确性优先于旧链接连续性。具体执行顺序和检查项见 `docs/operator-restructuring-guide.md`。

## 收录原则

公开 docs 不是 marketplace。只收录我们读过、试过、愿意解释的工具或 skill。

收录一个社区 skill 前，至少确认：

- 上游是公开可访问的仓库。
- 安装命令能被解释清楚。
- 站内第一句示例能稳定触发。
- 页面能讲清适合和不适合的场景。
- 上游明显破坏时，SorryCode 能更新说明、隐藏入口或切换到稳定版本。

站内不要搬运上游完整 README。站内负责选择、安装、触发、边界和最近验证口径；上游负责最新能力细节。
