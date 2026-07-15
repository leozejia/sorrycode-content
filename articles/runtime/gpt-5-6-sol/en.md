---
title: How to Use GPT-5.6 Sol
slug: gpt-5-6-sol
order: 2
summary: Use GPT-5.6 Sol for complex professional work, choose reasoning effort intentionally, and validate leaner prompts on representative tasks.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# How to Use GPT-5.6 Sol

`gpt-5.6-sol` is the frontier model in the GPT-5.6 family. It is built for complex professional work, long context, and multi-step agent tasks. The `gpt-5.6` alias also routes to Sol.

If Codex is not connected yet, start with [Models & Runtimes / Codex](/docs/runtime/codex). This page does not repeat installation or API key setup. It explains how to choose Sol, control reasoning, and simplify prompts.

<h2 id="when-to-use">When to Choose Sol</h2>

| Task | Recommendation |
| --- | --- |
| Complex coding, research, debugging, or professional knowledge work | Good fit |
| Long context, repeated tool use, and ongoing verification | Good fit |
| Final quality matters more than latency and cost | Good fit |
| High-volume, cost-sensitive, repetitive work | Compare Terra or Luna first |
| A small format conversion or short question | A frontier model is not the default choice |

Sol has a 1,050,000-token context window and supports up to 128,000 output tokens. A larger window solves capacity. It does not decide which old information should remain in the session.

<h2 id="first-run">Shortest Working Path</h2>

1. Connect Codex and verify the API key and network path.
2. Select `gpt-5.6-sol`.
3. Start with `medium` reasoning effort.
4. State the goal, sources, approval boundaries, evidence, and completion criteria.
5. Compare quality, tokens, latency, and cost on real tasks before moving to `high`, `xhigh`, or `max`.

Use this for a first run:

```text
Goal: produce [specific deliverable].

Context:
- [why this work matters]
- [who will use it]

Sources of truth:
- [files, pages, or data that must be read]

Authorization:
- You may perform [local and reversible actions].
- Stop before [external writes, destructive actions, or a real scope change].

Completion criteria:
- [checkable result]
- [tests, citations, or browser verification]

Finish the work that is already in scope before reporting the result. Label unverified work explicitly.
```

<h2 id="reasoning-effort">Choose a Reasoning Effort</h2>

GPT-5.6 supports `none`, `low`, `medium`, `high`, `xhigh`, and `max`.

| Level | Good fit |
| --- | --- |
| `none` | A latency baseline for work that does not need reasoning or tools |
| `low` | Latency-sensitive work with clear boundaries |
| `medium` | Balanced default starting point |
| `high` / `xhigh` | More reasoning produces a measured quality gain |
| `max` | The hardest quality-first work where latency and cost are acceptable |

When migrating from an older model, preserve the current effort as a baseline, then compare the same level with one level lower. GPT-5.6 can keep or improve quality at a lower effort because it uses tokens more efficiently.

<h2 id="max-pro-ultra">Max, Pro, and Ultra Are Different Controls</h2>

| Name | What it controls |
| --- | --- |
| `max` | Reasoning effort for one GPT-5.6 instance |
| Pro mode | More model work from the same GPT-5.6 model, enabled with `reasoning.mode: "pro"` in the API |
| Ultra | A multi-agent setting in Codex that coordinates four agents by default |

Ultra is not a `reasoning.effort` level, and it is not a model called `gpt-5.6-sol-ultra`. The OpenAI API provides a multi-agent beta for building Ultra-like experiences. Whether Ultra appears directly depends on the current client and account.

Do not ask the prompt to "use Pro" or "think harder." Choose the runtime mode in product settings or API parameters. Keep the prompt focused on the goal, context, constraints, evidence, and output format.

<h2 id="lean-prompts">Test Leaner Prompts With a Baseline</h2>

In a sample of internal coding-agent evaluations, OpenAI removed repeated instructions and examples and shortened tool descriptions. The leaner configurations produced:

- evaluation scores roughly 10% to 15% higher
- 41% to 66% fewer total tokens
- 33% to 67% lower cost

These ranges are directional results from an internal sample. They are not guaranteed for every application.

Use this process:

1. Start with a prompt and tool set that already works.
2. Remove one group of instructions, examples, or tools.
3. Run the same representative tasks.
4. Compare success, completeness, evidence, tokens, latency, and cost.
5. Keep rules that encode a product requirement or fix a measured gap.

Do not delete hundreds of lines at once and call the lower token count a success. See [How to Write Project Rules for Strong Models](/docs/agent-memory/strong-model-project-rules) for the full audit process.

<h2 id="autonomy">Use One Compact Autonomy Policy</h2>

Sol is proactive in multi-step work. Define authorization by action risk:

- Answers, explanations, reviews, diagnosis, and planning read material and report findings.
- Change, build, and fix requests authorize local edits and non-destructive verification inside the stated scope.
- External writes, destructive actions, purchases, and clear scope expansion require user confirmation.

State this policy once. Repeating "ask me first" and "do not edit" can make the model pause before normal reads, log inspection, and tests.

<h2 id="tools">When to Use Programmatic Tool Calling</h2>

Programmatic Tool Calling lets GPT-5.6 write JavaScript in a hosted runtime, call eligible tools, and reduce intermediate output.

Good fits:

- filtering, joining, ranking, and deduplication
- aggregating many results with the same shape
- batch validation with a defined input and output schema

Poor fits:

- one direct tool call is enough
- each result changes the next decision
- an action needs human approval
- the final answer must preserve native files or citations

When both direct and programmatic calls are available, define one handoff. State the eligible tools, output schema, concurrency and retry limits, stopping condition, and the decisions that must return to direct tool calls.

<h2 id="context">Long Context Still Needs Cleanup</h2>

GPT-5.6 supports persisted reasoning and explicit prompt caching. Reuse earlier reasoning only while the goal, assumptions, and priorities remain stable.

When the direction changes, earlier reasoning is stale. Keeping it can carry old conclusions into the next turn. For clearing, handoffs, and new sessions, continue with [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management).

<h2 id="checklist">Completion Check</h2>

```text
The requested outcome exists.
Every completion claim has supporting tool evidence.
Failed tests and skipped steps are reported accurately.
The prompt does not repeat instructions.
The task does not expose unrelated tools.
The quality gain from higher effort justifies its tokens, latency, and cost.
```

<h2 id="next">Next Step</h2>

- Connect Codex: [Models & Runtimes / Codex](/docs/runtime/codex)
- Manage long sessions: [Agent Infrastructure / What to Do When Sessions Get Too Long](/docs/agent-memory/context-management)
- Audit project rules: [Agent Infrastructure / How to Write Project Rules for Strong Models](/docs/agent-memory/strong-model-project-rules)

<h2 id="reference">References</h2>

- OpenAI / GPT-5.6 model guidance: <https://developers.openai.com/api/docs/guides/latest-model>
- OpenAI / GPT-5.6 Sol model page: <https://developers.openai.com/api/docs/models/gpt-5.6-sol>
- OpenAI / GPT-5.6 launch: <https://openai.com/index/gpt-5-6/>
