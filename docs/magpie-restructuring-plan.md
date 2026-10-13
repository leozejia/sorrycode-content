# sorrycode-content 文档重构方案：magpie 时代

> 分析时间：2026-10-13  
> 原因：magpie 的出现改变了多 agent 管理范式  
> 目标：简化文档、避免重复、提升用户体验

## 核心问题

### 问题 1：每个 runtime 都在重复"如何配置 API Key"

**当前状态**：
- `claude-code/zh.md` - 完整的 API Key + 一键安装流程
- `codex/zh.md` - 完整的 API Key + 一键安装流程
- `pi-agent/zh.md` - 完整的 provider 配置流程
- `cursor/zh.md` - 完整的 API Key 配置流程
- `dsh/zh.md` - 完整的 provider 配置流程
- `kimi-code/zh.md` - 完整的 API Key 配置流程
- `workbuddy/zh.md` - 完整的 models.json 配置流程
- `opencode/zh.md` - 完整的配置流程

**问题**：
- 17 个 runtime 文档都包含类似的"准备 API Key → 一键安装 → 手动配置"流程
- 用户要学 17 种不同的配置方式
- 文档维护成本极高（API endpoint 变化要改 17 个文档）
- 用户困惑："为什么每个工具配置方式都不一样？"

### 问题 2：模型版本文档快速过时

**当前过时文档**：
- `gpt-5-6-sol/zh.md` - GPT-5.6 已经不是最新（现在是 GPT-6.1）
- 文档中提到 `gpt-5.6-sol` 作为"前沿模型"，但 `gpt-6.1-sol` 才是当前最新
- 没有找到 `gpt-6.1-sol`、`gpt-6.1-astra`、`gpt-6-luna` 的文档

**问题**：
- 模型更新快，文档跟不上
- 用户看到的是过时信息
- 没有统一的"当前推荐模型"指南

### 问题 3：缺少"统一管理"的视角

**当前文档假设**：
- 用户一次只用一个 runtime
- 用户愿意为每个 runtime 单独配置
- 用户不需要在多个 runtime 之间切换

**实际情况**：
- 用户同时用多个 runtime（Claude Code + Codex + Pi）
- 用户想要快速切换模型和场景
- 用户不想记住每个 runtime 的配置文件位置

**magpie 解决了什么**：
- ✅ 统一配置所有 runtime
- ✅ 一个命令切换模型
- ✅ 场景管理（work/fast/experiment）
- ✅ 多账号自动切换
- ✅ 统一的模型发现

---

## 重构方案

### 方案 A：新增 magpie 文档 + 重构现有文档（推荐）

#### 1. 新增文档

**新增：`articles/runtime/magpie/zh.md`**
- 位置：runtime section，新增 `magpie` group（放在 OpenAI 和 Anthropic 之前）
- 内容：
  - magpie 是什么（统一模型网关）
  - 为什么需要 magpie（解决多 runtime 管理问题）
  - 快速开始：安装 + 添加 sorrycode providers + 配置 agents
  - 场景管理：work/fast/experiment profiles
  - 多账号管理：routing groups
  - 与各 runtime 的集成
  - 故障排查

**新增：`articles/models/current-lineup/zh.md`**（新 section）
- 位置：新建 `models` section（在 `runtime` 之前）
- 内容：
  - 当前模型阵容总览
  - 高质量模型：Opus 5.5、GPT-6.1 Sol、GPT-6.1 Astra
  - 干活模型：Sonnet 5.5、DeepSeek Flash
  - 快速模型：Haiku 5.5、Gemini 3.8 Flash、Luna
  - 实验模型：Grok 4.7、GLM 5.3
  - 如何选择模型（按任务类型）
  - 模型更新记录

#### 2. 重构现有文档

**保留但简化的文档**（17 个 runtime 文档）：

每个 runtime 文档结构调整为：

```markdown
# Claude Code / Codex / Pi Agent / ...

## 什么是 XXX
[简短介绍]

## 快速开始

### 推荐：使用 magpie（统一管理）
> 如果你使用多个 AI 工具，推荐先配置 magpie。
> 
> 👉 [完整指南：使用 magpie 管理所有 AI 工具](/docs/runtime/magpie)

**用 magpie 配置 XXX**：
```bash
magpie xxx sorrycode/claude-opus-5-5
```

### 传统方式：单独配置
> 如果你只用 XXX，或者不想用 magpie，可以单独配置。

[原来的完整配置流程，但移到折叠区域]

<details>
<summary>展开：单独配置 XXX 的完整步骤</summary>

[原来的内容]

</details>

## XXX 的特色功能
[这个 runtime 独有的功能，如 Claude Code 的 computer use]

## 常见问题
[这个 runtime 特有的问题]
```

**删除的文档**（1 个）：

❌ **删除：`gpt-5-6-sol/zh.md`**
- 原因：模型版本文档快速过时
- 替代：在 `models/current-lineup` 中统一讲所有 GPT 模型
- 如果用户访问旧链接，301 重定向到 `models/current-lineup#gpt-family`

**合并的文档**（1 个）：

