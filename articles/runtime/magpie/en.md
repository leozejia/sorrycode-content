---
title: magpie - Unified Model Management
slug: magpie
order: 0
summary: Use magpie to manage model configurations for Claude Code, Codex, Pi, and other AI tools in one place, switch scenarios with a single command.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: magpie
group_title: Unified Management
group_order: 5
---

# magpie - Unified Model Management

If you use multiple AI tools (Claude Code, Codex, Pi, Cursor, etc.), magpie makes configuration management simple.

## What is magpie

magpie is a **local model gateway** that:
- Runs at `127.0.0.1:3425`
- Manages model configurations for all AI tools in one place
- Supports one-command model and scenario switching
- Supports automatic multi-account rotation

**An analogy**:
- Without magpie: Each AI tool has its own config file, you need to edit N files
- With magpie: All AI tools access models through magpie, you only change one place

## Why magpie

### Problem 1: Scattered Configuration

**Without magpie**:
```
Claude Code → ~/.claude/settings.json
Codex       → ~/.codex/config.toml
Pi          → ~/.pi/agent/settings.json
Cursor      → ~/.cursor/config.json
```

Every time you want to switch models, you need to edit 4 files.

**With magpie**:
```bash
magpie claude sorrycode/claude-opus-5-5
magpie codex sorrycode/gpt-6.1-sol
magpie pi sorrycode/claude-opus-5-5
magpie cursor sorrycode/claude-sonnet-5-5
```

One command, done.

### Problem 2: Scenario Switching is Hard

You have different work scenarios:
- **Production mode**: Use best models (Opus 5.5, GPT-6.1 Sol)
- **Fast mode**: Use cheap models (DeepSeek Flash, Haiku)
- **Experiment mode**: Test new models (Grok, GLM)

**Without magpie**:
- Need to remember each scenario's config
- Need to edit all files when switching

**With magpie**:
```bash
magpie use work       # Production mode
magpie use fast       # Fast mode
magpie use experiment # Experiment mode
```

### Problem 3: Multi-Account Management is Complex

You have 3 sorrycode accounts and want automatic rotation:
- Account 1 runs out of quota → auto switch to account 2
- Account 2 also runs out → auto switch to account 3

**Without magpie**: Manually check quota, manually change config

**With magpie**: Automatic handling, seamless

## Quick Start

### Step 1: Install magpie

```bash
curl -fsSL https://usemagpie.ai/install.sh | sh
```

After installation:
- macOS: `/Applications/magpie.app` + `~/.local/bin/magpie`
- Can use GUI or CLI

### Step 2: Add sorrycode providers

