---
title: Tools Are Not Models
slug: tools-and-models
order: 3
summary: Understand workbenches, models, API keys, and Base URLs first, then start with the default GPT→Codex and Claude→Claude Code paths.
section: platform
section_title: Platform
section_order: 8
---

# Tools Are Not Models

First-time users often mix these together:

```text
Codex, Claude Code, GPT, Claude, API Key, Base URL, SorryCode
```

This page answers one question:

```text
Am I using a tool, or am I using a model?
```

Remember this:

```text
Codex / Claude Code are workbenches. GPT / Claude are models. SorryCode connects workbenches to models.
```

## What Each Name Means

| Name | Beginner meaning |
| --- | --- |
| `SorryCode` | provides API keys, balance, and model access |
| `Codex` | the GPT-path AI workbench |
| `Claude Code` | the Claude-path AI workbench |
| `GPT / Claude / Gemini` | the models that understand, reason, and generate |
| `API Key` | the key proving the request belongs to your account |
| `Base URL` | the address your workbench uses to connect to SorryCode |

The app you open is usually not the model. It is the workbench.

The workbench reads files, organizes context, calls tools, and runs commands. The model understands, reasons, and generates.

SorryCode lets those workbenches call models through your API key and records usage from your balance.

## Default Path

If you are not sure, start with the default path.

| What you want | Default entry |
| --- | --- |
| GPT / OpenAI-compatible path | [Runtime / Codex](/docs/runtime/codex) |
| Claude / Anthropic-compatible path | [Runtime / Claude Code](/docs/runtime/claude-code) |
| Create a key first | [Platform / Create API Key](/docs/platform/create-api-key) |
| Understand cost first | [Platform / How AI Cost Works](/docs/platform/ai-cost-basics) |

If you have no strong preference, start with `Codex`.

It is the most direct beginner entry for the GPT path.

## Why Not Cross-Wire Everything First

You may see people say:

```text
Claude Code can run GPT.
```

```text
Some agents can connect to many custom models.
```

Often, that is true.

But can run does not mean it should be your beginner default.

An agent request contains more than your latest sentence. It may include history, tool definitions, file snippets, project rules, compacted summaries, and the workbench's own state.

Different workbenches organize that context differently.

If the workbench and model are not a good default pairing, you may see:

- each conversation feels like it rereads the project
- context reuse is worse than expected
- the same task consumes more usage
- long sessions become slower
- responses arrive, but progress is weak

This is not about ranking tools.

It is about choosing the default path first.

Get the default path working before experimenting with custom connections.

## What One-Click Install Does

One-click install tries to connect three things:

```text
workbench + SorryCode endpoint + your API key
```

For example:

- Codex install connects Codex to `{{API_BASE_URL}}`
- Claude Code install connects Claude Code to `{{ANTHROPIC_BASE_URL}}`
- the installer asks for your own `sk-...`

You do not need to understand every config file on day one.

Just know that the installer connects your workbench to SorryCode.

## Where Cost Fits

Cost is not the main topic of this page.

Use this first:

```text
AI usage usually maps back to input, output, and cache.
```

To understand why an agent can use a lot even when the visible reply is short, read [Platform / How AI Cost Works](/docs/platform/ai-cost-basics).

## Next

- Unsure whether SorryCode fits you: [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for)
- Want to understand cost: [Platform / How AI Cost Works](/docs/platform/ai-cost-basics)
- GPT path: [Runtime / Codex](/docs/runtime/codex)
- Claude path: [Runtime / Claude Code](/docs/runtime/claude-code)
- No API key yet: [Platform / Create API Key](/docs/platform/create-api-key)
