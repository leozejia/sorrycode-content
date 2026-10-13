---
title: 如何选择模型
slug: how-to-choose
order: 2
summary: 根据任务类型、预算和性能需求选择合适的模型，而不是盲目使用最贵或最新的模型。
section: models
section_title: 模型
section_order: 5
---

# 如何选择模型

不同的任务适合不同的模型。**最贵的不一定是最合适的**，这页帮你根据实际需求选择模型。

## 选择原则

### 原则 1：先动态查询

不要根据文档中的模型名称选择，先查询你的 Key 当前可用的模型：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key" | \
  jq -r '.data[].id'
```

或使用 magpie：

```bash
magpie models
```

👉 [完整查询指南](/docs/models/how-to-query)

### 原则 2：按任务分类

不同任务对模型的要求不同：

| 任务类型 | 优先考虑 | 推荐模型类型 |
|---------|---------|------------|
| **复杂架构设计** | 质量 > 成本 > 速度 | Opus, GPT-Sol |
| **日常开发** | 性价比 > 速度 | Sonnet, DeepSeek |
| **简单修改** | 速度 > 成本 | Haiku, Flash |
| **大量重复任务** | 成本 > 速度 | DeepSeek, Gemini Flash |
| **生产代码审查** | 质量 > 成本 | Opus, GPT-Sol |

### 原则 3：理解模型层级

大多数模型厂商都有层级划分：

**Claude**：
- **Opus** - 最高质量，最贵，最慢
- **Sonnet** - 平衡性能，中等价格
- **Haiku** - 最快速，最便宜

**GPT**：
- **Sol** - 推理专家，支持 ultra reasoning
- **Astra/Luna** - 平衡或快速版本

**DeepSeek**：
- **V4 Pro** - 标准版本
- **Flash** - 快速版本

**通用规则**：
- 名称中带 "flash" 通常更快更便宜
- 版本号越高通常越新越好
- 不同变体（sol/astra/luna）有不同优化方向

## 按场景选择

### 场景 1：生产环境

**需求**：
- 代码质量至关重要
- 可以接受较高成本
- 延迟不是主要问题

**推荐策略**：
- 主力：选择 Opus 或 GPT-Sol 类型
- 备选：Sonnet 类型作为备用
- Reasoning effort: high/xhigh/max

**示例配置**：
```bash
# 查询可用的高质量模型
magpie models | grep -E "opus|sol"

# 配置工作模式
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
magpie save production
```

### 场景 2：日常开发

**需求**：
- 质量足够好即可
- 成本需要控制
- 需要快速响应

**推荐策略**：
- 主力：Sonnet 或 DeepSeek 类型
- 备选：Flash 类型应对简单任务
- Reasoning effort: medium/high

**示例配置**：
```bash
# 查询平衡型模型
magpie models | grep -E "sonnet|deepseek"

# 配置日常模式
magpie claude sorrycode/claude-sonnet-5-5 effort high
magpie codex sorrycode/deepseek-v4-pro effort medium
magpie save daily
```

### 场景 3：快速迭代

**需求**：
- 简单任务为主
- 成本极度敏感
- 速度优先

**推荐策略**：
- 主力：Haiku 或 Flash 类型
- 备选：Gemini Flash（免费或低成本）
- Reasoning effort: low/medium

**示例配置**：
```bash
# 查询快速模型
magpie models | grep -E "haiku|flash"

# 配置快速模式
magpie claude sorrycode/claude-haiku-4-5 effort medium
magpie codex sorrycode/deepseek-flash effort low
magpie save fast
```

### 场景 4：实验和对比

**需求**：
- 测试不同模型效果
- 对比质量和成本
- 探索新模型

**推荐策略**：
- 配置多个模型
- 用同一任务测试
- 记录效果和成本

**示例配置**：
```bash
# 查询所有可用模型
magpie models

# 测试 Claude
magpie claude sorrycode/claude-opus-5-5
# 执行任务，记录效果

# 测试 GPT
magpie claude sorrycode/gpt-6.1-sol
# 执行同样任务，对比效果

