---
title: Pi Agent
slug: pi-agent
order: 1
summary: Install Pi Agent and configure multiple SorryCode API keys for GPT, Gemini, Grok, DeepSeek, GLM, Kimi, Qwen, and other Responses models, then verify text and file tools.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: pi
group_title: Pi Agent
group_order: 23
---

# Pi Agent

Pi is a terminal coding agent from [earendil-works/pi](https://github.com/earendil-works/pi). It can read projects, edit files, and run commands. Pi is not tied to a specific model, and it does not have to use only one model. You can configure multiple keys, multiple providers, and multiple models in one file, including GPT, Gemini, Grok, and Chinese models such as DeepSeek, GLM, Kimi, and Qwen.

This guide covers the Pi project hosted at [pi.dev](https://pi.dev/), not another project with the same name.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="prepare-key">Prepare API Keys</h2>

Pi calls models through SorryCode's OpenAI-compatible Responses API. On the [SorryCode API Key page](https://sorrycode.com/keys), prepare a key for each model group you want, such as GPT, Gemini, Grok, or a Chinese model group.

Different keys belong to different groups and expose different models. First, list the models available to each key:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <PASTE YOUR SORRYCODE API KEY HERE>"
```

Use `curl.exe` in Windows PowerShell:

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <PASTE YOUR SORRYCODE API KEY HERE>"
```

Follow three rules when configuring models:

- Use the exact model ID returned by `/v1/models`.
- The list is the main source of truth for the selected key group, but it may not expose every routable alias. If a model should support Responses but is missing, verify it with a minimal `/v1/responses` request before adding it to `models.json`.
- Give each key its own provider name. Pi stores API keys per provider, so logging into the same provider again overwrites the old key.

For example, if the Gemini group returns `gemini-3.7-flash`, use the Gemini-group key for `gemini-3.7-flash`. If the Grok group returns `grok-4.6`, use the Grok-group key for `grok-4.6`.

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

<h2 id="configure">Configure Multiple Models in models.json</h2>

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

If the file already contains other providers, merge the example below into the existing `providers` object instead of replacing it. The following example shows multiple keys, multiple providers, and multiple models:

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
    "sorrycode-gemini": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "gemini-3.7-flash",
          "name": "Gemini 3.7 Flash",
          "contextWindow": 1048576,
          "maxTokens": 65536,
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
    "sorrycode-grok": {
      "baseUrl": "https://sorrycode.com/v1",
      "api": "openai-responses",
      "models": [
        {
          "id": "grok-4.6",
          "name": "Grok 4.6",
          "contextWindow": 500000,
          "maxTokens": 500000,
          "input": ["text", "image"],
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "low",
            "medium": "medium",
            "high": "high"
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
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "low",
            "medium": "medium",
            "high": "high",
            "xhigh": "xhigh",
            "max": "max"
          }
        },
        {
          "id": "glm-5.2",
          "name": "GLM-5.2",
          "contextWindow": 1000000,
          "maxTokens": 131072,
          "input": ["text"],
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "high",
            "medium": "high",
            "high": "high",
            "max": "max"
          }
        },
        {
          "id": "kimi-k3",
          "name": "Kimi K3",
          "contextWindow": 1048576,
          "maxTokens": 131072,
          "input": ["text", "image"],
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "low",
            "high": "high",
            "max": "max"
          }
        },
        {
          "id": "qwen3.8-max",
          "name": "Qwen3.8 Max",
          "contextWindow": 1000000,
          "maxTokens": 131072,
          "input": ["text", "image"],
          "reasoning": true,
          "thinkingLevelMap": {
            "low": "low",
            "medium": "medium",
            "xhigh": "xhigh"
          }
        }
      ]
    }
  }
}
```

Provider names are local identifiers, such as `sorrycode-gpt`, `sorrycode-gemini`, `sorrycode-grok`, and `sorrycode-cn`. One account can have multiple keys; give each key its own provider. The `models` array under `sorrycode-cn` can contain multiple Chinese models, but only when the key's group actually returns those models.

Field reference:

- `id`: the exact model ID sent to the API, taken from that key's `/v1/models`.
- `contextWindow`: Pi uses this for context accounting and automatic compaction. Defaults to 128,000 when omitted.
- `maxTokens`: maximum output tokens for one response. Defaults to 16,384 when omitted.
- `input`: `["text"]` for text-only models; `["text", "image"]` for multimodal models.
- `reasoning`: set to `true` when the model supports reasoning.
- `thinkingLevelMap`: controls which thinking levels appear in Pi. `xhigh` and `max` only appear when they are explicitly mapped.

Without a `thinkingLevelMap`, Pi exposes levels only through `high` by default. Do not copy another model's map; follow that model's official reasoning support.

<h2 id="login">Save an API Key for Each Provider</h2>

Start Pi:

```bash
pi
```

Log in once per provider:

```text
/login sorrycode-gpt
/login sorrycode-gemini
/login sorrycode-grok
/login sorrycode-cn
```

Paste the key for that group with each command. Pi stores credentials in its own authentication file. You do not need an environment variable, and keys should not be added to `models.json`.

Then use `/model` to select a provider and model, such as `sorrycode-gemini/gemini-3.7-flash`.

Confirm the configuration and auth before starting work:

```bash
pi --list-models
pi auth check --provider sorrycode-gemini --model gemini-3.7-flash --json
```

`--list-models` shows all configured models. `auth check` should return `ready` when that provider has a usable key.

<h2 id="verify">Verify Text and Tool Calls</h2>

Use any available model for a minimal text request. This example uses `gemini-3.7-flash`:

```bash
pi --provider sorrycode-gemini --model gemini-3.7-flash --no-tools --no-session -p "Reply with PI_SORRYCODE_OK only."
```

After Pi prints `PI_SORRYCODE_OK`, verify the file tool in an empty test directory:

```bash
mkdir pi-sorrycode-test
cd pi-sorrycode-test
pi --provider sorrycode-gemini --model gemini-3.7-flash --no-session -p "Create pi-check.txt containing PI_TOOL_OK and a final newline. Do not modify other files."
```

When the task finishes, confirm that `pi-check.txt` exists and contains `PI_TOOL_OK`. This verifies the model connection and Pi's tool-calling path.

<h2 id="thinking">Set the Thinking Level</h2>

In an interactive session, press `Shift+Tab` to cycle thinking levels or use `/settings` to set the default. You can also start Pi with a pinned level:

```bash
pi --provider <provider> --model <model>:<level>
```

For example:

```bash
pi --provider sorrycode-gemini --model gemini-3.7-flash:max
```

Verify whether a thinking level actually works with a minimal request instead of trusting the map alone. If upstream returns `400` with a message like `level "xhigh" not supported`, that level is currently unavailable even when Pi displays it.

<h2 id="common-issues">Common Issues</h2>

- `pi` is not found: close and reopen the terminal, then confirm that npm's global command directory is on `PATH`
- A provider is missing from `/login`: save `models.json`, then restart Pi
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

References: [Pi website](https://pi.dev/), [Pi repository](https://github.com/earendil-works/pi), and [Pi custom models](https://pi.dev/docs/latest/models).
