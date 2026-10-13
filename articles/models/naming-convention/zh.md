---
title: 模型命名规则
slug: naming-convention
order: 3
summary: 理解不同 AI 厂商的模型命名规则，快速识别模型的类型、版本和能力。
section: models
section_title: 模型
section_order: 5
---

# 模型命名规则

不同的 AI 厂商使用不同的命名规则。理解这些规则可以帮你快速判断模型的类型和能力。

## 通用规则

### 基本格式

大多数模型遵循：`{厂商}-{系列}-{版本}-{变体}`

例如：
- `claude-opus-5-5` → Claude 厂商，Opus 系列，5.5 版本
- `gpt-6.1-sol` → GPT 厂商，6.1 版本，Sol 变体
- `deepseek-flash` → DeepSeek 厂商，Flash 变体

### 层级指示

很多厂商用名称表示质量层级：

**高档模型**：
- `opus`（拉丁语：作品）
- `pro`（专业版）
- 数字版本号较高

**中档模型**：
- `sonnet`（十四行诗）
- `standard`（标准版）

**快速模型**：
- `haiku`（俳句，短小精悍）
- `flash`（闪电）
- `lite`（轻量版）

### 变体标识

同一版本可能有不同变体：

**GPT 变体**：
- `sol` → 推理专家（soliloquy，独白）
- `astra` → 平衡版本（astra，星辰）
- `luna` → 快速版本（luna，月亮）

**DeepSeek 变体**：
- `v4-pro` → 标准版本
- `flash` → 快速版本

## Claude 系列

### 命名格式

`claude-{tier}-{major}-{minor}`

**示例**：
- `claude-opus-5-5` → Opus 5.5
- `claude-sonnet-4-6` → Sonnet 4.6
- `claude-haiku-4-5-20251001` → Haiku 4.5（日期版本）

### Tier 说明

Claude 使用文学体裁命名层级：

**Opus**（歌剧）：
- 最高质量和能力
- 最适合复杂任务
- 成本最高，速度最慢

**Sonnet**（十四行诗）：
- 平衡质量和速度
- 适合日常开发
- 性价比高

**Haiku**（俳句）：
- 最快速响应
- 适合简单任务
- 成本最低

### 版本号

- **主版本号**：如 5, 4（能力代次）
- **次版本号**：如 5, 6（同代改进）
- 版本号越高通常能力越强

### 日期版本

某些模型带日期标识：
- `claude-haiku-4-5-20251001`
- 日期：2025年10月1日的版本
- 用于区分同一版本的不同快照

## GPT 系列

### 命名格式

`gpt-{version}-{variant}`

**示例**：
- `gpt-6.1-sol` → GPT 6.1 Sol
- `gpt-6.1-astra` → GPT 6.1 Astra
- `gpt-6-luna` → GPT 6 Luna
- `gpt-5.6` → GPT 5.6（基础版）

### 版本号

- **主版本**：如 6, 5（能力代次）
- **次版本**：如 .1, .6（改进版本）
- 更高版本通常更强

### 变体说明

GPT 6.1 系列有多个变体：

**Sol**（独白）：
- 推理专家
- 支持 ultra reasoning effort
- 适合复杂推理任务
- 成本最高

**Astra**（星辰）：
- 平衡版本
- 质量和速度均衡
- 适合大多数任务

**Luna**（月亮）：
- 快速版本
- 响应速度快
- 适合简单任务

## DeepSeek 系列

### 命名格式

`deepseek-{variant}`

**示例**：
- `deepseek-v4-pro` → DeepSeek V4 Pro
- `deepseek-flash` → DeepSeek Flash
- `deepseek-v3` → DeepSeek V3

### 变体说明

**V4 Pro**：
- 标准版本
- 性价比高
- 适合日常开发

**Flash**：
- 快速版本
- 成本极低
- 适合大量任务

### 版本迭代

- V4 > V3 > V2
- 更新版本通常更强
- 但价格可能也更高

## Gemini 系列

### 命名格式

