---
title: Tools Are Not Models
slug: tools-and-models
order: 2
summary: Understand what SorryCode, Codex, Claude Code, GPT, and Claude each do, then choose the default pairing before experimenting with custom setups.
section: platform
section_title: Platform
section_order: 8
---

# Tools Are Not Models

When people first use SorryCode, they often mix several things together: `Codex`, `Claude Code`, `GPT`, `Claude`, `API Key`, and `Base URL`.

Do not start by memorizing every term. Start with two rules:

```text
If you want GPT, start with Codex.
```

```text
If you want Claude, start with Claude Code.
```

Other combinations may be technically possible. They are just not the beginner default. On day one, the goal is to get a stable path working, not to debug compatibility.

<h2 id="what-each-piece-does">What Each Piece Does</h2>

Use this first mental model:

| Name | Beginner meaning |
| --- | --- |
| `SorryCode` | provides API keys, balance, and model access |
| `Codex` | the GPT workbench for reading projects, editing files, and running commands |
| `Claude Code` | the Claude workbench for reading projects, editing files, and running commands |
| `GPT / Claude` | the models that think and generate output |
| `API Key` | the key that proves the request belongs to your account |
| `Base URL` | the address your workbench uses to connect to SorryCode |

The app you open is usually not the model. It is the workbench.

Workbenches such as `Codex` and `Claude Code` read files, organize context, call tools, and run commands. Models such as `GPT` and `Claude` generate responses and decide the next step.

SorryCode connects the workbench to the model and records usage through your API key.

<h2 id="which-one-to-use">Which One Should I Use</h2>

If you just want to start, use this table:

| What you want to do | Start here |
| --- | --- |
| Use GPT for projects, file edits, and long tasks | [Runtime / Codex](/docs/runtime/codex) |
| Use Claude for projects, file edits, and long tasks | [Runtime / Claude Code](/docs/runtime/claude-code) |
| Create a key first | [Platform / Create API Key](/docs/platform/create-api-key) |
| Manually verify the key and endpoint | [Platform / First Request](/docs/platform/first-request) |
| Use OpenClaw or Hermes Agent | Treat it as an advanced custom setup |

If you have no strong preference, start with `Codex`. It is the most direct beginner path for GPT.

<h2 id="why-not-cross-wire">Why Not Cross-Wire Everything First</h2>

You may see people say that `Claude Code` can run GPT, `OpenClaw` can connect GPT, or `Hermes Agent` can use custom models.

Often, that is true.

But can run does not mean it should be your default path.

An agent request contains more than your latest sentence. It may include project context, tool definitions, history, file snippets, compacted summaries, and the workbench's own state.

Different workbenches organize that context differently. If the model and workbench are not a good default pairing, you may see:

- every session feels like it rereads the project
- context reuse is worse than expected
- the same task consumes more API usage
- long sessions become expensive
- responses arrive, but progress is slow

This is not about ranking tools. It is about choosing the default path first.

Get the default path working before experimenting with custom connections.

<h2 id="sorrycode-one-click-install">What SorryCode One-Click Install Does</h2>

One-click install does more than install software.

It tries to match three things:

```text
workbench + SorryCode endpoint + your API key
```

For example:

- Codex install connects Codex to `{{API_BASE_URL}}`
- Claude Code install connects Claude Code to `{{ANTHROPIC_BASE_URL}}`
- the installer asks for your own `sk-...`

You do not need to understand every config file on day one. Just know that the installer connects the workbench to SorryCode for you.

<h2 id="when-to-change-model">When Can I Change Models</h2>

You can change models, but first confirm:

- which workbench you are using
- whether you want GPT or Claude
- whether you accept that cost, caching, and context behavior may change

If you want a newer GPT model, change it inside `Codex` first.

If you want a Claude model, use the Claude Code path first.

Do not chase a new model name by putting it into a random workbench.

<h2 id="bad-pairing-signals">Signs You May Be Using the Wrong Pairing</h2>

Pause and check the tool-model pairing if:

- usage grows quickly after little visible work
- each conversation feels like it rereads the project
- a small edit consumes a surprising amount of API usage
- you put GPT into Claude Code and expect Codex-like cost behavior
- you put Claude into Codex and expect Claude Code-like behavior

Return to the default path first:

```text
GPT -> Codex
Claude -> Claude Code
```

Cross-wire only after you know why you are doing it.

<h2 id="next">Next</h2>

- GPT path: [Runtime / Codex](/docs/runtime/codex)
- Claude path: [Runtime / Claude Code](/docs/runtime/claude-code)
- No API key yet: [Platform / Create API Key](/docs/platform/create-api-key)
- Manual request check: [Platform / First Request](/docs/platform/first-request)
- Long-term project context: [Agent Infra / Long-Lived Context](/docs/agent-infra/context-management)
