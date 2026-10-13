---
title: How to Query Available Models
slug: how-to-query
order: 1
summary: Dynamically query models available to your API Key instead of relying on static documentation lists.
section: models
section_title: Models
section_order: 5
---

# How to Query Available Models

sorrycode aggregates multiple AI models, and the model list is continuously updated. **Don't rely on static documentation** - query dynamically to see what models your API Key currently has access to.

## Why Query Dynamically

❌ **Not recommended**: Check "current model list" in documentation
- Models update frequently, docs can be outdated
- Different API Key groups have different models
- New models may be available before docs are updated

✅ **Recommended**: Query dynamically each time you need
- Always get the latest model list
- See models your Key actually has access to
- Won't miss newly launched models

## Query Methods

### Method 1: Use API (Recommended)

The most direct way is to call the sorrycode API:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-your-key"
```

Example response:

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

**Extract model IDs**:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-your-key" | \
  jq -r '.data[].id'
```

### Method 2: Use magpie

If you use magpie, querying is more convenient:

```bash
# View all available models
magpie models

# View models for a specific provider
magpie provider sorrycode

# View detailed provider information
magpie provider sorrycode-claude
```

magpie will show:
- Model ID
- Model name
- Supported reasoning levels
- Whether image input is supported

### Method 3: Check in Tool UI

Most AI tools have a model selection interface:

**Codex / ChatGPT**:
- Open Codex App
- Click the model name in the bottom right
- View available model list

**Claude Code**:
- Run `claude` in terminal
- Use `/model` command to view available models

**Pi Agent**:
- Check `~/.pi/agent/models.json`
- Or run `pi --list-models`

## Understanding Results

### Model ID

Model ID is the identifier you use in configuration, for example:
- `claude-opus-5-5`
- `gpt-6.1-sol`
- `deepseek-flash`
- `grok-4.7`

### Model Naming Rules

Different vendors have different naming conventions:

**Claude**: `claude-{tier}-{version}`
- tier: opus, sonnet, haiku (decreasing quality)
- version: 5-5, 4-6, etc.

**GPT**: `gpt-{version}-{variant}`
- version: 6.1, 5.6, etc.
- variant: sol, astra, luna, etc.

**Others**:
- DeepSeek: `deepseek-{variant}`
- Grok: `grok-{version}`
- Gemini: `gemini-{version}-flash`

👉 [Full naming convention guide](/docs/models/naming-convention)

## Further Reading

- [How to Choose Models](/docs/models/how-to-choose) - Choose right model for tasks
- [Model Naming Convention](/docs/models/naming-convention) - Understand model naming
- [Using magpie](/docs/runtime/magpie) - Unified management for all tools
