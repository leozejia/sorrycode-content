---
title: Plugins 和 Skills 有什么区别
slug: plugins-vs-skills
order: 1
summary: Plugins 给 agent 提供新工具，Skills 教 agent 怎么做事。两者的适用场景、安装方式和调用语法不同。
section: runtime
section_title: 模型与工作台
section_order: 10
group: general
group_title: 通用
group_order: 40
---

# Plugins 和 Skills 有什么区别

如果你在 Codex 或 Claude Code 里看到 Plugins 和 Skills，可能会困惑它们的关系。

**简单回答：**

- **Plugins** 是给 agent 提供**新工具**的扩展（如操作浏览器、控制桌面）
- **Skills** 是教 agent **怎么做事**的工作流（如生成图片、排版文档）
- **它们不互斥** - 某些能力可以同时有 Plugin 和 Skill 两种形态

<h2 id="quick-comparison">快速对比</h2>

| 维度 | Plugins | Skills |
|------|---------|--------|
| **本质** | 系统级工具扩展 | 工作流知识包 |
| **提供什么** | 新的能力（如浏览器控制） | 做事的方法（如生成图片的流程） |
| **调用方式** | `@PluginName`（如 `@Chrome`） | 自然语言（如"请用 Kami..."） |
| **安装方式** | UI 可视化安装 或 配置文件 | `npx skills install` 或 让 agent 安装 |
| **适用范围** | Codex App, Claude Code (CLI & Desktop) | Codex 和 Claude Code 通用 |

<h2 id="what-are-plugins">Plugins 是什么</h2>

Plugins 是给 agent 提供新工具的扩展。

**常见 Plugins：**

- **@Chrome** - 操作真实 Chrome 浏览器（需要登录态的网站）
- **@Computer** - 操作桌面系统（系统设置、权限检查）
- **@Browser** - 测试本地网页（localhost 调试）
- **Spreadsheets** - 创建和编辑电子表格
- **Presentations** - 创建和编辑演示文稿
- **Documents** - 创建和编辑文档

**调用示例：**

```text
@Chrome 打开 X，帮我读这条帖子
@Computer 打开系统设置，检查屏幕录制权限
@Browser 打开 http://localhost:3000，测试登录流程
```

<h2 id="what-are-skills">Skills 是什么</h2>

Skills 是教 agent 怎么做事的工作流知识包。

**常见 Skills：**

- **SorryCode Image2** - 生成图片的流程和规范
- **Kami** - 排版一页纸的方法
- **Office Docs** - 处理 Word、Excel、PowerPoint 的工作流
- **Waza** - 代码审查的步骤
- **Ponytail** - 设计工作流（同时也有 Plugin 形态）

**调用示例：**

```text
请用 SorryCode Image2 生成一张封面
请用 Kami 把这份内容做成一页纸
请用 Waza 检查这次改动
```

<h2 id="key-difference">关键区别</h2>

### Plugins：提供工具

Plugins 给 agent **新的能力**，就像给人类装上机械臂、给汽车加装雷达。

**例子：**
- 没有 Chrome Plugin：agent 无法操作真实浏览器
- 装了 Chrome Plugin：agent 可以控制你的 Chrome，操作已登录的网站

### Skills：提供方法

Skills 教 agent **怎么用工具**，就像教人类如何开车、如何做菜。

**例子：**
- 没有 Kami Skill：agent 不知道如何排版一页纸
- 装了 Kami Skill：agent 知道一页纸的布局规则、字体选择、信息层级

### 它们可以共存

某些能力可以同时有 Plugin 和 Skill：

**例如 Ponytail：**
- **Ponytail Plugin**：提供设计工具的底层能力
- **Ponytail Skill**：教 agent 如何使用这些工具完成设计任务

<h2 id="installation">如何安装</h2>

### Codex App 安装 Plugins

**方式 1：可视化界面（推荐）**

1. 打开 Codex App
2. 点击侧边栏的「插件」
3. 浏览 Featured、Productivity 等分类
4. 点击插件旁边的「Try in chat」或安装按钮
5. 已安装的插件会显示在「已安装」区域

**方式 2：配置文件（备用）**

如果可视化界面不可用，可以手动编辑：

```text
~/.codex/config.toml
```

加入：

```toml
[plugins."chrome@openai-bundled"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true
```

保存后重启 Codex App。

