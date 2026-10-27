# SorryCode Content IA

更新时间：2026-10-27

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
| AGENTS | 怎么接入 SorryCode，安装 Agent 并完成第一个任务 | 默认用 Magpie 图形界面配置，不按厂商分组 |
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
- 单个 skill 页不重复解释 `Node.js / Git / Homebrew / PowerShell` 等共享环境。共享环境只在环境准备或排障页按需承接，不作为桌面 Agent 的通用前置。
- 如果用户不知道装什么，agent 应先读当前 Skills 分类和相关文章，再按用户目标决定，而不是凭历史记忆安装旧组合。

### Tools

`Tools` 放项目型工具链和独立工作台。判断标准是：用户第一步是不是初始化或使用一个工具，而不是安装一个全局 skill。

`Open Slide`、`HyperFrames`、`Open Design` 这类页面放在 Tools。它们可以被 Skills 页面引用，但不要伪装成普通 skill。

### 开始使用、AGENTS 和 Agent 基建

`开始使用` 给出唯一默认上手路线和必要的平台参考。`AGENTS` 负责 Magpie 配置与 Agent 首次使用。`Agent 基建` 写长期标准和协议。

不要把某个 skill 的详细工作流写进这些栏目。

`开始使用` 作为第一章，文章保持分工，不合并成一篇长文：

- `第一次使用 SorryCode`：按创建 Key、Magpie 配置、安装并启用 Agent、首次任务的顺序引导；不知道选什么时默认 Codex，不先让用户比较所有工具；
- `SorryCode 适合谁`：回答用户定位、余额制价值、订阅制取舍；
- `创建 API Key`：只讲创建、分组、限额和密钥安全，创建后前往 Magpie，不重复各工具配置；
- `首条请求`：提供手动验证和排障入口；
- `AI 成本怎么计算`：解释 input、output、cache 和倍率。

`工具不是模型` 继续放在核心概念，回答工作台、模型、API Key、Base URL 的关系。
安装页和首条请求页只负责执行路径，不再承担商业定位或成本科普。

`articles/agents/` 的公开展示名在中英文中均为 `AGENTS`，URL 为 `/docs/agents/*`。导航平铺，不按 OpenAI、Anthropic 等厂商分组。默认六篇：

1. 用 Magpie 配置 SorryCode
2. Codex
3. Claude Code
4. DeepSeek Harness
5. WorkBuddy
6. 其他 Agents

原 `runtime` 栏目硬切删除，不保留旧正文、兼容路由或重定向。

`Magpie` 页面只说明通过图形界面接入 SorryCode 的最短路径：从官网安装、按 SorryCode 模型分组分别添加自定义供应商和对应 API Key、获取模型，然后在 Agent 面板启用。不要在这篇入门文档维护未经当前界面验证的 CLI、场景、账号轮换或工具兼容性说明。

各 Agent 页只保留官方安装入口、在 Magpie 启用、打开工作目录和一个首次任务。Codex、DSH、WorkBuddy 默认走桌面端；Claude Code 按当前官方终端安装方式说明，不混同 Claude Desktop。换模型回 Magpie 操作，不在各页维护手写配置、环境变量或第二套 SorryCode 安装器。

OpenCode、Pi、Kimi Code、Grok Build 和 Cursor 合并到“其他 Agents”，只保留官方下载入口与必要边界。Cursor CLI、普通编辑器和 Cursor Private Inference 必须区分，不把某一种形态的支持推及全部产品。Magpie 不显示或不支持的客户端，不承诺能一键接入。

不再维护具体模型版本的独立使用页或完整型号清单。模型选择以当前分组返回的目录为准，不因型号迭代新增入门文章。

取消独立的“Agent 能力是怎么扩展的”文章。稳定的 Skill、MCP、Plugin 与权限关系只在已有工作方法页面简要说明，不作为上手前置。

`Agent 基建 / 强模型的项目规则怎么写` 负责审计 `AGENTS.md`、`CLAUDE.md` 和常驻 Skills。
它不重复基础规则文件和 Skills 教程，只讲强模型下哪些规则应保留、哪些规则需要用同一组
代表性任务逐批删减。

图片任务通过已有的 `SorryCode Image2` Skill 承接。删除 GPT Image 2 / 2.5、Grok 图片与视频的独立模型/API 教程，引用同时改为可执行的任务入口或删除。不把原始 API 说明搬到 Skills 凑篇数。

Magpie 接入不等于 Agent 自动获得生图或视频工具。Skills 需要的凭证、工具与权限仍须单独满足；没有稳定任务入口的能力不进入默认推荐。

更多素材生产和视觉资产工作流仍可指向 `sorryassets.com`，但不在 SorryCode 文档里展开其私有模型、价格或接口。

## API Key 表达规则

公开文档先讲协议和分组权限，再讲工具如何使用 Key：

- 能否复用一把 Key，取决于它所属分组是否开放目标模型，以及该工具使用的协议和接口是否兼容；不是按工具名称强制一对一分配。
- 兼容的工具可以共用一把 Key。按工具或用途分开创建 Key，是为了更清晰地统计用量、设置限额、排查问题或轮换凭证。
- Magpie 按 SorryCode 分组分别添加供应商和对应 Key。同一兼容分组可供多个 Agent 使用，不要把“需要匹配分组”写成“每个 Agent 必须创建专用 Key”。
- REST API 示例直接在请求头中提供可替换的分组 Key 占位值，不要求用户先设置通用环境变量。
- 默认由 Magpie 管理 Agent 的接入配置。控制台已有接入工具不在本轮删除，但不再作为公开入门文档的竞争默认路线。
- 只有具体 Skill 确实依赖环境变量时，才在该 Skill 页面公开变量名，并区分 Skill 凭证与 Magpie 接入。手动 API 排障示例使用 Bearer Token 占位值，不引入通用密钥环境变量。
- 手动 API 排障示例使用当前分组返回的准确模型 ID，不把 Magpie 本地生成的供应商前缀拼进直连请求。
- 不复制持续变化的完整模型目录。模型 ID、能力和思考档位以当前分组与实际请求验证为准。

不要把一个通用变量名写成 SorryCode 全局 Key，也不要仅凭 `sk-...` 判断不同分组的 Key 可以互换。

## 执行型教程的 Agent 提示

需要已有 Agent 执行安装脚本、配置文件或 API 验证的教程，在导语之后、第一个二级标题之前放一次统一的 Agent 提示。首次接入的 Magpie 图形界面、Agent 安装与开始使用页不放，避免要求尚未装好 Agent 的用户先交给 Agent 配置。概念、成本说明和路线选择页也不放。

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