magpie needs to know your API keys. Get API keys from [sorrycode console](https://sorrycode.com/keys).

**Recommended config** (covers all models):

```bash
# Main provider (Claude + GPT + DeepSeek)
magpie provider add "SorryCode" \
  url=https://api.sorrycode.com/v1 \
  key=sk-your-main-key

# Claude dedicated (native Anthropic API, more stable)
magpie provider add "SorryCode Claude" \
  url=https://sorrycode.com \
  key=sk-your-claude-key \
  anthropic=true

# GPT dedicated
magpie provider add "SorryCode GPT" \
  url=https://sorrycode.com/v1 \
  key=sk-your-gpt-key \
  responses=true

# Chinese models (DeepSeek, GLM)
magpie provider add "SorryCode CN" \
  url=https://sorrycode.com/v1 \
  key=sk-your-cn-key \
  responses=true
```

**Minimal config** (one key):

```bash
magpie provider add "SorryCode" \
  url=https://api.sorrycode.com/v1 \
  key=sk-your-key
```

### Step 3: Configure model list

Tell magpie which models each provider has.

**Query available models**:

```bash
# Check which models your key has
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer sk-your-key"
```

**Configure models**:

```bash
# Main provider
magpie provider models sorrycode \
  claude-opus-5-5 \
  claude-sonnet-5-5 \
  claude-haiku-4-5-20251001 \
  gpt-6.1-sol \
  deepseek-v4-pro

# Claude provider (if configured)
magpie provider models sorrycode-claude \
  claude-opus-5-5 \
  claude-sonnet-5-5

# GPT provider (if configured)
magpie provider models sorrycode-gpt \
  gpt-6.1-sol

# CN provider (if configured)
magpie provider models sorrycode-cn \
  deepseek-flash \
  glm-5.3-prime
```

### Step 4: Configure your AI tools

Set default models for each tool:

```bash
# Save current config (just in case)
magpie save baseline

# Configure Claude Code
magpie claude sorrycode/claude-opus-5-5 effort max

# Configure Codex
magpie codex sorrycode/gpt-6.1-sol effort xhigh

# Configure Pi
magpie pi sorrycode/gpt-6.1-sol thinking xhigh

# Configure Cursor (if you use it)
magpie cursor sorrycode/claude-sonnet-5-5
```

**Note**: You need to restart the corresponding tool after configuration for changes to take effect.

### Step 5: Verify configuration

```bash
# View all tool configurations
magpie agents

# View all available models
magpie models

# View provider details
magpie provider sorrycode
```

## Scenario Management

### Create work scenarios

**Scenario 1: Production mode (high quality)**

```bash
magpie claude sorrycode/claude-opus-5-5 effort max
magpie codex sorrycode/gpt-6.1-sol effort xhigh
magpie pi sorrycode/claude-opus-5-5 thinking xhigh
magpie save work
```

**Scenario 2: Fast mode (save money)**

```bash
magpie claude sorrycode/claude-haiku-4-5-20251001 effort medium
magpie codex sorrycode/deepseek-v4-pro effort medium
magpie pi sorrycode/deepseek-flash thinking low
magpie save fast
```

**Scenario 3: Experiment mode (test new models)**

```bash
magpie claude sorrycode/claude-sonnet-5-5 effort high
magpie codex sorrycode/gpt-6.1-sol effort high
magpie pi sorrycode/deepseek-flash thinking medium
magpie save experiment
```

### Switch scenarios

```bash
# Morning work
magpie use work

# Afternoon simple edits
magpie use fast

# Friday experiments
magpie use experiment

# Restore initial config
magpie use baseline
```

## Integration with AI Tools

### Claude Code

magpie manages Claude Code's model configuration:

```bash
# Switch main model
magpie claude sorrycode/claude-opus-5-5

# Switch haiku model (fast tasks)
magpie claude haiku sorrycode/claude-haiku-4-5-20251001

# Switch reasoning effort
magpie claude effort max
```

**Note**: Claude Code takes effect immediately, no restart needed.

👉 [Full guide: Claude Code](/docs/runtime/claude-code)

### Codex / ChatGPT

magpie manages Codex's model configuration:

```bash
# Switch model
magpie codex sorrycode/gpt-6.1-sol

# Switch reasoning effort
magpie codex effort xhigh
```

**Note**: After switching, you need to restart Codex and Codex app-server:
```bash
codex app-server daemon restart
# Then restart Codex app
```

**Session loss issue**:
- ✅ Switch model in Codex UI → sessions not lost
- ❌ magpie command + restart → sessions lost

**Recommendation**:
- Have important sessions → switch in tool UI
- Scenario switching/daily start → use magpie command

👉 [Full guide: Codex](/docs/runtime/codex)

### Pi Agent

magpie manages Pi's model configuration:

```bash
# Switch model
magpie pi sorrycode/gpt-6.1-sol

# Switch thinking level
magpie pi thinking xhigh
```

**Note**: Pi takes effect immediately, no restart needed.

👉 [Full guide: Pi Agent](/docs/runtime/pi-agent)

### Cursor

magpie manages Cursor's model configuration:

```bash
# Switch model
magpie cursor sorrycode/claude-sonnet-5-5
```

**Note**: You need to restart Cursor after switching.

👉 [Full guide: Cursor](/docs/runtime/cursor)

## Common Commands

### View status

```bash
# View all providers
magpie providers

# View all models
magpie models

# View all AI tool status
magpie agents

# View provider details
magpie provider sorrycode

# View quota
magpie quota
```

### Switch configuration

```bash
# Switch individual tool's model
magpie claude sorrycode/claude-opus-5-5
magpie codex sorrycode/gpt-6.1-sol

# Switch reasoning level
magpie claude effort max
magpie codex effort xhigh
```

### Profile management

```bash
# Save current config
magpie save <profile-name>

# Switch profile
magpie use work
magpie use fast
magpie use experiment

# View all profiles
magpie profiles

# Restore initial config
magpie use baseline
```

## FAQ

### Q: Does magpie replace original config?

**A**: No. magpie is **enhancement**, not replacement.

- ✅ Original provider config is still there
- ✅ You can still manually switch models in tool UI
- ✅ magpie is just an additional option

**You can mix**:
- Daily use magpie for quick scenario switching
- Temporary testing in tool UI manual selection

### Q: Will switching with magpie lose sessions?

**A**: Depends on the tool.

| Tool | magpie switch + restart | Tool UI switch |
|------|------------------------|----------------|
| Codex | ❌ Will lose | ✅ Won't lose |
| Claude Code | ✅ Won't lose (no restart) | ✅ Won't lose |
| Pi | ✅ Won't lose (no restart) | ✅ Won't lose |
| Cursor | ❌ Will lose | ✅ Won't lose |

**Recommendation**:
- Have important sessions → use tool UI
- Scenario switching → use magpie command

## Further Reading

- [Claude Code](/docs/runtime/claude-code) - Claude Code detailed guide
- [Codex](/docs/runtime/codex) - Codex detailed guide
- [Pi Agent](/docs/runtime/pi-agent) - Pi Agent detailed guide
