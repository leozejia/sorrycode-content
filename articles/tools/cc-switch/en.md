---
title: CC-Switch
slug: cc-switch
order: 1
summary: An advanced config-switching tool for graphical endpoint, API key, and multi-runtime configuration management.
section: tools
section_title: Tools
section_order: 28
---

# CC-Switch

If one-click install already works and you later need to switch endpoints, API keys, or runtime configs often, then CC-Switch is worth looking at.

It is not the runtime itself. It is the local tool that manages endpoint switching, API keys, and config state for you.

Reference: [CC-Switch project repository](https://github.com/farion1231/cc-switch)

## Who this fits

This path is better if:

- you want graphical config management
- you switch between multiple endpoints
- you do not want to remember where env vars live
- you want to get online first and understand runtime details later

## What you get from it

CC-Switch is useful for consolidating:

- endpoint configuration
- API key configuration
- multi-site switching
- local runtime config management

## How to connect SorryCode

1. Sign in to SorryCode
2. Go to [Getting Started / Create API Key](/docs/start/create-api-key)
3. Click the CCS import action from the key list
4. Or create the config manually
5. Fill in the address and key required by your runtime

For OpenAI-compatible flows, the typical values are:

- Base URL: `{{API_BASE_URL}}`
- API Key: your `sk-...`

For Claude Code flows, CC-Switch usually maps to the Claude-side config template instead.

## When it is better than manual setup

Prefer CC-Switch when:

- you do not want to manage `export / setx`
- you switch between multiple providers often
- you want to keep endpoint setup separate from runtime launch details

## How it relates to one-click install

Beginners should start with one-click install by default.

CC-Switch is not a required prerequisite. It is an advanced config-switching tool for users who already know which endpoints, API keys, or runtime configs they need to manage.

## Next

- Want Codex: [Runtime / Codex](/docs/runtime/codex)
- Want Claude Code: [Runtime / Claude Code](/docs/runtime/claude-code)
- Want the shared prerequisite page: [Environment / Node.js](/docs/environment/nodejs)
