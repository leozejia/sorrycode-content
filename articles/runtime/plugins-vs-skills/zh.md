---
title: Plugins 和 Skills 有什么区别
slug: plugins-vs-skills
order: 4
summary: Plugins 给 agent 提供新工具，Skills 教 agent 怎么做事——两者适用场景、安装方式、调用语法完全不同。
section: runtime
section_title: Runtime
section_order: 10
---

# Plugins 和 Skills 有什么区别

如果你在 Codex 或 Claude Code 里看到 Plugins 和 Skills，可能会困惑它们是不是一回事。

**简单回答：**

- **Plugins** 是给 agent 提供新工具的扩展，比如操作浏览器、控制桌面、制作视频
- **Skills** 是教 agent 怎么做事的手册，比如生成图片、排版文档、审查代码

一个扩展能力边界，一个传授工作方法。

<h2 id="quick-comparison">快速对比</h2>

| 维度 | Plugins | Skills |
|------|---------|--------|
| **本质** | 系统级能力扩展 | 工作流操作手册 |
| **适用范围** | 主要是 Codex App | Codex 和 Claude Code 通用 |
| **调用方式** | `@Chrome`、`@Computer` | 自然语言，如"请用 Kami..." |
| **安装方式** | 修改配置文件 + 重启 | `npx skills install` |
| **典型场景** | 操作浏览器、桌面、专用服务 | 内容创作、文档处理、代码审查 |

<h2 id="what-are-plugins">Plugins 是什么</h2>

Plugins 是 Codex 特有的外部能力扩展。它们让 agent 可以操作浏览器、控制桌面、或者连接专用服务。

**常见 Plugins：**

- **@Chrome** - 操作真实 Chrome 浏览器，适合需要登录态的网站（X、GitHub、Gmail、Stripe）
- **@Browser** - 测试本地网页，适合 localhost 调试、截图、表单流程验证
- **@Computer** - 操作桌面系统，适合系统设置、权限检查、桌面应用
- **@HyperFrames** - 制作 HTML 视频和动效

**调用示例：**

```text
@Chrome 打开 X，帮我读这条帖子
@Browser 打开 http://localhost:3000，测试登录流程
@Computer 打开系统设置，检查屏幕录制权限
@HyperFrames 做一个 10 秒产品介绍视频
```

**技术特点：**

- 需要在 `~/.codex/config.toml` 配置后重启 Codex App
- Chrome 需要安装扩展和 native host
- Computer Use 需要授予系统屏幕录制和辅助功能权限
- 全局启用，runtime 启动时加载

<h2 id="what-are-skills">Skills 是什么</h2>

Skills 是可安装、可复用的工作流能力包。它们教 agent 如何处理特定类型的任务，但不改变 agent 的基础工具集。

**常见 Skills：**

- **SorryCode Image2** - 生成图片、设计封面、制作配图
- **Kami** - 把内容排版成一页纸
- **Office Docs** - 编辑 Word、Excel、PowerPoint
- **Waza** - 代码审查、提交前检查
- **DBSkill** - 商业诊断、竞品分析

**调用示例：**

```text
请用 SorryCode Image2 生成一张封面
请用 Kami 把这份内容做成一页纸
请用 Waza 检查这次改动
```

**技术特点：**

- 基于开放标准（open agent skills standard），Codex 和 Claude Code 都支持
- 通过 `npx skills install` 安装到 `~/.agents/skills` 或项目 `.agents/skills`
- Progressive disclosure：agent 先看 description，需要时才加载完整 SKILL.md
- 可能包含脚本、模板、字体、示例文件

<h2 id="when-to-use">什么时候用哪个</h2>

### 用 Plugins 的场景

- 需要操作真实浏览器，而不是无头浏览器
- 需要用到已登录的网站（X、GitHub、Gmail、Stripe、Google Cloud Console）
- 需要操作桌面应用或系统设置
- 需要多标签页协同、截图、表单自动化
- 需要制作 HTML 视频或动效

### 用 Skills 的场景

- 需要可复用的业务工作流（设计、文档、代码审查）
- 需要跨 runtime 通用的能力（Codex 和 Claude Code 都能用）
- 团队协作需要统一工作标准
- 反复要求 agent 做同一类事，希望它记住方法
- 需要传授领域知识或操作规范

<h2 id="installation">安装方式对比</h2>

### Plugins 安装

Plugins 主要在 Codex App 里配置。

编辑配置文件：

```text
~/.codex/config.toml
```

加入这段：

```toml
[plugins."browser-use@openai-bundled"]
enabled = true

[plugins."chrome@openai-bundled"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true

[plugins."hyperframes@openai-curated"]
enabled = true
```

保存后完全退出并重启 Codex App。

