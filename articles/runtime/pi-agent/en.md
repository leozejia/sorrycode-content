---
title: Pi Agent
slug: pi-agent
order: 1
summary: Install Pi Agent, connect it to a Responses-compatible SorryCode model, and verify both text and file tools.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: pi
group_title: Pi Agent
group_order: 23
---

# Pi Agent

Pi is a terminal coding agent from [earendil-works/pi](https://github.com/earendil-works/pi). It can read projects, edit files, and run commands. Pi is not tied to a specific model. This guide connects Pi to SorryCode and completes a first agent task with a Responses-compatible model available to your API key.

This guide covers the Pi project hosted at [pi.dev](https://pi.dev/), not another project with the same name.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="prepare-key">Prepare an API Key</h2>

Pi calls models through SorryCode's OpenAI-compatible Responses API. On the [SorryCode API Key page](https://sorrycode.com/keys), choose a key whose group exposes a Responses-compatible model. You can reuse an existing compatible key. Create another key only when you need separate usage records, spending limits, or credential rotation.

First, list the models available to this key:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <PASTE YOUR SORRYCODE API KEY HERE>"
```

Use `curl.exe` in Windows PowerShell:

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <PASTE YOUR SORRYCODE API KEY HERE>"
```

Prefer an exact model ID from the response when you configure Pi. The list is the main source of truth for the selected key group, but it may not expose every routable alias. If you know a model should support Responses but it is missing from the list, verify it with a minimal `/v1/responses` request before adding it to `models.json`. Do not guess model names from web pages or tutorials.

Different keys on the same account can belong to different groups and expose different models. Pi stores API keys per provider, so logging into the same provider again overwrites the old key. If you use several groups at once, such as GPT, Gemini, Grok, and DeepSeek, create a separate provider for each group, for example `sorrycode-gpt`, `sorrycode-cn`, and `sorrycode-grok`.

This example includes both `deepseek-v4-flash` and `deepseek-v4-pro`; `deepseek-v4-flash` is the model verified for this guide. Pi is not limited to DeepSeek. Other Responses-compatible models work as well. Availability ultimately depends on what that key can successfully call.

<h2 id="install">Install Pi</h2>

Pi currently requires Node.js `22.19.0` or newer. Check your environment first:

```bash
node --version
npm --version
```

If either command is missing or Node.js is too old, read [Node.js](/docs/environment/nodejs). Then install the official Pi package:

```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

The same npm command works on macOS, Linux, and Windows. Confirm the install:

```bash
pi --version
```

<h2 id="configure">Configure the SorryCode Provider</h2>

Pi reads custom models from:

- macOS / Linux: `~/.pi/agent/models.json`
- Windows: `%USERPROFILE%\.pi\agent\models.json`

On macOS or Linux, create the directory and open the file:

```bash
mkdir -p ~/.pi/agent
nano ~/.pi/agent/models.json
```

In Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$HOME\.pi\agent" | Out-Null
notepad "$HOME\.pi\agent\models.json"
```

If the file already contains other providers, merge `sorrycode` into the existing `providers` object instead of replacing the file:

```json
{
  "providers": {
    "sorrycode": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "deepseek-v4-flash",
          "name": "DeepSeek V4 Flash via SorryCode",
          "contextWindow": 1000000,
          "maxTokens": 384000,
          "input": ["text"],
          "reasoning": true
        },
        {
          "id": "deepseek-v4-pro",
          "name": "DeepSeek V4 Pro via SorryCode",
          "contextWindow": 1000000,
          "maxTokens": 384000,
          "input": ["text"],
          "reasoning": true,
          "thinkingLevelMap": {
            "off": null,
            "minimal": null,
            "low": "low",
            "medium": "high",
            "high": "high",
            "xhigh": "high",
            "max": "max"
          }
        }
      ]
    }
  }
}
```

To use another Responses-compatible model, replace `id` with an exact model ID returned by `/v1/models` and update `name` if needed. The `models` array can contain multiple entries. Set `"reasoning": true` only when the selected model supports reasoning; otherwise set it to `false`.

For multiple keys, do not put every key into the same `sorrycode` provider. Create one provider per key. `baseUrl` and `api` can stay the same; `models` should only contain the models that key can call:

```json
{
  "providers": {
    "sorrycode-gpt": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "gpt-5.6-sol",
          "name": "GPT-5.6 Sol",
          "contextWindow": 1050000,
          "maxTokens": 128000,
          "input": ["text", "image"],
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "low",
            "medium": "medium",
            "high": "high",
            "xhigh": "xhigh",
            "max": "max"
          }
        }
      ]
    },
    "sorrycode-cn": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "deepseek-v4-flash",
          "name": "DeepSeek V4 Flash",
          "contextWindow": 1000000,
          "maxTokens": 384000,
          "input": ["text"],
          "reasoning": true
        }
      ]
    }
  }
}
```

Provider names are local identifiers, such as `sorrycode-gpt`, `sorrycode-cn`, or `sorrycode-grok`. Save each key separately with `/login <provider>` so keys do not overwrite each other.

DeepSeek's official Pi configuration gives both V4 Pro and V4 Flash a 1,000,000-token context window and a 384,000-token maximum output. Pi uses `contextWindow` to calculate context usage and automatic compaction, while `maxTokens` limits a single response. Both fields must be set explicitly. Without them, Pi falls back to 128,000 and 16,384.

Pi only exposes thinking levels through `high` by default for a custom model. The `thinkingLevelMap` for `deepseek-v4-pro` follows the model's current official rules: `low` remains `low`; `medium`, `high`, and `xhigh` use `high`; and `max` remains `max`. Pi only shows the extended `xhigh` and `max` choices when they are declared explicitly. Do not copy this map to another model unless its official documentation defines the same behavior.

After configuration, verify the supported thinking levels with a minimal request instead of trusting the map alone. If upstream returns `400` with a message like `level "xhigh" not supported`, that level is currently unavailable even when Pi displays it.

In an interactive session, press `Shift+Tab` to cycle thinking levels or use `/settings` to set the default. You can also start Pi with a pinned level:

```bash
pi --provider <provider> --model <model>:<level>
```

For example: `pi --provider sorrycode-gpt --model gpt-5.6-sol:max`.

<h2 id="login">Save the API Key</h2>

Start Pi:

```bash
pi
```

Enter `/login <provider>`, for example `/login sorrycode` or `/login sorrycode-cn`, and paste the key for that provider. Pi stores it in its own authentication file. You do not need an environment variable, and the key should not be added to `models.json`. With multiple keys, log in once per provider name and do not reuse one provider name for different keys.

Enter `/model` and select the model you configured. With the example configuration on this page, select either `sorrycode/deepseek-v4-flash` or `sorrycode/deepseek-v4-pro`. After selecting Pro, you can set the default thinking level to `max` in `/settings`.

Confirm the configuration and auth before starting work:

```bash
pi --list-models
pi auth check --provider sorrycode-cn --model deepseek-v4-flash --json
```

`--list-models` shows the models you configured. `auth check` should return `ready` when the provider has a usable key.

<h2 id="verify">Verify Text and Tool Calls</h2>

Start with the recommended `deepseek-v4-flash` model. When using another model, replace the model ID in the command:

```bash
pi --provider sorrycode --model deepseek-v4-flash --no-tools --no-session -p "Reply with PI_SORRYCODE_OK only."
```

After Pi prints `PI_SORRYCODE_OK`, verify the file tool in an empty test directory:

```bash
mkdir pi-sorrycode-test
cd pi-sorrycode-test
pi --provider sorrycode --model deepseek-v4-flash --no-session -p "Create pi-check.txt containing PI_TOOL_OK and a final newline. Do not modify other files."
```

When the task finishes, confirm that `pi-check.txt` exists and contains `PI_TOOL_OK`. This verifies both the model connection and agent tool calls.

<h2 id="common-issues">Common Issues</h2>

- `pi` is not found: close and reopen the terminal, then confirm that npm's global command directory is on `PATH`
- `sorrycode` is missing from `/login`: save `models.json`, then restart Pi
- The target model is missing from `/model`: check the JSON syntax, authentication status, model entry, and key group
- `401`: the key is incomplete, expired, or does not match the selected group
- `404` or model not found: query `/v1/models` again and use an exact ID from the response
- Pi can reply but cannot create a file: use a verified model and confirm that the task allows the `write` tool
- Windows blocks `pi.ps1`: read [Windows PowerShell](/docs/environment/windows-powershell)
- `/v1/responses` returns `502`: the model may be listed but the upstream group is temporarily unavailable; retry or check SorryCode status before changing Pi config
- `400` with `level "..." not supported`: the upstream model does not support that thinking level; use a supported level or set that entry to `null` in `thinkingLevelMap`
- A model is in `models.json` but missing from `/model`: confirm the provider is logged in with `pi auth check --provider <provider> --model <model> --json`
- A model ID is missing from `/v1/models`: do not copy it blindly; run a minimal `/v1/responses` request and add it only if that request succeeds
- Models from another key are missing: do not overwrite one provider with another key; create a separate provider for that key group

This page recommends and verifies Pi `0.84.1` with `deepseek-v4-flash`. Both the minimal text request and the `write` tool call passed. Pi can also use other Responses-compatible models available through SorryCode.

References: [Pi website](https://pi.dev/), [Pi repository](https://github.com/earendil-works/pi), [Pi custom models](https://pi.dev/docs/latest/models), and [DeepSeek with Pi Mono](https://api-docs.deepseek.com/quick_start/agent_integrations/pi_mono).
