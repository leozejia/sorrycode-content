---
title: 如何查询可用模型
slug: how-to-query
order: 1
summary: 动态查询你的 API Key 可用的模型，而不是依赖静态文档列表。
section: models
section_title: 模型
section_order: 5
---

# 如何查询可用模型

sorrycode 聚合了多家 AI 模型，模型列表会持续更新。**不要依赖静态文档**，应该动态查询你的 API Key 当前可用的模型。

## 为什么要动态查询

❌ **不推荐**：查看文档中的"当前模型列表"
- 模型更新快，文档容易过时
- 不同的 API Key 分组有不同的模型
- 新模型上线后文档可能还没更新

✅ **推荐**：每次需要时动态查询
- 总是获取最新的模型列表
- 看到你的 Key 真正可用的模型
- 不会错过新上线的模型

## 查询方法

### 方法 1：使用 API（推荐）

最直接的方式是调用 sorrycode API：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key"
```

返回示例：

```json
{
  "data": [
    {
      "id": "claude-opus-5-5",
      "object": "model",
      "created": 1234567890,
      "owned_by": "anthropic"
    },
    {
      "id": "gpt-6.1-sol",
      "object": "model",
      "created": 1234567890,
      "owned_by": "openai"
    }
  ]
}
```

**提取模型 ID**：

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-你的key" | \
  jq -r '.data[].id'
```

### 方法 2：使用 magpie

如果你使用 magpie，可以更方便地查询：

```bash
# 查看所有可用模型
magpie models

# 查看某个 provider 的模型
magpie provider sorrycode

# 查看某个 provider 的详细信息
magpie provider sorrycode-claude
```

magpie 会显示：
- 模型 ID
- 模型名称
- 支持的 reasoning levels
- 是否支持图片输入

### 方法 3：在工具界面中查看

大多数 AI 工具都有模型选择界面：

**Codex / ChatGPT**：
- 打开 Codex App
- 点击右下角的模型名称
- 查看可用模型列表

**Claude Code**：
- 在命令行运行 `claude`
- 使用 `/model` 命令查看可用模型

**Pi Agent**：
- 查看 `~/.pi/agent/models.json`
- 或运行 `pi --list-models`

## 理解返回结果

### 模型 ID

模型 ID 是你在配置中使用的标识符，例如：
- `claude-opus-5-5`
- `gpt-6.1-sol`
- `deepseek-flash`
- `grok-4.7`

### 模型命名规则

不同厂商有不同的命名规则：

**Claude**：`claude-{tier}-{version}`
- tier: opus, sonnet, haiku（质量递减）
- version: 5-5, 4-6 等

**GPT**：`gpt-{version}-{variant}`
- version: 6.1, 5.6 等
- variant: sol, astra, luna 等

**其他**：
- DeepSeek: `deepseek-{variant}`
- Grok: `grok-{version}`
- Gemini: `gemini-{version}-flash`

👉 [完整命名规则说明](/docs/models/naming-convention)

## 查询不同分组的模型

sorrycode 使用分组 Key 管理不同模型集合。同一个账号可能有多个分组 Key。

### 查询你有哪些分组

1. 登录 [sorrycode 控制台](https://sorrycode.com/keys)
2. 查看你的 API Keys 列表
3. 每个 Key 会显示所属分组（如 "Claude 分组"、"GPT 分组"）

### 查询每个分组的模型

为每个 Key 分别查询：

```bash
# Claude 分组
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-claude-key"

# GPT 分组
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-gpt-key"

# 国产模型分组
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-cn-key"
```

## 配置查询到的模型

### 使用 magpie

```bash
# 1. 添加 provider
magpie provider add "SorryCode" \
  url=https://sorrycode.com/v1 \
  key=sk-你的key

# 2. 查询可用模型
magpie provider sorrycode

# 3. 配置你想用的模型
magpie provider models sorrycode \
  claude-opus-5-5 \
  gpt-6.1-sol \
  deepseek-flash

# 4. 在工具中使用
magpie claude sorrycode/claude-opus-5-5
magpie codex sorrycode/gpt-6.1-sol
```

### 手动配置

不同工具的配置方式不同：

**Codex**：编辑 `~/.codex/config.toml`

**Claude Code**：编辑 `~/.claude/settings.json`

**Pi Agent**：编辑 `~/.pi/agent/models.json`

详见各工具的文档。

## 保持模型列表更新

### 定期重新查询

建议：
- 每周查询一次新模型
- 有新功能发布时立即查询
- 遇到配置问题时先查询确认

### 订阅更新通知

1. 关注 sorrycode 控制台的通知
2. 查看 [sorrycode 更新日志](https://sorrycode.com/changelog)
3. 加入 sorrycode 社区

## 常见问题

### Q: 我查询到的模型比文档少怎么办？

**A**: 这是正常的。

- 不同分组 Key 包含不同的模型
- 检查你的订阅和分组
- 联系 sorrycode 支持确认

### Q: 查询失败怎么办？

**A**: 检查以下几点：

1. **API Key 是否正确**
   ```bash
   echo $SORRYCODE_API_KEY
   ```

2. **网络是否连通**
   ```bash
   curl https://sorrycode.com/v1/models
   ```

3. **Key 是否过期或被禁用**
   - 登录控制台检查状态

### Q: 查询到的模型在工具中不可用？

**A**: 可能的原因：

1. **工具未重启**
   - Codex 需要重启
   - Claude Code 实时生效
   - Pi 实时生效

2. **配置格式错误**
   - 检查模型 ID 是否正确
   - 检查 provider 配置

3. **模型 ID 拼写错误**
   - 重新查询确认正确的 ID

### Q: 同一个模型在不同 provider 中？

**A**: 这是正常的。magpie 支持 routing groups：

```bash
# 同一模型在多个账号
magpie provider models sorrycode-1 claude-opus-5-5
magpie provider models sorrycode-2 claude-opus-5-5

# 创建 routing group（自动切换）
magpie group add "Opus Cluster" \
  models=sorrycode-1/claude-opus-5-5,sorrycode-2/claude-opus-5-5 \
  routing=smart
```

## 进一步阅读

- [如何选择模型](/docs/models/how-to-choose) - 根据任务选择合适的模型
- [模型命名规则](/docs/models/naming-convention) - 理解不同模型的命名
- [使用 magpie 管理模型](/docs/runtime/magpie) - 统一管理所有 AI 工具