# 测试 DeepSeek
magpie claude sorrycode/deepseek-v4-pro
# 对比性价比
```

## 按任务类型选择

### 复杂架构设计

**特点**：
- 需要深度推理
- 涉及多个模块
- 需要权衡多种方案

**推荐**：
- 优先：Opus 或 GPT-Sol
- Reasoning effort: xhigh/max
- 不要为了省钱用低档模型

### 功能实现

**特点**：
- 需要理解需求
- 编写新代码
- 可能需要重构

**推荐**：
- 优先：Sonnet 类型
- Reasoning effort: high
- 性价比最重要

### Bug 修复

**特点**：
- 需要理解现有代码
- 定位问题
- 修复后验证

**推荐**：
- 简单 bug：Haiku/Flash + medium
- 复杂 bug：Sonnet/Opus + high
- 根据复杂度选择

### 代码审查

**特点**：
- 需要发现潜在问题
- 评估代码质量
- 提出改进建议

**推荐**：
- 优先：Opus 或 GPT-Sol
- Reasoning effort: high/xhigh
- 质量比成本重要

### 文档生成

**特点**：
- 格式化输出
- 不需要复杂推理
- 量可能很大

**推荐**：
- 优先：Haiku/Flash
- Reasoning effort: low/medium
- 速度和成本优先

### 简单修改

**特点**：
- 格式调整
- 变量重命名
- 简单重构

**推荐**：
- 优先：Haiku/Flash
- Reasoning effort: low
- 不要浪费在高档模型上

## 按预算选择

### 预算充足

**策略**：
- 默认使用高档模型
- 不用担心成本
- 追求最佳质量

**配置**：
```bash
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
```

### 预算中等

**策略**：
- 主力用平衡模型
- 简单任务用快速模型
- 关键任务才用高档模型

**配置**：
```bash
# 日常用 Sonnet
magpie claude sorrycode/claude-sonnet-5-5 effort high

# 简单任务切换到 Haiku
magpie claude sorrycode/claude-haiku-4-5 effort medium
```

### 预算紧张

**策略**：
- 主力用开源模型
- 优先 DeepSeek/Gemini Flash
- 关键任务才用商业模型

**配置**：
```bash
# 主力用 DeepSeek
magpie claude sorrycode/deepseek-flash effort medium
magpie codex sorrycode/deepseek-v4-pro effort high

# 关键任务临时切换
magpie use production  # 切到高档模型
# 完成后切回
magpie use daily
```

## 如何测试和对比

### 第一步：选择测试任务

选择一个**代表性任务**：
- 不要太简单（看不出差异）
- 不要太复杂（成本太高）
- 能体现日常工作特点

### 第二步：用不同模型执行

```bash
# 测试模型 A
magpie claude sorrycode/claude-opus-5-5
# 执行任务，记录：
# - 完成时间
# - 代码质量
# - Token 消耗
# - 是否需要修改

# 测试模型 B
magpie claude sorrycode/claude-sonnet-5-5
# 执行同样任务，记录同样指标

# 测试模型 C
magpie claude sorrycode/deepseek-v4-pro
# 继续对比
```

### 第三步：综合评估

制作对比表格：

| 模型 | 完成时间 | 代码质量 | Token 成本 | 需要修改 | 综合评分 |
|------|---------|---------|-----------|---------|---------|
| Opus 5.5 | 60s | 优秀 | $0.50 | 否 | ⭐⭐⭐⭐⭐ |
| Sonnet 5.5 | 30s | 良好 | $0.20 | 一次 | ⭐⭐⭐⭐ |
| DeepSeek | 20s | 可用 | $0.05 | 两次 | ⭐⭐⭐ |

### 第四步：做出选择

根据你的实际需求权衡：
- 追求质量 → 选 Opus
- 追求性价比 → 选 Sonnet
- 追求成本 → 选 DeepSeek

## 常见问题

### Q: 总是用最新/最贵的模型不行吗？

**A**: 可以，但不划算。

- 简单任务用高档模型是浪费
- 成本会快速累积
- 性价比不是最优

**建议**：
- 关键任务用高档模型
- 日常任务用中档模型
- 简单任务用快速模型

### Q: 如何知道模型的能力？

**A**: 通过实际测试。

- 不要只看宣传
- 用你的实际任务测试
- 记录效果和成本

### Q: 模型版本号越高越好吗？

**A**: 通常是，但不绝对。

- 新版本通常更强
- 但可能更贵
- 可能有不同的优化方向

**建议**：
- 测试后再升级
- 不要盲目追新

### Q: 不同任务需要切换模型吗？

**A**: 建议用场景 profiles。

```bash
# 创建不同场景
magpie save production  # 高质量场景
magpie save daily       # 日常场景
magpie save fast        # 快速场景

# 根据任务切换
magpie use production   # 关键任务
magpie use daily        # 日常开发
magpie use fast         # 简单修改
```

### Q: 在工具界面里手动切换会丢失会话吗？

**A**: 取决于工具。

| 工具 | 界面切换 | magpie 切换 + 重启 |
|------|---------|-------------------|
| Codex | ✅ 不丢失 | ❌ 会丢失 |
| Claude Code | ✅ 不丢失 | ✅ 不丢失 |
| Pi | ✅ 不丢失 | ✅ 不丢失 |

**建议**：
- 有重要会话 → 在工具界面切换
- 每天开始/场景切换 → 用 magpie

## 进一步阅读

- [如何查询可用模型](/docs/models/how-to-query) - 动态查询模型列表
- [模型命名规则](/docs/models/naming-convention) - 理解模型命名
- [使用 magpie 管理模型](/docs/runtime/magpie) - 统一管理所有工具