🔀 **合并：`codex-multi-model/zh.md` → `magpie/zh.md`**
- 原因：用 magpie 配置多模型是更简单的方式
- `codex-multi-model` 讲的是"在 Codex 里用 Grok"，magpie 完全覆盖这个场景
- 保留旧链接，301 重定向到 `magpie#multi-model`

#### 3. 更新导航结构

**`articles/runtime/index.json` 调整**：

```json
{
  "navigation": {
    "groups": [
      {
        "id": "magpie",
        "title": { "en": "Unified Management", "zh": "统一管理" },
        "items": ["magpie"]
      },
      {
        "id": "openai",
        "title": { "en": "OpenAI", "zh": "OpenAI" },
        "items": ["codex", "gpt-image-2", "gpt-image-2-5"]
      },
      {
        "id": "anthropic",
        "title": { "en": "Anthropic", "zh": "Anthropic" },
        "items": ["claude-code", "claude-fable-5", "claude-desktop"]
      },
      ...
    ]
  }
}
```

**新增：`articles/models/index.json`**：

```json
{
  "section": "models",
  "title": { "en": "Models", "zh": "模型" },
  "navigation": {
    "groups": [
      {
        "id": "overview",
        "title": { "en": "Overview", "zh": "总览" },
        "items": ["current-lineup", "how-to-choose"]
      },
      {
        "id": "families",
        "title": { "en": "Model Families", "zh": "模型系列" },
        "items": ["gpt-family", "claude-family", "deepseek-family"]
      }
    ]
  }
}
```

---

### 方案 B：最小改动方案（不推荐）

只新增 `magpie` 文档，不改动现有文档。

**问题**：
- 用户不知道应该用 magpie 还是单独配置
- 文档重复和过时问题依然存在
- 错失了优化用户体验的机会

---

## 详细文档结构

### 新文档 1：`articles/runtime/magpie/zh.md`

```markdown
---
title: magpie - 统一管理所有 AI 工具
slug: magpie
order: 0
summary: 用 magpie 统一管理 Claude Code、Codex、Pi 等所有 AI 工具的模型配置，一个命令切换场景。
section: runtime
group: magpie
group_title: 统一管理
group_order: 5
---

# magpie - 统一管理所有 AI 工具

如果你同时使用多个 AI 工具（Claude Code、Codex、Pi、Cursor 等），magpie 能让配置管理变得简单。

## magpie 是什么

magpie 是一个**本地模型网关**，它：
- 在 `127.0.0.1:3425` 运行
- 统一管理所有 AI 工具的模型配置
- 支持一键切换模型和场景
- 支持多账号自动切换

**一个比喻**：
- 没有 magpie：每个 AI 工具都有自己的配置文件，你要改 N 个文件
- 有了 magpie：所有 AI 工具都通过 magpie 访问模型，你只改一个地方

## 为什么需要 magpie

### 问题 1：配置分散

**没有 magpie**：
```
Claude Code → ~/.claude/settings.json
Codex       → ~/.codex/config.toml
Pi          → ~/.pi/agent/settings.json
Cursor      → ~/.cursor/config.json
```

每次想换模型，要改 4 个文件。

**有了 magpie**：
```bash
magpie claude sorrycode/claude-opus-5-5
magpie codex sorrycode/gpt-6.1-sol
magpie pi sorrycode/claude-opus-5-5
magpie cursor sorrycode/claude-sonnet-5-5
```

一个命令，搞定。

### 问题 2：场景切换困难

你有不同的工作场景：
- **工作模式**：用最好的模型（Opus 5.5、GPT-6.1 Sol）
- **快速模式**：用便宜的模型（DeepSeek Flash、Haiku）
- **实验模式**：测试新模型（Grok、GLM）

**没有 magpie**：
- 要记住每个场景的配置
- 切换时要改所有文件

**有了 magpie**：
```bash
magpie use work       # 工作模式
magpie use fast       # 快速模式
magpie use experiment # 实验模式
```

### 问题 3：多账号管理麻烦

你有 3 个 sorrycode 账号，想自动轮换：
- 账号 1 配额用完 → 自动切换到账号 2
- 账号 2 也用完 → 自动切换到账号 3

**没有 magpie**：手动检查配额，手动改配置

**有了 magpie**：自动处理，无感知

## 快速开始

### 第一步：安装 magpie

```bash
curl -fsSL https://usemagpie.ai/install.sh | sh
```

安装完成后：
- macOS: `/Applications/magpie.app` + `~/.local/bin/magpie`
- 可以用 GUI 或 CLI

### 第二步：添加 sorrycode providers

magpie 需要知道你的 API keys。从 sorrycode 控制台获取 API key：

```bash
# 添加主 provider（覆盖 Claude + GPT + DeepSeek）
magpie provider add "SorryCode" \
  url=https://api.sorrycode.com/v1 \
  key=sk-你的key
```

如果你有多个 key（针对不同模型系列），可以分别添加：

```bash
# GPT 专用 key
magpie provider add "SorryCode GPT" \
  url=https://sorrycode.com/v1 \
  key=sk-gpt-key \
  responses=true

