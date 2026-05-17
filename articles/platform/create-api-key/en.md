---
title: Create API Key
slug: create-api-key
order: 4
summary: Understand what an API key is, then create an sk-... key in the SorryCode console for Codex, Claude Code, or Skills.
section: platform
section_title: Platform
section_order: 8
---

# Create API Key

An `API` is the channel tools use to talk to models.

When you chat with AI in a browser, you type into a web page. Tools like `Codex`, `Claude Code`, and `Skills` do not click web pages like humans do. They need a software-to-software way to request a model. That way is called an API.

An `API Key` is the key on that channel. It proves that this is your SorryCode account using the model. It usually starts with `sk-...`.

No matter whether you use Codex, Claude Code, CC-Switch, an image skill, or manual setup, this step is unavoidable. The current one-click installers also ask for the API key during the flow, so it is better to prepare it first inside the console.

## The Shortest Path

1. Open `https://sorrycode.com/login` and sign in to the SorryCode console
2. Find `API Keys` inside the console
3. If you do not have one yet, create a new key
4. Copy it and store it safely

What you should end up with is an `sk-...`.

The quick link is:

`https://sorrycode.com/keys`

But do not rely on the URL alone. A first-time user usually needs to know where this page sits inside the console.

## What You Actually Need to Remember

As a beginner, remember three lines:

- `API` is the channel
- `API Key` is the key
- `SorryCode` is where you create the key, manage balance, and connect tools to models

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
- Unsure how runtimes and models relate: [Platform / Tools Are Not Models](/docs/platform/tools-and-models)
- Want a minimal validation first: [Platform / First Request](/docs/platform/first-request)
- Want less terminal work: [Tools / CC-Switch](/docs/tools/cc-switch)
