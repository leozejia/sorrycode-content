---
title: Create API Key
slug: create-api-key
order: 4
summary: Understand what an API key is, then create separate sk-... keys for Codex, Claude Code, Skills, or other uses.
section: platform
section_title: Platform
section_order: 8
---

# Create API Key

An `API` is the channel tools use to talk to models.

When you chat with AI in a browser, you type into a web page. Tools like `Codex`, `Claude Code`, and `Skills` do not click web pages like humans do. They need a software-to-software way to request a model. That way is called an API.

An `API Key` is the key on that channel. It proves that this is your SorryCode account using the model. It usually starts with `sk-...`.

No matter whether you use Codex, Claude Code, CC-Switch, an image skill, or manual setup, this step is unavoidable. The current one-click installers also ask for the API key during the flow, so it is better to prepare it first inside the console.

One SorryCode balance can have multiple API keys. As a beginner, do not force every tool to share the same key.

If you want to use both Codex and Claude Code, create two keys:

```text
one key for Codex
one key for Claude Code
```

This does not split your balance. The balance is still shared. Separate keys make usage records, group switching, spending limits, and troubleshooting much clearer.

## The Shortest Path

1. Open `https://sorrycode.com/login` and sign in to the SorryCode console
2. Find `API Keys` in the left menu
3. Create a new key
4. Name it by use, such as `Codex`, `Claude Code`, or `Image Skill`
5. Select a group
6. Copy the key and store it safely

What you should end up with is an `sk-...`.

The quick link is:

`https://sorrycode.com/keys`

But do not rely on the URL alone. A first-time user usually needs to know where this page sits inside the console.

![API Keys entry in the console sidebar](./api-key-menu.png)

## What to Fill In

The name is only for you. Use the tool or purpose:

```text
Codex
Claude Code
Image Skill
Test Request
```

The group decides which model group and billing multiplier this key uses. You can switch the group later from the API key list.

The spending limit controls the maximum balance this key can consume. `0` means no separate limit. Beginners can leave it alone first, then add limits after regular usage starts.

The rate limit controls request frequency. It is not the model multiplier. If you are just using Codex or Claude Code normally, you usually do not need to enable it first.

The key expiration is useful for temporary test keys. Long-term Codex / Claude Code keys usually do not need an expiration date at the start.

![When creating a key, start with the name and group](./create-key-dialog.png)

## What You Actually Need to Remember

As a beginner, remember three lines:

- `API` is the channel
- `API Key` is the key
- `SorryCode` is where you create the key, manage balance, and connect tools to models

Then remember one more line:

```text
one balance can have multiple API keys.
```

You can create separate keys for separate tools. For example: one for Codex, one for Claude Code, and one for an image skill. They use the same balance, but management and troubleshooting become much clearer.

If you use one-click install, the installer writes most config for you. You usually do not need to understand `Base URL` first.

Only continue with the values below when you are configuring manually:

- API Key: the `sk-...` value you just created
- which Base URL your target workbench needs

If you use `Codex` and other OpenAI-compatible paths, the Base URL is:

- `{{API_BASE_URL}}`

If you use `Claude Code` and other Anthropic-compatible paths, the Base URL is:

- `{{ANTHROPIC_BASE_URL}}`

Some runtime field names can look misleading.

For example, `Claude Code` calls the field `ANTHROPIC_AUTH_TOKEN`, but the value inside it is still the same `sk-...`.

## How to Use It After Creation

After creation, the console shows the full key. Copy the `sk-...` value.

![Copy the API key after creation](./key-created-copy.png)

If you use the Codex or Claude Code one-click installer, the installer will stop and ask you to paste an API key. Paste the `sk-...` value there.

If you already created a key, the API key list lets you:

- copy the key
- rename it
- switch its group
- set a spending limit
- disable or delete keys you no longer use

Do not force every tool into one key. Separate keys make later usage records much easier to understand.

![You can switch groups from the API key list](./key-group-switch.png)

## Security Rules

- do not commit it into a repo
- do not paste it into public chats
- do not put it directly into long-lived shell history
- revoke and recreate it immediately if it leaks

## Next

- Unsure whether SorryCode fits you: [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for)
- Want to understand AI cost: [Platform / How AI Cost Works](/docs/platform/ai-cost-basics)
- Want to start with Codex: [Runtime / Codex](/docs/runtime/codex)
- Want to start with Claude Code: [Runtime / Claude Code](/docs/runtime/claude-code)
- Unsure how runtimes and models relate: [Platform / Tools Are Not Models](/docs/concepts/tools-models-platform)
- Want a minimal validation first: [Platform / First Request](/docs/platform/create-api-key)
- Want less terminal work: [Tools / CC-Switch](/docs/tools/cc-switch)