# Claude 专用 key（原生 Anthropic API）
magpie provider add "SorryCode Claude" \
  url=https://sorrycode.com \
  key=sk-claude-key \
  anthropic=true

# 国产模型 key（DeepSeek、GLM）
magpie provider add "SorryCode CN" \
  url=https://sorrycode.com/v1 \
  key=sk-cn-key \
  responses=true
```

### 第三步：配置模型列表

告诉 magpie 每个 provider 有哪些模型：

```bash
# 主 provider 的模型
magpie provider models sorrycode \
  claude-opus-5-5 \
  claude-sonnet-5-5 \
  gpt-6.1-sol \
  deepseek-v4-pro

# GPT provider 的模型
magpie provider models sorrycode-gpt \
  gpt-6.1-sol \
  gpt-6.1-astra \
  gpt-6-luna

# Claude provider 的模型
magpie provider models sorrycode-claude \
  claude-opus-5-5 \
  claude-sonnet-5-5 \
  claude-haiku-5-5

# 国产模型 provider
magpie provider models sorrycode-cn \
  deepseek-flash \
  glm-5.3-prime
```

### 第四步：配置你的 AI 工具

为每个工具设置默认模型：

```bash
# 保存当前配置（以防万一）
magpie save baseline

# 配置 Claude Code
magpie claude sorrycode-claude/claude-opus-5-5 effort max

# 配置 Codex
magpie codex sorrycode-gpt/gpt-6.1-sol effort xhigh

# 配置 Pi
magpie pi sorrycode-gpt/gpt-6.1-sol thinking xhigh

# 配置 Cursor
magpie cursor sorrycode/claude-sonnet-5-5
```

**注意**：配置后需要重启对应的工具才能生效。

### 第五步：验证配置

```bash
# 查看所有工具的当前配置
magpie agents

# 查看所有可用模型
magpie models

# 查看某个 provider 详情
magpie provider sorrycode-claude
```

## 场景管理

### 创建工作场景

**场景 1：工作模式（高质量）**

```bash
magpie claude sorrycode-claude/claude-opus-5-5 effort max
magpie codex sorrycode-gpt/gpt-6.1-sol effort xhigh
magpie pi sorrycode-claude/claude-opus-5-5 thinking xhigh
magpie cursor sorrycode-claude/claude-opus-5-5
magpie save work
```

**场景 2：快速模式（省钱）**

```bash
magpie claude sorrycode-claude/claude-haiku-5-5 effort medium
magpie codex sorrycode-gpt/gpt-6-luna effort medium
magpie pi sorrycode-cn/deepseek-flash thinking low
magpie cursor sorrycode-cn/deepseek-flash
magpie save fast
```

**场景 3：实验模式（测试新模型）**

```bash
magpie claude sorrycode-cn/glm-5.3-prime effort high
magpie codex sorrycode-gpt/gpt-6.1-astra effort high
magpie pi sorrycode-cn/deepseek-flash thinking medium
magpie cursor sorrycode/claude-sonnet-5-5
magpie save experiment
```

### 切换场景

```bash
# 早上开始工作
magpie use work

# 下午做简单修改
magpie use fast

# 周五测试新想法
magpie use experiment

# 恢复到初始配置
magpie use baseline
```

## 多账号管理（高级）

如果你有多个 sorrycode 账号，可以创建 routing group 实现自动切换。

### 添加多个账号

```bash
# 账号 1
magpie provider add "SorryCode 1" \
  url=https://api.sorrycode.com/v1 \
  key=sk-account1

magpie provider models sorrycode-1 claude-opus-5-5 gpt-6.1-sol

# 账号 2
magpie provider add "SorryCode 2" \
  url=https://api.sorrycode.com/v1 \
  key=sk-account2

magpie provider models sorrycode-2 claude-opus-5-5 gpt-6.1-sol

# 账号 3
magpie provider add "SorryCode 3" \
  url=https://api.sorrycode.com/v1 \
  key=sk-account3

magpie provider models sorrycode-3 claude-opus-5-5 gpt-6.1-sol
```

### 创建 routing group

```bash
# 创建 Opus 集群（3 个账号轮换）
magpie group add "Opus Cluster" \
  models=sorrycode-1/claude-opus-5-5,sorrycode-2/claude-opus-5-5,sorrycode-3/claude-opus-5-5 \
  routing=smart

# 使用 routing group
magpie claude group/opus-cluster
magpie pi group/opus-cluster
```

**工作原理**：
1. magpie 优先使用账号 1
2. 账号 1 配额用完 → 自动切换到账号 2
3. 账号 2 也用完 → 自动切换到账号 3
4. 所有账号恢复后 → 重新均衡分配

## 与各 AI 工具的集成

### Claude Code

magpie 接管 Claude Code 的模型配置：

```bash
# 切换主模型
magpie claude sorrycode-claude/claude-opus-5-5

# 切换 haiku 模型（快速任务）
magpie claude haiku sorrycode-claude/claude-haiku-5-5

# 切换 reasoning effort
magpie claude effort max
```

**注意**：切换后无需重启 Claude Code，实时生效。

### Codex

magpie 接管 Codex 的模型配置：

```bash
# 切换模型
magpie codex sorrycode-gpt/gpt-6.1-sol

