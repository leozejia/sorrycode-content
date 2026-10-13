---
title: magpie - 统一管理所有 AI 工具
slug: magpie
order: 0
summary: 用 magpie 统一管理 Claude Code、Codex、Pi 等所有 AI 工具的模型配置，一个命令切换场景。
section: runtime
section_title: 模型与工作台
section_order: 10
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

magpie 需要知道你的 API keys。从 [sorrycode 控制台](https://sorrycode.com/keys)获取 API key。

**推荐配置**（覆盖所有模型）：

```bash
# 主 provider（Claude + GPT + DeepSeek）
magpie provider add "SorryCode" \
  url=https://api.sorrycode.com/v1 \
  key=sk-你的主key

# Claude 专用（原生 Anthropic API，更稳定）
magpie provider add "SorryCode Claude" \
  url=https://sorrycode.com \
  key=sk-你的claude-key \
  anthropic=true

# GPT 专用
magpie provider add "SorryCode GPT" \
  url=https://sorrycode.com/v1 \
  key=sk-你的gpt-key \
  responses=true

# 国产模型（DeepSeek、GLM）
magpie provider add "SorryCode CN" \
  url=https://sorrycode.com/v1 \
  key=sk-你的cn-key \
  responses=true
```

**最简配置**（只用一个 key）：

```bash
magpie provider add "SorryCode" \
  url=https://api.sorrycode.com/v1 \
  key=sk-你的key
```

### 第三步：配置模型列表

告诉 magpie 每个 provider 有哪些模型。

**查询可用模型**：

```bash
# 查看你的 key 有哪些模型
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key"
```

**配置模型**：

```bash
# 主 provider
magpie provider models sorrycode \
  claude-opus-5-5 \
  claude-sonnet-5-5 \
  claude-haiku-4-5-20251001 \
  gpt-6.1-sol \
  deepseek-v4-pro

# Claude provider（如果配置了）
magpie provider models sorrycode-claude \
  claude-opus-5-5 \
  claude-sonnet-5-5

# GPT provider（如果配置了）
magpie provider models sorrycode-gpt \
  gpt-6.1-sol

# CN provider（如果配置了）
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
magpie claude sorrycode/claude-opus-5-5 effort max

# 配置 Codex
magpie codex sorrycode/gpt-6.1-sol effort xhigh

# 配置 Pi
magpie pi sorrycode/gpt-6.1-sol thinking xhigh

# 配置 Cursor（如果你用）
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
magpie provider sorrycode
```

## 场景管理

### 创建工作场景

**场景 1：工作模式（高质量）**

```bash
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
magpie pi sorrycode/claude-opus-5-5 thinking xhigh
magpie save work
```

**场景 2：快速模式（省钱）**

```bash
magpie claude sorrycode/claude-haiku-4-5-20251001 effort medium
magpie codex sorrycode/deepseek-v4-pro effort medium
magpie pi sorrycode/deepseek-flash thinking low
magpie save fast
```

**场景 3：实验模式（测试新模型）**

```bash
magpie claude sorrycode/claude-sonnet-5-5 effort high
magpie codex sorrycode/gpt-6.1-sol effort high
magpie pi sorrycode/deepseek-flash thinking medium
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

## 与各 AI 工具的集成

### Claude Code

magpie 接管 Claude Code 的模型配置：

```bash
# 切换主模型
magpie claude sorrycode/claude-opus-5-5

# 切换 haiku 模型（快速任务）
magpie claude haiku sorrycode/claude-haiku-4-5-20251001

# 切换 reasoning effort
magpie claude effort max
```

**注意**：Claude Code 无需重启，实时生效。

👉 [完整指南：Claude Code](/docs/runtime/claude-code)

### Codex / ChatGPT

magpie 接管 Codex 的模型配置：

```bash
# 切换模型
magpie codex sorrycode/gpt-6.1-sol

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

👉 [完整指南：Codex](/docs/runtime/codex)

### Pi Agent

magpie 接管 Pi 的模型配置：

```bash
# 切换模型
magpie pi sorrycode/gpt-6.1-sol

# 切换 thinking level
magpie pi thinking xhigh
```

**注意**：Pi 无需重启，实时生效。

👉 [完整指南：Pi Agent](/docs/runtime/pi-agent)

### Cursor

magpie 接管 Cursor 的模型配置：

```bash
# 切换模型
magpie cursor sorrycode/claude-sonnet-5-5
```

**注意**：切换后需要重启 Cursor。

👉 [完整指南：Cursor](/docs/runtime/cursor)

### 其他工具

magpie 支持的所有工具：

```bash
# 查看支持列表
magpie agents
```

当前支持（2026-10）：
- Claude Code, Claude Desktop
- Codex, ChatGPT App
- Pi Agent
- Cursor
- DeepSeek Harness (DSH)
- Kimi Code
- WorkBuddy
- OpenCode
- Zed
- 等等...

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
magpie provider sorrycode

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
magpie provider sorrycode
```

**测试 API key**：
```bash
curl https://api.sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key"
```

**重新配置 provider**：
```bash
magpie provider set sorrycode key=sk-新的key
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
- OpenCode
- Zed
- 等等...

### Q: 我可以只用 magpie 管理部分工具吗？

**A**: 可以。

magpie 不是"全有或全无"：
- 用 magpie 管理 Claude Code + Codex
- Pi 继续手动配置
- 完全没问题

### Q: 在 Codex 中用其他厂商的模型（Grok、DeepSeek）

**A**: magpie 完全支持。

之前你需要手动配置 `~/.codex/config.toml`，现在用 magpie 更简单：

```bash
# 添加 Grok provider
magpie provider add "Grok" \
  url=https://sorrycode.com/v1 \
  key=sk-你的grok-key \
  responses=true

magpie provider models grok grok-4.7

# 在 Codex 中使用 Grok
magpie codex grok/grok-4.7
```

这替代了之前 [在 ChatGPT / Codex 中使用其他模型](/docs/runtime/codex-multi-model) 文档中的手动配置流程。

## 进一步阅读

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
- 你只用一个 AI 工具
- 你不需要切换场景
- 你习惯手动配置

**推荐做法**：
1. 先用 magpie 配置好所有工具
2. 创建 2-3 个常用 profiles
3. 日常用 magpie 切换场景
4. 临时测试用工具界面切换
