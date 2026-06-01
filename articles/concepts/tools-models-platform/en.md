---
title: "Tools, Models, Platforms — Stop Confusing Them"
slug: tools-models-platform
order: 7
summary: GPT, Claude, Codex, Claude Code, Cursor, DeepSeek, Qwen — these names fall into three layers: models are the brain, workbenches are the body, platforms are the infrastructure. Don't chase model names. Pick your workbench first — where you produce work is where AI should stack its buffs.
section: concepts
section_title: Core Concepts
section_order: 5
---

# Tools, Models, Platforms — Stop Confusing Them

You may already be overwhelmed by these names:

```text
GPT, Claude, DeepSeek, Qwen, Gemini
Codex, Claude Code, Cursor, Copilot
SorryCode, OpenAI, Anthropic, various API gateways
```

Thrown together, they all look like the same kind of thing.

They're not.

<h2 id="three-layers">The Three Layers</h2>

Sort these names into three layers, and everything becomes clear:

```text
Bottom layer: Models (the brain)
  GPT, Claude, DeepSeek, Qwen, Gemini
  Responsible for: understanding, reasoning, generating content

Middle layer: Workbench / Runtime (the body)
  Codex, Claude Code, Cursor, Copilot
  Responsible for: reading files, executing commands, organizing context, calling tools

Top layer: Platform (the infrastructure)
  SorryCode, OpenAI official, Anthropic official, various API gateways
  Responsible for: API access, billing, key management
```

Think of it like buying a car:

```text
Model = engine (built by Volkswagen/Toyota/Honda)
Workbench = car body (different automakers build different cars with the same engine)
Platform = gas station (where you fuel up, how you pay)
```

A good engine doesn't mean a good car. A good car body doesn't mean fuel efficiency. A convenient gas station doesn't make the car faster.

Three layers, each doing its own job.

<h2 id="why-layers-matter">Why You Must Separate These Three</h2>

Because the most common beginner mistake is: **chasing model names.**

"GPT-5 is out! I need to use GPT-5!"
"Claude Opus has the highest benchmark scores! Switch to Claude!"
"DeepSeek is cheaper! Switch everything to DeepSeek!"

Chasing model names is like chasing engine specs. The engine matters, but if you put it in a car that doesn't fit your needs, a great engine won't help.

```text
The same model, mounted on different workbenches, can perform completely differently.
```

Why? Because the workbench determines:
- What context the model can see
- What tools the model can use
- How context is organized and cached
- How sessions are maintained and history is compressed

These "workbench decisions" often affect your experience more than the model itself.

```text
Pick the workbench first, then the model.
```

<h2 id="how-to-choose">How to Choose: Workbench First, Model Second</h2>

The default rule is simple:

```text
You primarily use GPT → pick Codex as your workbench
You primarily use Claude → pick Claude Code as your workbench
You primarily use a specific Chinese model → check if its vendor has an Agent client
```

Why this pairing? Each workbench is designed and optimized first and foremost for its "home" model. Context organization, caching strategy, prompt formatting — all tuned for that model.

Cross-combinations can work. But they might not be cost-effective.

```text
Codex + Claude can work.
But context reuse, cache hits, consumption control —
these may not be as good as the native pairing.
Beginners: take the default path first. Experiment later.
```

<h2 id="convergence">Everyone Is Building Agents</h2>

You may have noticed: model vendors are all launching their own Agents.

OpenAI has Codex. Anthropic has Claude Code. Google has Gemini integrations everywhere. DeepSeek, Qwen, and other Chinese vendors — each is building their own Agent solution.

This is not a coincidence.

```text
Model vendors understand better than anyone:
AI that can only chat is a demo.
AI that can do work and operate a computer is the product.
```

What does this mean for ordinary users?

You don't need to chase. Whichever model vendor you pick, they likely already have or will soon have a corresponding Agent workbench. What you need isn't "the best model" — it's "pick a workbench and complete one task end to end."

<h2 id="dont-chase">What Not to Do</h2>

Three beginner traps:

**1. Don't chase benchmark leaderboards**

Today this one scores highest. Tomorrow that one. Benchmark scores are lab data — they may have nothing to do with your actual task. A model that's 2 points better at math reasoning won't write better meeting notes for you.

**2. Don't try too many tools at once**

Install Codex, then Cursor, then Claude Code — four tools in three days, none of them used to complete a single task.

Pick one first. Take one task from start to finish. Then decide whether to switch.

**3. Don't cross-wire setups after reading two tutorials**

There are tutorials online showing how to run GPT through Claude Code, or DeepSeek through Cursor. It can work. But for beginners — walk the default path first. Advanced configs come later.

<h2 id="map">A Map</h2>

| Where you are now | Recommendation |
| --- | --- |
| I know nothing | Start with [What AI Actually Is](/docs/concepts/what-is-ai) |
| I want to try, not sure what to install | Install Codex — simplest beginner entry point |
| I primarily use GPT | [Runtime / Codex](/docs/runtime/codex) |
| I primarily use Claude | [Runtime / Claude Code](/docs/runtime/claude-code) |
| I use a Chinese model | Check the vendor's Agent client; setup logic is similar |
| I want multi-model access through one entry | Use SorryCode as a unified API gateway, switch models as needed |
| I'm already using it, want to manage it better | [Agent Advanced](/docs/agent-infra/overview) |

<h2 id="remember">Remember One Thing</h2>

```text
Model is the brain. Workbench is the body. Platform is the infrastructure.
Don't chase model names.
Pick your workbench first — where you produce work is where AI stacks its buffs.
```

<h2 id="next">Next Step</h2>

All the concepts are covered. Last chapter: where do you actually start?

[Where to Start](/docs/concepts/where-to-start)