# 切换 reasoning effort
magpie codex effort xhigh
```

**注意**：切换后需要重启 Codex 和 Codex app-server：
```bash
codex app-server daemon restart
# 然后重启 Codex app
```

**会话丢失问题**：
- ✅ 在 Codex 界面里切换模型 → 会话不丢失
- ❌ 用 magpie 命令切换 + 重启 → 会话丢失

**建议**：
- 有重要会话时 → 在 Codex 界面里手动切换
- 场景切换/每天开始工作 → 用 magpie 命令

### Pi Agent

magpie 接管 Pi 的模型配置：

```bash
# 切换模型
magpie pi sorrycode-gpt/gpt-6.1-sol

# 切换 thinking level
magpie pi thinking xhigh
```

**注意**：Pi 无需重启，实时生效。

### Cursor

magpie 接管 Cursor 的模型配置：

```bash
# 切换模型
magpie cursor sorrycode/claude-sonnet-5-5
```

**注意**：切换后需要重启 Cursor。

## 常用命令速查

### 查看状态

```bash
# 查看所有 providers
magpie providers

# 查看所有模型
magpie models

# 查看所有 AI 工具状态
magpie agents

# 查看某个 provider 详情
magpie provider sorrycode-claude

# 查看配额
magpie quota
```

### 切换配置

```bash
# 切换单个工具的模型
magpie claude sorrycode/claude-opus-5-5
magpie codex sorrycode/gpt-6.1-sol

# 切换 reasoning level
magpie claude effort max
magpie codex effort xhigh

# 使用 routing group
magpie claude group/opus-cluster
```

### Profile 管理

```bash
# 保存当前配置
magpie save <profile-name>

# 切换 profile
magpie use work
magpie use fast
magpie use experiment

# 查看所有 profiles
magpie profiles

# 恢复初始配置
magpie use baseline
```

## 故障排查

### 问题 1：magpie 网关没有启动

**症状**：AI 工具报错连接 `127.0.0.1:3425` 失败

**检查**：
```bash
lsof -i :3425
```

**解决**：
```bash
# 启动 magpie
open -a magpie
# 或
magpie tui
```

### 问题 2：切换模型后不生效

**Codex**：需要重启
```bash
codex app-server daemon restart
# 然后重启 Codex app
```

**Cursor**：需要重启 Cursor

**Claude Code**：应该实时生效，如果不生效，重启 Claude Code

**Pi**：应该实时生效

### 问题 3：API 调用失败

**检查 provider 状态**：
```bash
magpie provider sorrycode-claude
```

**测试 API key**：
```bash
curl https://api.sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key"
```

**重新配置 provider**：
```bash
magpie provider set sorrycode-claude key=sk-新的key
```

### 问题 4：想恢复原始配置

**方法 1**：使用 baseline profile
```bash
magpie use baseline
```

**方法 2**：关闭 magpie，手动编辑配置文件
- Claude Code: `~/.claude/settings.json`
- Codex: `~/.codex/config.toml`
- Pi: `~/.pi/agent/settings.json`

## 常见问题

### Q: magpie 会替换掉原来的配置吗？

**A**: 不会。magpie 是**增强**，不是替换。

- ✅ 原来的 provider 配置还在
- ✅ 你仍然可以在各工具界面里手动切换模型
- ✅ magpie 只是多了一个选项

**你可以混用**：
- 日常用 magpie 快速切换场景
- 临时测试时在工具界面里手动选

### Q: 用 magpie 切换会丢失会话吗？

**A**: 取决于工具。

| 工具 | magpie 切换 + 重启 | 工具界面切换 |
|------|------------------|-------------|
| Codex | ❌ 会丢失 | ✅ 不丢失 |
| Claude Code | ✅ 不丢失（无需重启） | ✅ 不丢失 |
| Pi | ✅ 不丢失（无需重启） | ✅ 不丢失 |
| Cursor | ❌ 会丢失 | ✅ 不丢失 |

**建议**：
- 有重要会话 → 用工具界面切换
- 场景切换 → 用 magpie 命令

### Q: magpie 支持哪些 AI 工具？

**A**: 查看支持列表：
```bash
magpie agents
```

当前支持（2026-10）：
- Claude Code, Claude Desktop
- Codex, ChatGPT App
- Pi Agent
- Cursor
- DeepSeek Harness
- Kimi Code
- WorkBuddy
- Zed
- 等等...

### Q: 我可以只用 magpie 管理部分工具吗？

**A**: 可以。

magpie 不是"全有或全无"：
- 用 magpie 管理 Claude Code + Codex
- Pi 继续手动配置
- 完全没问题

### Q: magpie 的配置存在哪里？

**A**: 
- macOS: `~/.config/magpie/`
- Windows: `%APPDATA%\magpie\`

## 进一步阅读

- [当前模型阵容](/docs/models/current-lineup) - 了解所有可用模型
- [如何选择模型](/docs/models/how-to-choose) - 根据任务选择合适的模型
- [Claude Code](/docs/runtime/claude-code) - Claude Code 详细指南
- [Codex](/docs/runtime/codex) - Codex 详细指南
- [Pi Agent](/docs/runtime/pi-agent) - Pi Agent 详细指南

## 总结

**magpie 的价值**：
- ✅ 统一配置所有 AI 工具
- ✅ 一个命令切换场景
- ✅ 多账号自动管理
- ✅ 简化日常工作流

**何时使用 magpie**：
- ✅ 你使用多个 AI 工具
- ✅ 你需要在不同场景间切换
- ✅ 你有多个 sorrycode 账号
- ✅ 你想要统一的管理界面

**何时不用 magpie**：
- ❌ 你只用一个 AI 工具
- ❌ 你不需要切换场景
- ❌ 你习惯手动配置

**推荐做法**：
1. 先用 magpie 配置好所有工具
2. 创建 2-3 个常用 profiles
3. 日常用 magpie 切换场景
4. 临时测试用工具界面切换
```

