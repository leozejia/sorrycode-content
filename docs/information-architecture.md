# SorryCode Content IA

更新时间：2026-05-13

这份文档定义 `sorrycode-content` 的内容维护边界。它是内容团队内部文档，不进入线上 docs。

`sorrycode` 线上只读取：

- `index.json`
- `articles/<section>/index.json`
- `articles/<section>/<slug>/<locale>.md`
- article 同目录下的公开图片资源

`docs/` 只放内部治理文档，例如 IA、页面 contract、收录标准和维护边界。不要把 `docs/` 路径写进公开 index。

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
| 开始使用 | 第一次用 SorryCode，应该从哪走 | 路线图，低术语，按目标分流 |
| Platform | SorryCode API、Key、模型、图片接口怎么用 | 平台能力和开发者参考 |
| Runtime | 具体 AI 工作台怎么安装、启动、验证 | onboarding，必须闭环 |
| Skills | 装好 runtime 后，给 agent 增加什么能力 | 能力选择、安装、触发、边界 |
| 新手村 | 今天想完成一个具体成果，怎么走 | 任务路线，少选择，给默认路径 |
| 工具 | 独立工具链或工作台怎么用 | 初始化、使用、适用边界 |
| Agent 基建 | 长期上下文、AGENTS.md、CLAUDE.md、DESIGN.md、MCP、Skills 这些长期标准是什么 | 原理、标准、可长期引用 |
| 环境准备 | 多个路径共用的稳定前置 | 少量共享准备 |
| 排障 | 共性错误怎么分型和修复 | 错误现象、原因、下一步 |

交叉是正常的。比如做 PPT 会经过 `新手村`、`Skills`、`工具` 和 `办公文档`。治理目标不是消灭交叉，而是避免同一段解释在多个页面重复。

## 页面职责

### 新手村

`新手村` 是任务教程。它回答“我第一次想拿到一个结果，默认怎么做”。

页面应该保留：

- 任务目标
- 准备物品
- 通关步骤
- 复制这句话
- 通关标志
- 卡关怎么办
- 下一关

新手村不负责完整比较所有工具。它只给默认路径，并链接到 Skills 或 Tools 的选择页。

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

### Platform 和 Agent 基建

`Platform` 写 SorryCode 平台能力。`Agent 基建` 写长期标准和协议。

不要把某个 skill 的详细工作流写进这两类页面。

Platform 当前应拆成三层，不要合并成一篇：

- `SorryCode 适合谁`：回答用户定位、余额制价值、订阅制取舍。
- `AI 成本怎么计算`：回答底层模型消耗如何落回 input / output / cache。
- `工具不是模型`：回答工作台、模型、API Key、Base URL 的关系和默认路径。

安装页和首条请求页只负责执行路径，不再承担商业定位或成本科普。

## 公开内容更新顺序

如果只改公开正文、标题、摘要、导航分组和页面 contract：

1. 先更新本仓库 `docs/` 下的内部治理文档。
2. 再更新 `articles/` 正文。
3. 再更新 `articles/<section>/index.json` 和根 `index.json`。

只有当改动影响 `sorrycode` 的 renderer、内容代理、缓存、安全校验或内容源读取规则时，才需要同步改 `sorrycode/docs/architecture/`。

## 命名、路径和 IA 改造策略

后续文档 IA 改造默认硬切。硬切不只针对 URL，也包括公开标题、slug、目录路径、栏目归属、导航分组和页面定位。

- 发现名称不准确，就改名称。
- 发现 slug 或目录路径不准确，就改 slug 和目录路径。
- 发现栏目归属不准确，就移动到正确栏目或分组。
- 改 slug 就删除旧 slug，不保留旧 URL。
- 不为旧 article 做兼容入口、站内重定向或隐藏保底页。
- 站内链接必须一次性更新干净。
- 根 `index.json` 和 section index 不允许继续引用旧路径。
- 长期结构正确性优先于短期链接连续性。不要因为旧路径已经存在，就继续保留不准确的名称、slug、目录或栏目归属。

这条规则的目的，是避免内容仓库为了历史命名、临时分类和早期理解长期背兼容包袱。公开文档不是不可变 API，IA 应该服务当前理解和长期维护边界。

每次硬切都必须同时处理：

- `articles/<section>/<slug>/` 实际目录
- Markdown frontmatter 里的 `slug`、`title`、`summary`、`section` 和分组字段
- 根 `index.json` 里的 `slug`、`markdownPath`、`assetBaseUrl`、`route`、`title` 和 `summary`
- `articles/<section>/index.json` 里的 `articles` 和 `navigation.groups[].items`
- 全仓站内链接，例如 `/docs/<section>/<slug>`
- 必要的内部治理文档，例如本文件或专题策略文档

## 收录原则

公开 docs 不是 marketplace。只收录我们读过、试过、愿意解释的工具或 skill。

收录一个社区 skill 前，至少确认：

- 上游是公开可访问的仓库。
- 安装命令能被解释清楚。
- 站内第一句示例能稳定触发。
- 页面能讲清适合和不适合的场景。
- 上游明显破坏时，SorryCode 能更新说明、隐藏入口或切换到稳定版本。

站内不要搬运上游完整 README。站内负责选择、安装、触发、边界和最近验证口径；上游负责最新能力细节。
