---
title: How AI Cost Works
slug: ai-cost-basics
order: 2
summary: Do not judge cost by visible reply length. Understand input, output, cache, and group multipliers before comparing model cost.
section: platform
section_title: Platform
section_order: 8
---

# How AI Cost Works

Many first-time users have the same question:

```text
The AI barely wrote anything. Why did it use so much?
```

AI cost is not based on the number of words you can see.

Model usage usually maps back to three categories:

```text
input: what the model read
output: what the model generated
cache: what the model reused, or wrote for later reuse
```

Your final payment experience may be balance, subscription, quota, or invoice, but the underlying model resource usually maps back to these three.

## Tokens Are Not Words

Models do not process text by directly counting words or characters.

They process `tokens`.

You can think of a token as a small internal text piece. A common rough estimate in English is that one token is about 4 characters, or about 0.75 words.

But that is only a rule of thumb.

Chinese, code, punctuation, spaces, paths, JSON, and Markdown tables can all make token counts unintuitive.

So do not judge cost by looking at the final answer and saying:

```text
It only replied with 200 words. Why was it expensive?
```

You are seeing output. The model may have read much more input.

## 1. Input: What the Model Read

Input is what the model reads.

It is not only your latest message.

It can also include:

- system prompts
- conversation history
- file contents
- tool results
- error logs
- project rules
- uploaded documents or image descriptions

If the AI replies with two sentences, that does not mean it only processed two sentences.

It may have read a large amount of context first.

## 2. Output: What the Model Generated

Output is what the model generates.

Replies, code, summaries, and rewritten text are output.

For many models, output tokens cost more than input tokens.

But output is not always identical to the final visible text.

Reasoning models may produce internal reasoning / thinking tokens. Those tokens may not fully appear in the final response, but they are usually billed on the output side.

So "it barely wrote anything" can be misleading.

It may not have written much for you to see, but it may have spent work internally.

## 3. Cache: What the Model Reused

Cache handles repeated context.

If stable content is reused across requests, the system may cache it.

When cache hits, cached input / cache read is usually cheaper than normal input.

But cheaper is not free.

Some model providers separate:

- cache read: reading already-cached content
- cache write: writing content into cache for the first time

The first cache write may also cost money.

So do not hear "cache hit" and assume "free".

Cache reduces repeated-input cost. It does not make model work free.

## How Web Chat Triggers Usage

You may think you only sent one sentence.

But a web product may also include:

- conversation history
- system rules
- files and images
- search results
- tool results

Those mostly become input.

The model reply becomes output.

Stable context may use cache if the product supports it.

## How API Calls Trigger Usage

API usage is the clearest mapping.

The `prompt / messages / tools / files` you send are input.

The model `response` is output.

Repeated prefixes, system prompts, and long context may hit cache.

If you write API requests yourself, understand these three categories first.

## How Agent Runtimes Trigger Usage

Agent runtimes such as `Codex` and `Claude Code` are where cost is easiest to misunderstand.

An agent is not a single question and a single answer.

It may read files, run commands, inspect errors, call tools, plan across multiple steps, and feed the results back into context.

Those actions keep creating input.

Each time the model analyzes, decides, summarizes, or rewrites, it creates output.

If the runtime organizes stable context well, it may hit cache.

If not, it may reread and rewrite more than you expect.

## Three Questions to Ask

Do not start with:

```text
How much did it write?
```

Start with:

```text
How much input did it read?
```

```text
How much output did it generate?
```

```text
Did it use cache?
```

After those three, you can judge whether the usage makes sense.

## How This Relates to SorryCode

SorryCode gives you one entry point and one balance.

You can connect Codex, Claude Code, Skills, image APIs, and other tools through it.

But no matter which entry you use, model consumption still comes back to input, output, and cache.

Understanding these three explains why "asking AI one question" can cost differently in web chat, API calls, and agent runtimes.

## What 0.8x, 1x, and 2x Mean in Groups

In the console, you may see labels such as `0.8x multiplier`, `1x multiplier`, or `2x multiplier`.

The `x` is a billing multiplier. It is not speed.

![A 0.8x multiplier label in a console group](./group-multiplier-08.png)

It does not mean:

- faster requests
- higher permission
- bigger is always better
- the best beginner choice

It means this group charges your balance by multiplying the official USD model price.

Use this first:

```text
USD balance charged = official model USD price × group multiplier
```

For example, if a model would normally cost `1 USD`:

```text
0.8x group charges about 0.8 USD balance
1x group charges about 1 USD balance
2x group charges about 2 USD balance
```

## Why 0.8x Can Feel Close to 10 Percent

The current SorryCode recharge rule is roughly:

```text
1 RMB recharge ≈ 1 USD balance
```

If you compare official USD pricing as a RMB user, you usually also think through the USD to RMB exchange rate. For rough mental math, use `1 USD ≈ 6.8 RMB`.

So the RMB cost ratio is roughly:

```text
RMB cost ratio ≈ group multiplier / 6.8
```

Examples:

| Group multiplier | Rough math | Close to official RMB cost |
| --- | --- | --- |
| `0.8x` | `0.8 / 6.8 ≈ 0.12` | a little over 10 percent |
| `1x` | `1 / 6.8 ≈ 0.15` | about 15 percent |
| `2x` | `2 / 6.8 ≈ 0.29` | about 30 percent |

This is only a rough way to understand the price feel. It is not an exchange-rate promise. Actual model prices, group multipliers, and model availability follow what the console shows.

Remember this:

```text
The multiplier is a price multiplier, not a speed multiplier.
```

## Next

- Unsure whether SorryCode fits you: [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for)
- Unsure how tools and models differ: [Platform / Tools Are Not Models](/docs/platform/tools-and-models)
- Ready to start: [Platform / Create API Key](/docs/platform/create-api-key)
- GPT path: [Runtime / Codex](/docs/runtime/codex)
- Claude path: [Runtime / Claude Code](/docs/runtime/claude-code)