---

### 新文档 2：`articles/models/current-lineup/zh.md`

```markdown
---
title: 当前模型阵容
slug: current-lineup
order: 1
summary: sorrycode 当前提供的所有模型，按用途分类，帮助你快速选择合适的模型。
section: models
section_title: 模型
section_order: 5
---

# 当前模型阵容

sorrycode 聚合了多家前沿 AI 模型。这页帮你了解当前可用的所有模型，并按用途分类。

> **快速导航**
>
> - [高质量模型](#high-quality) - 生产代码、关键功能
> - [干活模型](#workhorse) - 日常开发、快速迭代
> - [快速模型](#fast) - 简单任务、测试
> - [实验模型](#experimental) - 测试、对比

## 模型分类

我们按实际使用场景分类，而不是按厂商：

| 分类 | 用途 | 成本 | 速度 |
|------|------|------|------|
| **高质量** | 生产代码、关键功能、复杂推理 | 高 | 慢 |
| **干活** | 日常开发、快速迭代、大量任务 | 中 | 中 |
| **快速** | 简单修改、测试、调试、文档 | 低 | 快 |
| **实验** | 测试新模型、对比效果 | 中 | 中 |

---

<h2 id="high-quality">高质量模型</h2>

**用途**：生产代码、关键功能、需要最高质量的任务

### Claude Opus 5.5

**模型 ID**：`claude-opus-5-5`

**特点**：
- Claude 系列最高质量模型
- 最强的推理和代码能力
- 支持 max reasoning effort
- 200k context window

**何时使用**：
- ✅ 复杂架构设计
- ✅ 关键功能开发
- ✅ 需要深度推理的任务
- ✅ 代码审查和重构

**成本**：高

**配置示例**：
```bash
magpie claude sorrycode/claude-opus-5-5 effort max
```

---

### GPT-6.1 Sol

**模型 ID**：`gpt-6.1-sol`

**特点**：
- GPT-6.1 系列的推理专家
- 支持 ultra reasoning effort（独有）
- 1M+ context window
- 最高 128k output tokens

**何时使用**：
- ✅ 需要最强推理的任务
- ✅ 多步骤 Agent 工作流
- ✅ 长上下文处理
- ✅ 专业知识工作

**成本**：高（ultra effort 更高）

**配置示例**：
```bash
magpie codex sorrycode/gpt-6.1-sol effort xhigh
```

**注意**：`ultra` effort 成本很高，先用 `xhigh` 验证效果。

---

### GPT-6.1 Astra

**模型 ID**：`gpt-6.1-astra`

**特点**：
- GPT-6.1 系列的均衡模型
- 质量和速度的平衡
- 支持 high/xhigh reasoning

**何时使用**：
- ✅ 需要高质量但也看重速度
- ✅ 成本敏感但质量不能妥协
- ✅ 中等复杂度的任务

**成本**：中高

---

<h2 id="workhorse">干活模型</h2>

**用途**：日常开发、快速迭代、大量任务

### Claude Sonnet 5.5

**模型 ID**：`claude-sonnet-5-5`

**特点**：
- Claude 系列的平衡模型
- 质量足够好，速度快
- 成本合理
- 支持 high/xhigh reasoning

**何时使用**：
- ✅ 日常代码开发
- ✅ 功能实现
- ✅ Bug 修复
- ✅ 代码重构

**成本**：中

**配置示例**：
```bash
magpie claude sorrycode/claude-sonnet-5-5 effort high
```

**推荐**：这是大多数人的日常首选。

---

### DeepSeek Flash

**模型 ID**：`deepseek-flash`

**特点**：
- 开源模型，性价比极高
- 速度快
- 质量足够应对大部分任务
- 支持 high/max reasoning

**何时使用**：
- ✅ 大量重复任务
- ✅ 成本敏感的场景
- ✅ 快速原型
- ✅ 简单到中等复杂度的任务

**成本**：低

**配置示例**：
```bash
magpie pi sorrycode/deepseek-flash thinking high
```

---

<h2 id="fast">快速模型</h2>

**用途**：简单任务、测试、调试、文档

### Claude Haiku 5.5

**模型 ID**：`claude-haiku-5-5`

**特点**：
- Claude 系列最快的模型
- 成本低
- 质量足够应对简单任务
- 支持 low/medium reasoning

**何时使用**：
- ✅ 简单代码修改
- ✅ 格式转换
- ✅ 文档生成
- ✅ 简单问答

**成本**：低

**配置示例**：
```bash
magpie claude sorrycode/claude-haiku-5-5 effort medium
```

---

### GPT-6 Luna

**模型 ID**：`gpt-6-luna`

**特点**：
- GPT-6 系列的快速模型
- 平衡速度和质量
- 成本合理

**何时使用**：
- ✅ 快速测试
- ✅ 简单任务
- ✅ 高并发场景

**成本**：低

---

### Gemini 3.8 Flash

**模型 ID**：`gemini-3.8-flash`

**特点**：
- Google 的快速模型
- 免费或低成本
- 适合简单任务

**何时使用**：
- ✅ 成本极度敏感
- ✅ 简单重复任务
- ✅ 测试和验证

**成本**：极低

---

<h2 id="experimental">实验模型</h2>

**用途**：测试新模型、对比效果、探索

### Grok 4.7

**模型 ID**：`grok-4.7`

**特点**：
- xAI 的模型
- 实时数据接入
- 独特的回答风格

**何时使用**：
- ✅ 需要实时信息
- ✅ 对比不同模型效果
- ✅ 探索新方向

**成本**：中

---

### GLM 5.3 Prime

**模型 ID**：`glm-5.3-prime`

**特点**：
- 智谱 AI 的模型
- 国产模型
- 中文能力强

**何时使用**：
- ✅ 中文任务
- ✅ 对比国产模型
- ✅ 测试备选方案

**成本**：中

---

### DeepSeek V4 Pro

**模型 ID**：`deepseek-v4-pro`

**特点**：
- DeepSeek 的高质量版本
- 比 Flash 慢但质量更好
- 性价比高

**何时使用**：
- ✅ 需要比 Flash 更好的质量
- ✅ 成本敏感但质量重要
- ✅ 对比开源模型

**成本**：中

---

## 如何选择模型

### 按任务类型选择

| 任务类型 | 推荐模型 | 备选 |
|---------|---------|------|
| **复杂架构设计** | Opus 5.5, GPT-6.1 Sol | GPT-6.1 Astra |
| **日常开发** | Sonnet 5.5, DeepSeek Flash | GPT-6.1 Astra |
| **简单修改** | Haiku 5.5, Luna, Gemini Flash | Sonnet 5.5 |
| **代码审查** | Opus 5.5, GPT-6.1 Sol | Sonnet 5.5 |
| **文档生成** | Haiku 5.5, Luna | Sonnet 5.5 |
| **测试对比** | Grok 4.7, GLM 5.3, DeepSeek V4 Pro | - |

### 按预算选择

| 预算 | 工作模式 | 快速模式 |
|------|---------|---------|
| **不限** | Opus 5.5 + GPT-6.1 Sol | Sonnet 5.5 |
| **中等** | Sonnet 5.5 + GPT-6.1 Astra | DeepSeek Flash |
| **紧张** | DeepSeek Flash + DeepSeek V4 Pro | Haiku 5.5, Gemini Flash |

### 按场景选择

**生产环境**：
- 主力：Opus 5.5, GPT-6.1 Sol
- 备选：Sonnet 5.5, GPT-6.1 Astra

**开发环境**：
- 主力：Sonnet 5.5, DeepSeek Flash
- 备选：DeepSeek V4 Pro, Haiku 5.5

**测试环境**：
- 主力：Haiku 5.5, Luna, Gemini Flash
- 备选：DeepSeek Flash

## 模型更新记录

### 2026-10-13
- ✅ 新增：`claude-opus-5-5`
- ✅ 新增：`claude-sonnet-5-5`
- ✅ 新增：`claude-haiku-5-5`
- ✅ 新增：`gpt-6.1-sol`
- ✅ 新增：`gpt-6.1-astra`
- ✅ 新增：`gpt-6-luna`
- ✅ 新增：`deepseek-flash`
- ⚠️ 过时：`gpt-5.6-sol` → 推荐升级到 `gpt-6.1-sol`
- ⚠️ 过时：`claude-opus-4-6` → 推荐升级到 `claude-opus-5-5`

### 如何保持更新

1. **查看 sorrycode 控制台**：最新模型会第一时间出现
2. **查询 API**：
   ```bash
   curl https://sorrycode.com/v1/models \
     -H "Authorization: Bearer sk-你的key"
   ```
3. **关注文档更新**：这页会保持同步

## 用 magpie 管理模型

如果你使用多个 AI 工具，推荐用 magpie 统一管理：

```bash
# 工作模式：高质量
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
magpie save work

