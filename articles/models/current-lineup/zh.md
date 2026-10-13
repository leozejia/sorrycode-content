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
# 使用 magpie
magpie claude sorrycode/claude-opus-5-5 effort max

# 或在工具界面中选择
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

### Claude Haiku 4.5

**模型 ID**：`claude-haiku-4-5-20251001`

**特点**：
- Claude 系列最快的模型
- 成本低
- 质量足够应对简单任务
- 支持 low/medium/high reasoning

**何时使用**：
- ✅ 简单代码修改
- ✅ 格式转换
- ✅ 文档生成
- ✅ 简单问答

**成本**：低

**配置示例**：
```bash
magpie claude haiku sorrycode/claude-haiku-4-5-20251001 effort medium
```

**注意**：当前最新 Haiku 是 4.5 版本。

---

### Gemini 3.8 Flash

**模型 ID**：`gemini-3.8-flash`

**特点**：
- Google 的快速模型
- 成本低
- 适合简单任务

**何时使用**：
- ✅ 成本极度敏感
- ✅ 简单重复任务
- ✅ 测试和验证

**成本**：极低

---

### DeepSeek V4 Pro

**模型 ID**：`deepseek-v4-pro`

**特点**：
- DeepSeek 的标准版本
- 比 Flash 慢但质量更好
- 性价比高

**何时使用**：
- ✅ 需要比 Flash 更好的质量
- ✅ 成本敏感但质量重要
- ✅ 日常开发

**成本**：低

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

### Claude Opus 4.6

**模型 ID**：`claude-opus-4-6`

**特点**：
- 上一代 Claude 旗舰模型
- 仍然很强大
- 成本相对 5.5 低一些

**何时使用**：
- ✅ 需要高质量但预算有限
- ✅ 对比不同版本效果

**成本**：中高

**注意**：推荐升级到 Opus 5.5。

---

## 如何选择模型

### 按任务类型选择

| 任务类型 | 推荐模型 | 备选 |
|---------|---------|------|
| **复杂架构设计** | Opus 5.5, GPT-6.1 Sol | Sonnet 5.5 |
| **日常开发** | Sonnet 5.5, DeepSeek Flash | DeepSeek V4 Pro |
| **简单修改** | Haiku 4.5, Gemini Flash | Sonnet 5.5 |
| **代码审查** | Opus 5.5, GPT-6.1 Sol | Sonnet 5.5 |
| **文档生成** | Haiku 4.5, Gemini Flash | Sonnet 5.5 |
| **测试对比** | Grok 4.7, GLM 5.3, Opus 4.6 | - |

### 按预算选择

| 预算 | 工作模式 | 快速模式 |
|------|---------|---------|
| **不限** | Opus 5.5 + GPT-6.1 Sol | Sonnet 5.5 |
| **中等** | Sonnet 5.5 + DeepSeek V4 Pro | DeepSeek Flash |
| **紧张** | DeepSeek Flash + DeepSeek V4 Pro | Haiku 4.5, Gemini Flash |

### 按场景选择

**生产环境**：
- 主力：Opus 5.5, GPT-6.1 Sol
- 备选：Sonnet 5.5

**开发环境**：
- 主力：Sonnet 5.5, DeepSeek Flash
- 备选：DeepSeek V4 Pro, Haiku 4.5

**测试环境**：
- 主力：Haiku 4.5, Gemini Flash
- 备选：DeepSeek Flash

## 查看可用模型

### 通过 API 查询

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key"
```

不同的 API key 可能返回不同的模型列表，取决于你的订阅分组。

### 通过 magpie 查看

如果你使用 magpie：

```bash
# 查看所有可用模型
magpie models

# 查看某个 provider 的模型
magpie provider sorrycode
```

## 用 magpie 管理模型

如果你使用多个 AI 工具，推荐用 magpie 统一管理：

### 创建工作场景

```bash
# 工作模式：高质量
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
magpie pi sorrycode/claude-opus-5-5 thinking xhigh
magpie save work

# 快速模式：省钱
magpie claude sorrycode/claude-haiku-4-5-20251001 effort medium
magpie codex sorrycode/deepseek-v4-pro effort medium
magpie pi sorrycode/deepseek-flash thinking low
magpie save fast

# 切换
magpie use work
magpie use fast
```

👉 [完整指南：使用 magpie 管理所有 AI 工具](/docs/runtime/magpie)

## 模型更新记录

### 2026-10-13
- ✅ 当前推荐：`claude-opus-5-5`, `claude-sonnet-5-5`
- ✅ 当前推荐：`gpt-6.1-sol`
- ✅ 当前推荐：`deepseek-flash`, `deepseek-v4-pro`
- ⚠️ 过时但可用：`claude-opus-4-6` → 推荐升级到 `claude-opus-5-5`
- ⚠️ 过时但可用：`gpt-5.6-sol` → 推荐升级到 `gpt-6.1-sol`（如果可用）

### 如何保持更新

1. **查看 sorrycode 控制台**：最新模型会第一时间出现
2. **查询 API**：定期查询你的 key 返回的模型列表
3. **关注文档更新**：这页会保持同步

## 常见问题

### Q: 哪个模型最好？

**A**: 没有"最好"，只有"最合适"。

- 追求质量 → Opus 5.5, GPT-6.1 Sol
- 追求性价比 → Sonnet 5.5, DeepSeek Flash
- 追求速度 → Haiku 4.5, Gemini Flash

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

- `claude-opus-4-6` 仍然可用，但 `claude-opus-5-5` 更强
- 旧版本可能逐渐被弃用

### Q: 我的 key 没有某个模型怎么办？

**A**: 不同的 API key 分组包含不同的模型。

解决方法：
1. 检查你的订阅分组
2. 联系 sorrycode 支持
3. 使用其他可用的模型

### Q: reasoning effort 是什么？

**A**: 控制模型的推理深度。

- `low/medium` - 快速响应，适合简单任务
- `high/xhigh` - 深度推理，适合复杂任务
- `max/ultra` - 最深推理，适合最复杂任务（成本高）

推荐：
- 日常用 `medium` 或 `high`
- 复杂任务用 `xhigh`
- 只在必要时用 `max` 或 `ultra`

## 进一步阅读

- [如何选择模型](/docs/models/how-to-choose) - 详细的选择指南
- [使用 magpie 管理模型](/docs/runtime/magpie) - 统一管理所有 AI 工具
- [GPT 系列详解](/docs/models/gpt-family) - GPT-6.1 详细对比
- [Claude 系列详解](/docs/models/claude-family) - Opus, Sonnet, Haiku 对比