`gemini-{version}-{variant}`

**示例**：
- `gemini-3.8-flash` → Gemini 3.8 Flash
- `gemini-3.7-flash` → Gemini 3.7 Flash

### 版本说明

- 版本号如 3.8, 3.7
- 更高版本能力更强

### Flash 变体

- 当前主要是 Flash 变体
- 快速且成本低
- 适合简单任务

## Grok 系列

### 命名格式

`grok-{version}`

**示例**：
- `grok-4.7` → Grok 4.7
- `grok-4.6` → Grok 4.6

### 特点

- xAI 的模型
- 实时数据接入
- 独特的回答风格

## GLM 系列

### 命名格式

`glm-{version}-{variant}`

**示例**：
- `glm-5.3-prime` → GLM 5.3 Prime
- `glm-4` → GLM 4

### 变体说明

**Prime**：
- 高级版本
- 智谱 AI 的旗舰模型
- 中文能力强

## 如何快速识别模型

### 看名称识别层级

**高档模型标识**：
- `opus` → Claude 最高档
- `sol` → GPT 推理专家
- `pro` → 专业版本
- `prime` → 高级版本

**快速模型标识**：
- `flash` → 快速版本
- `haiku` → Claude 最快
- `luna` → GPT 快速版
- `lite` → 轻量版

### 看版本号识别新旧

- **Claude**: 5.x > 4.x
- **GPT**: 6.x > 5.x
- **DeepSeek**: V4 > V3
- **Gemini**: 3.8 > 3.7

### 看厂商识别特点

**Anthropic (Claude)**：
- 代码能力强
- 推理质量高
- 遵循指令好

**OpenAI (GPT)**：
- 通用能力强
- 生态丰富
- 支持插件多

**DeepSeek**：
- 性价比高
- 开源友好
- 中文能力好

**Google (Gemini)**：
- 多模态强
- 成本低
- 更新快

**xAI (Grok)**：
- 实时数据
- 独特风格
- 创新实验

## 实际应用

### 根据名称选择

**需要最高质量**：
```bash
# 查找 opus 或 sol
magpie models | grep -E "opus|sol"
```

**需要快速响应**：
```bash
# 查找 flash 或 haiku
magpie models | grep -E "flash|haiku|luna"
```

**需要性价比**：
```bash
# 查找 sonnet 或 deepseek
magpie models | grep -E "sonnet|deepseek"
```

### 根据版本选择

**选择最新版本**：
```bash
# Claude: 找最高版本号
magpie models | grep claude | grep "5-"

# GPT: 找 6.x 系列
magpie models | grep gpt | grep "6\."
```

## 常见问题

### Q: 版本号一定越高越好吗？

**A**: 通常是，但不绝对。

- 新版本通常更强
- 但可能更贵
- 可能有不同的优化方向

**建议**：测试后再决定。

### Q: 同一版本的不同变体怎么选？

**A**: 根据任务需求。

- 复杂任务 → Sol/Pro
- 日常任务 → Astra/Standard
- 简单任务 → Luna/Flash

### Q: 模型名称会变吗？

**A**: 会。

- 厂商可能调整命名
- 旧版本可能被弃用
- 新变体可能出现

**建议**：动态查询，不要硬编码。

### Q: 如何知道新模型上线？

**A**: 定期查询。

```bash
# 每周查询一次
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key" | \
  jq -r '.data[].id' > models-$(date +%Y%m%d).txt

# 对比上次查询
diff models-20261001.txt models-20261008.txt
```

### Q: 模型命名有官方文档吗？

**A**: 有些厂商有，有些没有。

- Anthropic: 有官方文档
- OpenAI: 有官方文档
- 其他: 可能没有

**建议**：根据实际可用模型理解命名规则。

## 进一步阅读

- [如何查询可用模型](/docs/models/how-to-query) - 动态查询模型列表
- [如何选择模型](/docs/models/how-to-choose) - 根据任务选择
- [使用 magpie 管理模型](/docs/runtime/magpie) - 统一管理