# 快速模式：省钱
magpie claude sorrycode/claude-haiku-5-5 effort medium
magpie codex sorrycode/gpt-6-luna effort medium
magpie save fast

# 切换
magpie use work
magpie use fast
```

👉 [完整指南：使用 magpie 管理所有 AI 工具](/docs/runtime/magpie)

## 常见问题

### Q: 哪个模型最好？

**A**: 没有"最好"，只有"最合适"。

- 追求质量 → Opus 5.5, GPT-6.1 Sol
- 追求性价比 → Sonnet 5.5, DeepSeek Flash
- 追求速度 → Haiku 5.5, Luna, Gemini Flash

### Q: 如何测试不同模型？

**A**: 用同一个任务测试：

```bash
# 测试 Opus 5.5
magpie claude sorrycode/claude-opus-5-5
# 执行任务，记录效果

# 测试 Sonnet 5.5
magpie claude sorrycode/claude-sonnet-5-5
# 执行同样的任务，对比效果
```

### Q: 模型版本会自动更新吗？

**A**: 不会。你需要手动切换到新版本。

推荐做法：
1. 在测试项目中验证新版本
2. 确认效果满意后，更新生产配置

### Q: 过时的模型还能用吗？

**A**: 能用，但不推荐。

- `gpt-5.6-sol` 仍然可用，但 `gpt-6.1-sol` 更好
- `claude-opus-4-6` 仍然可用，但 `claude-opus-5-5` 更强

## 进一步阅读

- [如何选择模型](/docs/models/how-to-choose) - 详细的选择指南
- [使用 magpie 管理模型](/docs/runtime/magpie) - 统一管理所有 AI 工具
- [GPT 系列详解](/docs/models/gpt-family) - GPT-6.1 Sol, Astra, Luna 对比
- [Claude 系列详解](/docs/models/claude-family) - Opus, Sonnet, Haiku 对比
```