**额外依赖：**
- Chrome Plugin 需要安装 [Codex Chrome Extension](https://chromewebstore.google.com/detail/codex/hehggadaopoacecdllhhajmbjkdcmajg)
- Computer Use 需要授予 macOS 屏幕录制和辅助功能权限

### Claude Code Desktop 安装 Plugins (Beta)

**注意：此功能目前处于 Beta 状态。**

1. 打开 Claude Code Desktop
2. 进入 Settings > Plugins & skills
3. 在「PLUGIN MARKETPLACES」区域
4. 添加 Git repository 作为插件源
5. 插件会安装到 `/Library/Application Support/Claude/org-plugins`

### 安装 Skills

**命令行安装：**

```bash
npx skills install <skill-name>
```

**让 agent 安装：**

```text
请帮我安装 SorryCode Image2 这个 skill
```

**卸载：**

```bash
npx skills remove --global <skill-name>
```

<h2 id="compatibility">兼容性</h2>

| Runtime | Plugins | Skills |
|---------|---------|--------|
| Codex App | ✅ 完整支持 | ✅ 完整支持 |
| Codex CLI | ⚠️ 部分支持 | ✅ 完整支持 |
| Claude Code CLI | ✅ 完整支持 | ✅ 完整支持 |
| Claude Code Desktop | 🧪 Beta 支持 | ✅ 完整支持 |
| Claude Desktop | ❌ 不支持 | ❌ 不支持 |

**说明：**

- Plugins 在 Codex App 和 Claude Code CLI 中支持最完善
- Claude Code Desktop 的 Plugins 支持处于实验阶段
- Skills 基于开放标准（open agent skills standard），跨 runtime 通用
- Claude Desktop 只支持第三方推理网关，不支持 Plugins 和 Skills

**Claude Code CLI 中使用 Plugins：**

```bash
# 查看可用的 plugin 命令
/plugin

# 管理 Claude Code plugins
/plugin (plugins)

# 激活待处理的 plugin 更改
/reload-plugins
```

<h2 id="when-to-use">什么时候用哪个</h2>

### 用 Plugins 的场景

- 需要操作真实浏览器（而不是无头浏览器）
- 需要用到已登录的网站（X、GitHub、Gmail）
- 需要操作桌面应用或系统设置
- 需要访问特定系统级能力

### 用 Skills 的场景

- 需要可复用的工作流（设计、文档、代码审查）
- 需要跨 runtime 使用（Codex 和 Claude Code 都能用）
- 希望团队统一工作标准
- 反复做同一类任务，希望 agent 记住方法

### 两者一起用

它们不冲突，可以组合使用：

```text
示例工作流：
1. 用 @Chrome 登录 Figma，导出设计资产
2. 用 SorryCode Image2 Skill 生成品牌一致的配图
3. 用 Office Docs Skill 把内容排版成文档
4. 用 @Browser 预览最终效果
```

<h2 id="technical-difference">技术层面的区别</h2>

### Plugins

- **安装位置**：系统级（Codex App）或组织级（Claude Code Desktop）
- **启动时机**：全局启用，runtime 启动时加载
- **权限需求**：可能需要系统权限（屏幕录制、辅助功能、浏览器扩展）
- **调用语法**：`@PluginName`
- **本质**：系统级能力扩展

### Skills

- **安装位置**：`~/.agents/skills/` 或项目 `.agents/skills/`
- **结构**：`SKILL.md`、`description`、`references/`、`scripts/`、`assets/`
- **加载机制**：Progressive disclosure（先看 description，需要时才加载完整内容）
- **调用语法**：自然语言或显式点名
- **本质**：工作流知识包

<h2 id="why-both">为什么需要两种机制</h2>

**Plugins：能力边界**

有些事情 agent 做不了，不是因为它不知道怎么做，而是因为它**物理上没有这个能力**。

例如：
- agent 无法操作你的 Chrome（除非装 Chrome Plugin）
- agent 无法控制桌面（除非装 Computer Use Plugin）

**Skills：知识边界**

有些事情 agent 能做，但**不知道你的工作流和标准**。

例如：
- agent 会生成图片，但不知道你的品牌规范
- agent 会写代码，但不知道你的审查标准

**两者解决不同问题：**

| 问题类型 | 解决方案 |
|---------|---------|
| agent 做不了 | 装 Plugin 提供新能力 |
| agent 不知道怎么做 | 装 Skill 提供工作流 |
| agent 能做但不稳定 | 装 Skill 统一标准 |

<h2 id="with-mcp">Plugins、Skills 和 MCP 的关系</h2>

三者定位不同但可以组合：

- **Plugins** - 系统级工具（浏览器、桌面、专用服务）
- **Skills** - 工作流知识（如何完成任务）
- **MCP** - 数据连接协议（读数据库、调 API）

**组合示例：**

```text
完整工作流：
1. 通过 MCP 读取数据库中的客户数据
2. 用 @Chrome Plugin 登录 CRM 系统
3. 用 DBSkill 分析数据并生成报告
4. 用 Office Docs Skill 排版成文档
```

<h2 id="common-questions">常见问题</h2>

### Codex App 通过 API 登录后能用 Plugins 吗？

**可以。** Plugins 是本地能力扩展，不依赖 Codex 官方账号。

### 为什么有些能力既是 Plugin 又是 Skill？

因为它们解决不同层次的问题：
- **Plugin 层**：提供底层能力
- **Skill 层**：提供工作流指导

### Claude Code Desktop 的 Plugins 功能稳定吗？

**目前是 Beta 状态。** 建议：
- 生产环境优先使用 Skills
- 实验性工作可以试用 Plugins (Beta)

### 如何判断我需要 Plugin 还是 Skill？

问自己：
- agent 能不能做？→ 不能 → 需要 Plugin
- agent 知不知道怎么做？→ 不知道 → 需要 Skill
- agent 做得稳不稳定？→ 不稳定 → 需要 Skill

<h2 id="next">接下来</h2>

**如果你想安装 Plugins：**

- Codex App 用户：打开侧边栏「插件」，可视化浏览和安装
- Claude Code CLI 用户：使用 `/plugin` 命令管理插件
- Claude Code Desktop 用户：Settings > Plugins & skills（Beta 功能）

**如果你想安装 Skills：**

- 看 [Skills / 精选 Skills](/docs/skills/featured-skills) 找合适的 skill
- 或者看 [让 AI 记住工作方法](/docs/agent-memory/remember-skills) 了解如何制作自己的 skill
