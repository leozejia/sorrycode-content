---
title: Runtimes and Models
slug: runtime-models
order: 2
summary: Understand Codex, Claude Code, protocols, and models so you do not connect a model to the wrong runtime and waste API usage.
section: platform
section_title: Platform
section_order: 8
---

# Runtimes and Models

Beginners often mix up `Codex`, `Claude Code`, `gpt-5.4`, and `claude-sonnet-4-5`.

Remember this first:

```text
A runtime is not a model. The runtime drives the workflow; the model does the thinking.
```

`Codex` and `Claude Code` are agent runtimes. They read projects, send requests, edit files, and run commands. The model behind them is what consumes API usage.

<h2 id="five-pieces">Separate These Five Pieces</h2>

| Name | What it does | Beginner meaning |
| --- | --- | --- |
| `Model` | thinks and generates text or images | the engine, such as GPT or Claude |
| `Agent Runtime` | reads files, edits files, runs commands, and manages context | the AI workbench, such as Codex or Claude Code |
| `Skills` | tell the agent how to do a class of tasks | capability packs installed into the workbench |
| `MCP` | connects agents to external tools and data | an advanced connection method; beginners do not need it first |
| `SorryCode` | provides API keys, balance, and model access | the place that connects workbenches to models |

You do not need to learn `MCP` or protocol details on day one. What affects cost and experience first is which workbench you open and which model it calls.

<h2 id="simple-map">The Simple Map</h2>

Start with this mental model:

| Tool you open | Default protocol mental model | Recommended model mental model | Beginners should avoid |
| --- | --- | --- | --- |
| `Codex` | OpenAI-compatible | GPT models such as `gpt-5.4` | Forcing Claude models into Codex |
| `Claude Code` | Anthropic-compatible | Claude models such as `claude-sonnet-4-5` | Forcing GPT models into Claude Code |
| `OpenClaw` | Custom / OpenAI-compatible | Advanced custom connection | Treating it as a drop-in Codex replacement for GPT |
| `Hermes Agent` | Custom endpoint | Advanced custom connection | Treating it as a drop-in Codex replacement for GPT |

This does not mean cross-wiring is technically impossible. It means beginners should not treat it as the default path. The highest-value default pairings are `Codex + GPT` and `Claude Code + Claude`. `OpenClaw / Hermes Agent` can be useful advanced custom connections, but do not assume their GPT cache and cost behavior equals Codex.

<h2 id="why-it-costs-more">Why the Wrong Pair Can Cost More</h2>

An agent runtime does not simply forward your words to a model.

It also handles:

- project context
- conversation state
- tool calls
- history compaction
- cache behavior
- protocol-specific request formatting

If you run `gpt-5.4` through `Claude Code / OpenClaw / Hermes Agent`, or a Claude model through `Codex`, several things can happen:

- the runtime request format may not match what the model is optimized for
- context cache hit rate may drop
- the same task may send more tokens
- conversation history may be billed more repeatedly
- it may still “work”, but cost more than it should

So the question is not only whether it can run. The question is whether it is worth running that way.

<h2 id="beginner-rule">Beginner Rule</h2>

If you are unsure, use these two rules:

```text
Use GPT models through Codex first.
```

```text
Use Claude models through Claude Code first.
```

Do not chase a new model name by putting it into a random runtime.

If someone says “Claude Code can also run GPT,” treat that as an advanced experiment, not the default cheap path.

<h2 id="what-sorrycode-installs">What SorryCode One-Click Install Does</h2>

SorryCode one-click install does more than install the tool. It writes a matched default setup:

- `Runtime / Codex`
  - OpenAI-compatible Base URL
  - GPT model defaults
  - the default main entry for GPT paths
- `Runtime / Claude Code`
  - Anthropic-compatible Base URL
  - Claude model defaults
  - the default main entry for Claude paths
- `OpenClaw / Hermes Agent`
  - advanced custom connections
  - useful for gateway compatibility checks, but not the beginner default cost-saving path

This is why beginners should start with one-click install instead of hand-editing config files.

<h2 id="when-change-model">When to Change Models</h2>

You can change models, but only after you know:

- which runtime you are using
- whether it uses OpenAI-compatible or Anthropic-compatible protocol
- whether the target model fits that runtime
- cache, context, and billing behavior may change
- you need to watch usage, not just whether the response returns

If you want a newer GPT model, prefer changing it inside `Codex`, for example:

```bash
codex -m gpt-5.5
```

If you want a Claude model, prefer using Claude Code's own configuration path.

<h2 id="cost-check">How to Notice a Bad Pairing</h2>

Pause and check the runtime-model pairing if:

- usage grows quickly after only a few prompts
- you did not ask for a large code change, but usage is high
- every conversation feels like it rereads the whole project
- you put a GPT model name into `Claude Code / OpenClaw / Hermes Agent` but expect Codex-like cost behavior
- you put a Claude model name into `Codex`

Go back to the default path first:

- GPT models: [Runtime / Codex](/docs/runtime/codex)
- Claude models: [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="next">Next</h2>

- GPT / Codex path: [Runtime / Codex](/docs/runtime/codex)
- Claude Code path: [Runtime / Claude Code](/docs/runtime/claude-code)
- Manual protocol check: [Platform / First Request](/docs/platform/first-request)