---

## 需要删除/合并的文档清单

### ❌ 删除

1. **`articles/runtime/gpt-5-6-sol/zh.md`**
   - 原因：模型版本过时
   - 替代：`articles/models/current-lineup/zh.md#gpt-family`
   - 重定向：`/docs/runtime/gpt-5-6-sol` → `/docs/models/current-lineup#gpt-61-sol`

### 🔀 合并

1. **`articles/runtime/codex-multi-model/zh.md` → `articles/runtime/magpie/zh.md`**
   - 原因：magpie 是更好的多模型管理方案
   - 保留核心内容：如何在 Codex 里用 Grok、DeepSeek
   - 重定向：`/docs/runtime/codex-multi-model` → `/docs/runtime/magpie#multi-model`

## 需要简化的文档清单

### 📝 简化（17 个 runtime 文档）

所有 runtime 文档都需要调整结构：

1. **保留**：
   - 工具介绍
   - 工具特色功能
   - 工具特有的配置（如 Claude Code 的 computer use）

2. **简化**：
   - API Key 配置流程 → 推荐用 magpie，传统方式折叠
   - 一键安装流程 → 推荐用 magpie，传统方式折叠
   - 模型选择 → 链接到 `models/current-lineup`

3. **新增**：
   - magpie 快速配置指南
   - 与 magpie 的集成说明

**受影响的文档**：
- `claude-code/zh.md`
- `codex/zh.md`
- `pi-agent/zh.md`
- `cursor/zh.md`
- `dsh/zh.md`
- `kimi-code/zh.md`
- `workbuddy/zh.md`
- `opencode/zh.md`
- `claude-desktop/zh.md`
- `claude-fable-5/zh.md`
- `grok-build/zh.md`
- `grok-image/zh.md`
- `grok-video/zh.md`
- `gpt-image-2/zh.md`
- `gpt-image-2-5/zh.md`
- `agent-capabilities/zh.md`

---

## 新文档结构总览

```
articles/
├── models/                        [新增 section]
│   ├── index.json
│   ├── current-lineup/           [新增] 当前模型阵容
│   │   ├── zh.md
│   │   └── en.md
│   ├── how-to-choose/            [新增] 如何选择模型
│   │   ├── zh.md
│   │   └── en.md
│   ├── gpt-family/               [新增] GPT 系列详解
│   │   ├── zh.md
│   │   └── en.md
│   └── claude-family/            [新增] Claude 系列详解
│       ├── zh.md
│       └── en.md
│
├── runtime/
│   ├── index.json                [更新] 新增 magpie group
│   ├── magpie/                   [新增] magpie 统一管理
│   │   ├── zh.md
│   │   └── en.md
│   ├── codex/                    [简化] 推荐 magpie
│   │   ├── zh.md
│   │   └── en.md
│   ├── claude-code/              [简化] 推荐 magpie
│   │   ├── zh.md
│   │   └── en.md
│   ├── pi-agent/                 [简化] 推荐 magpie
│   │   ├── zh.md
│   │   └── en.md
│   ├── gpt-5-6-sol/              [删除] 过时
│   ├── codex-multi-model/        [合并到 magpie]
│   └── ...                       [其他 runtime 文档简化]
│
├── start/                        [保持不变]
├── concepts/                     [保持不变]
├── agent-memory/                 [保持不变]
├── environment/                  [保持不变]
├── practices/                    [保持不变]
├── tools/                        [保持不变]
└── troubleshoot/                 [保持不变]
```

---

## 实施步骤

### Phase 1：准备工作（1-2 天）

1. ✅ 完成 magpie 实际配置测试（已完成）
2. ✅ 整理 magpie 配置文档（已完成 `docs/research/magpie-完整配置总结.md`）
3. ⏳ 确认当前模型阵容（需要和 sorrycode 后端确认）
4. ⏳ 确认模型 ID 和命名规范