**额外依赖：**

- Chrome 需要安装 [Codex Chrome Extension](https://chromewebstore.google.com/detail/codex/hehggadaopoacecdllhhajmbjkdcmajg) 和 native host
- Computer Use 需要授予 macOS 屏幕录制和辅助功能权限

### Skills 安装

Skills 可以通过命令行安装，也可以让 agent 自己读文档安装。

**命令行安装：**

```bash
npx skills install <skill-name>
```

**让 agent 安装：**

```text
请帮我安装 SorryCode Image2 这个 skill
```

Agent 会自动判断当前环境、检查依赖、执行安装。

安装完成后，重启 Codex 或 Claude Code 即可使用。

**卸载：**

```bash
npx skills remove --global <skill-name>
```

<h2 id="compatibility">兼容性</h2>

| Runtime | Plugins | Skills |
|---------|---------|--------|
| Codex App | ✅ 支持 | ✅ 支持 |
| Codex CLI | ⚠️ 部分支持 | ✅ 支持 |
| Claude Code CLI | ❌ 不支持 | ✅ 支持 |
| Claude Code Desktop | ❌ 不支持 | ✅ 支持 |
| Claude Desktop | ❌ 不支持 | ❌ 不支持 |

**说明：**

- Plugins 是 Codex 生态专属，主要在 Codex App 里使用
- Skills 基于开放标准，跨 runtime 通用
- Claude Desktop 只支持第三方推理网关，不支持 Plugins 和 Skills

<h2 id="technical-difference">技术层面的区别</h2>

### Plugins

- 配置在 `~/.codex/config.toml`
- 全局启用，runtime 启动时加载
- 需要额外权限（浏览器扩展权限、系统权限）
- 调用语法是 `@PluginName`
- 本质是系统级能力扩展

### Skills

- 安装到 `~/.agents/skills/` 或 `.agents/skills/`
- 结构包含 `SKILL.md`、`description`、`references/`、`scripts/`、`assets/`
- Progressive disclosure：agent 先看 description 判断是否需要，需要时才加载完整内容
- 调用语法是自然语言
- 本质是工作流操作手册

<h2 id="api-login">Codex App 通过 API 登录后也能用 Plugins 吗</h2>

**可以。**

现在 Codex App 通过 API 登录（比如接入 SorryCode Gateway）后，也可以正常使用 Plugins。

配置方式和账号登录时一样：

1. 编辑 `~/.codex/config.toml`
2. 加入 Plugins 配置
3. 重启 Codex App

Plugins 是本地能力扩展，不依赖 Codex 官方账号。只要 Codex App 能正常运行，Plugins 就能用。

<h2 id="can-they-work-together">Plugins 和 Skills 可以一起用吗</h2>

**可以。**

它们不冲突。

比如你可以：

1. 用 `@Chrome` 登录 Salesforce，抓取客户数据
2. 用 DBSkill 分析这些数据，生成诊断报告
3. 用 Office Docs skill 把报告排版成 Word 文档
4. 用 SorryCode Image2 生成报告封面

Plugins 扩展能力边界，Skills 传授工作方法。两者组合可以完成更复杂的工作流。

<h2 id="with-mcp">Plugins、Skills 和 MCP 是什么关系</h2>

三者定位不同：

- **MCP（Model Context Protocol）** - 工具和数据连接协议，让 agent 可以读数据库、调 API、访问外部系统
- **Plugins** - Codex 特定的系统能力扩展，给 agent 提供浏览器、桌面、专用服务
- **Skills** - 工作流能力包，教 agent 如何处理特定类型的任务

它们可以组合：

- 一个图片 skill 可以调用 MCP 连接的图片 API
- 一个数据分析 skill 可以通过 MCP 读取数据库，再用 `@Browser` 展示可视化结果
- 一个测试 skill 可以用 `@Chrome` 操作真实浏览器，再通过 MCP 记录测试结果

<h2 id="next">接下来</h2>

**如果你想用 Plugins：**

- Codex App 用户可以直接配置 `~/.codex/config.toml`
- Claude Code 用户暂时不支持 Plugins，可以考虑使用 Skills 或 MCP

**如果你想用 Skills：**

- 先看 [Agent 基建 / Skills](/docs/agent-memory/remember-skills) 了解 Skills 标准
- 再看 [Skills / 精选 Skills](/docs/skills/featured-skills) 找到适合你的 skill
- 或者直接让 agent 读当前 Skills 列表，按你的目标推荐

**如果你不确定：**

问 agent：

```text
我想让你操作 Gmail，应该用 Plugin 还是 Skill？
我想让你每次生成图片都遵循品牌规范，应该用 Plugin 还是 Skill？
```

Agent 会根据任务特点给出建议。