### Phase 2：创建新文档（2-3 天）

1. ⏳ 创建 `articles/runtime/magpie/zh.md`
2. ⏳ 创建 `articles/models/current-lineup/zh.md`
3. ⏳ 创建 `articles/models/how-to-choose/zh.md`
4. ⏳ 创建 `articles/models/gpt-family/zh.md`
5. ⏳ 创建 `articles/models/claude-family/zh.md`
6. ⏳ 创建对应的英文版本

### Phase 3：重构现有文档（3-5 天）

1. ⏳ 更新 17 个 runtime 文档（推荐 magpie，简化配置流程）
2. ⏳ 删除 `gpt-5-6-sol/zh.md` + 设置重定向
3. ⏳ 合并 `codex-multi-model` 到 `magpie` + 设置重定向
4. ⏳ 更新 `articles/runtime/index.json`（新增 magpie group）
5. ⏳ 创建 `articles/models/index.json`

### Phase 4：验证和发布（1-2 天）

1. ⏳ 检查所有链接
2. ⏳ 验证重定向
3. ⏳ 本地预览所有修改
4. ⏳ 提交和部署
5. ⏳ 监控用户反馈

---

## 预期效果

### 用户体验改善

**之前**：
1. 用户打开 Claude Code 文档
2. 看到完整的 API Key 配置流程
3. 配置好 Claude Code
4. 想用 Codex，又要走一遍流程
5. 想切换模型，不知道怎么做
6. 想知道哪个模型好，要搜索多个文档

**之后**：
1. 用户打开 Claude Code 文档
2. 看到"推荐：用 magpie 统一管理"
3. 点击链接，完成 magpie 配置
4. 所有工具都配置好了
5. 切换模型：`magpie use work`
6. 选择模型：查看 `models/current-lineup`

### 文档维护简化

**之前**：
- 模型更新 → 要改多个 runtime 文档
- API endpoint 变化 → 要改 17 个文档
- 新增 runtime → 要写完整的配置流程

**之后**：
- 模型更新 → 只改 `models/current-lineup`
- API endpoint 变化 → 只改 `magpie` 文档
- 新增 runtime → 只写工具特色 + 链接 magpie

### 用户路径优化

**路径 1：新用户**
```
开始使用 → 创建 API Key → 安装 magpie → 配置工具 → 选择模型
```

**路径 2：单工具用户**
```
Codex 文档 → 传统配置方式（折叠） → 开始使用
```

**路径 3：多工具用户**
```
magpie 文档 → 配置所有工具 → 场景管理 → 开始使用
```

---

## 风险和备选方案

### 风险 1：用户习惯单独配置

**缓解措施**：
- 保留传统配置方式（折叠）
- 明确说明两种方式的优劣
- 不强制用户使用 magpie

### 风险 2：magpie 本身有 bug

**缓解措施**：
- 文档中包含故障排查
- 提供恢复原始配置的方法
- 保留传统配置方式作为备选

### 风险 3：重构工作量大

**缓解措施**：
- 分阶段实施
- 优先处理核心文档（magpie、codex、claude-code）
- 其他文档逐步更新

### 备选方案：最小改动

如果资源有限，可以先：
1. 只新增 `magpie` 文档
2. 只新增 `models/current-lineup` 文档
3. 在核心 runtime 文档开头加一句"推荐用 magpie"
4. 其他文档暂不改动

---

## 总结

### 核心改动

1. **新增 1 个 section**：`models/`
2. **新增 5 篇文档**：magpie + 4 篇模型文档
3. **简化 17 篇文档**：runtime 文档推荐 magpie
4. **删除 1 篇文档**：gpt-5.6-sol（过时）
5. **合并 1 篇文档**：codex-multi-model → magpie

### 预期收益

1. **用户体验**：
   - ✅ 配置更简单（一次配置所有工具）
   - ✅ 切换更方便（一个命令切换场景）
   - ✅ 选择更清晰（统一的模型指南）

2. **文档质量**：
   - ✅ 减少重复内容
   - ✅ 降低维护成本
   - ✅ 信息更新及时

3. **产品定位**：
   - ✅ 体现 sorrycode 的整合能力
   - ✅ magpie 成为差异化竞争力
   - ✅ 用户粘性提升

### 关键决策点

**决策 1**：是否采用方案 A（全面重构）？
- 推荐：是
- 理由：长期收益大于短期成本

**决策 2**：是否删除 `gpt-5.6-sol` 文档？
- 推荐：是（但保留重定向）
- 理由：过时信息损害用户体验

**决策 3**：是否强制用户使用 magpie？
- 推荐：否
- 理由：保留选择权，避免用户反感

---

## 下一步

1. **确认方案**：选择方案 A 或备选方案
2. **分配资源**：确定人力和时间
3. **开始实施**：按 Phase 1-4 执行
4. **收集反馈**：监控用户反馈，持续优化

**需要你的决策**：
- ✅ 同意整体方向？
- ✅ 确认实施阶段？
- ✅ 需要调整哪些内容？
