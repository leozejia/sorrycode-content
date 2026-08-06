---
title: Why AI Is Different Now
slug: why-now
order: 2
summary: You tried AI a few years ago and found it underwhelming. Context, tool use, and reasoning have since combined to move AI from answering questions toward participating in real work.
section: concepts
section_title: Core Concepts
section_order: 5
---

# Why AI Is Different Now

You probably have a question, and it's a fair one:

```text
I tried AI back in 2023.
It was interesting for a few minutes, but not that useful.
Why are so many people saying AI can actually do things now?
```

You're not alone. Most people's first AI experience was the 2023 ChatGPT web version. That version really did feel more like a fun chat toy — it could write poems, tell stories, answer simple questions, but you wouldn't seriously expect it to get work done.

A few years later, what changed?

<h2 id="not-just-better">It's Not Just "Got Smarter"</h2>

The easiest mistake is to think of AI progress as "the models keep getting smarter."

```text
The issue isn't that AI's IQ went up.
The issue is that AI gained three new capabilities between the early chat models and today's systems:
1. It can read more at once — enough to read an entire book
2. It has hands now — not just generating text, but operating software
3. It can think before speaking — from one-shot Q&A to multi-step reasoning
```

Taken individually, each one looks like an incremental improvement.

Taken together, they're a qualitative leap.

<h2 id="analogy">Think of It as a Factory</h2>

2023 AI was like a single-purpose machine tool.

You feed it a piece of material, it performs one operation, then stops and waits. You feed it the next piece. Each cycle starts from scratch.

Today's AI is more like an assembly line.

You put raw material in at one end. It moves through every station on its own — reading files, analyzing data, calling tools, producing output, checking quality. You don't need to supervise every step. You only need to inspect the final result.

```text
Single machine → Assembly line
That's the core difference between early chat AI and today's Agents.
```

This change didn't come from any single model getting smarter. It came from three foundational capabilities stacking together.

<h2 id="context">Breakthrough 1: Context Window — from One Page to One Book</h2>

The context window is, simply put, how much content AI can "see" at once.

Early, commonly used GPT-4 versions had an 8K token context window. A complete system prompt + your question + the AI's response might fill it up. Anything beyond that got cut off.

What's 8K tokens? Roughly 6,000 English words, or the length of a short article.

```text
2023: AI could read one page at a time.
Want it to understand your entire project? Not possible.
Want it to remember a full conversation history? Won't fit.
```

Today, context limits vary from tens of thousands to hundreds of thousands of tokens, with some models offering more.

A large context window can hold an entire novel or a substantial bundle of project material. But fitting it in does not mean AI will understand every detail.

```text
Today: AI can see much more material at once.
You can give it a book or a bundle of project files and ask it to work from them.
With enough material, it can still miss details or lose track of earlier information.
```

But this capability comes with a cost.

The more AI reads, the slower it processes and the more it consumes. And dumping everything on AI isn't always the best strategy — just like you wouldn't stack every company file on one employee's desk.

That's why later we have [How to Manage AI's Memory](/docs/concepts/what-is-context).

<h2 id="tools">Breakthrough 2: Tool Use — AI Grew Hands</h2>

Early mainstream chat products mostly did one thing: you entered text and they returned text.

It couldn't read your files. It couldn't run programs. It couldn't query databases. It couldn't open a browser. It was a brain in a jar.

Today's Agents have "tool use" capabilities.

It can now:

```text
Read files, write files, execute commands, call APIs,
query databases, operate browsers.
```

What does this mean in practice?

Before: you asked AI "help me analyze this Excel report." You had to copy-paste the Excel contents yourself, AI would analyze, then you'd act on the results.

Now: you say "help me analyze this Excel." The Agent opens the file on its own, reads the data, performs analysis, generates charts, saves results. You take a final look.

```text
AI grew hands.
This is the essential difference between Agent and chat AI.
```

Tool use isn't proprietary to any single model. OpenAI, Anthropic, Google, and China's DeepSeek and Qwen — they're all teaching their models to use tools. The industry consensus is clear:

```text
AI that can only talk is a toy.
AI that can use tools is a tool.
```

The next chapter [Agent: From Chat to Work](/docs/concepts/what-is-agent) explores this in depth.

<h2 id="reasoning">Breakthrough 3: Reasoning — from Think-While-Speaking to Think-Then-Speak</h2>

Have you ever experienced this: you ask AI a complex math problem, and it gets it wrong?

It's not that it can't solve it. It's that it "thinks while speaking" — it writes the answer while reasoning. Halfway through it realizes the earlier step was wrong, but it's already committed.

Like someone asked to answer a complex question impromptu — they start speaking before their thoughts are fully formed.

In recent years, reasoning models gave AI another way to work: **think first, then speak.**

These are called "reasoning models." They internally explore multiple approaches and answers, then output the best one.

| | Standard model | Reasoning model |
| --- | --- | --- |
| How it works | Think while speaking | Think first, then speak |
| Speed | Fast | Slow |
| Best for | Daily chat, translation, summarization, writing | Math, logic, coding, complex analysis, multi-step decisions |
| What you see | Usually a direct answer | Some products show "thinking..." before the answer |

```text
Reasoning models aren't "smarter."
They work differently — they spend extra time thinking internally.
```

This distinction matters because not every task needs a reasoning model.

Translating text, writing a social post, summarizing an article — use a standard model. It's faster and cheaper.

For financial analysis, debugging, or multi-step logical deduction, a reasoning model is usually a better fit, but its result still needs verification.

Later, [When to Trust AI and When Not To](/docs/concepts/calibration) covers how to decide which to use.

<h2 id="multiplicative">Three Capabilities: Multiplication, Not Addition</h2>

The most important thing is to understand how these three breakthroughs relate.

They're not three separate things. They work together:

```text
Large context × Tool use × Reasoning = Agent
```

An example.

You ask 2023 AI to analyze sales data:

- **Small context**: It can't read all your data
- **No tools**: You have to manually copy-paste data to it
- **No reasoning**: Its analysis may be superficial

You ask a current Agent to do the same:

- **Large context**: It can hold more months of sales reports in one pass
- **Has tools**: It runs statistical scripts, generates charts, creates report files
- **Can reason**: It can help spot anomalies, form hypotheses, and suggest next steps

```text
Three capabilities combined don't produce "three times better."
They produce a shift from "advisor" to "worker."
```

<h2 id="why-matters">Why This Matters to You</h2>

You don't need to study how context windows expanded. You don't need to understand the protocol details of tool calling. You don't need to read the internal mechanisms of reasoning models.

You only need to know one thing:

```text
Early chat AI mainly answered questions.
Today's Agents can participate in real work.
```

The difference between these two isn't "better." It's **usable versus not usable.**

If you tried AI earlier and thought "interesting, but not very useful," that reaction was understandable. Many products at the time struggled to complete real workflows reliably.

It is worth making that judgment again now.

Not because your earlier judgment was wrong. Because AI gained capabilities it didn't have before.

<h2 id="remember">Remember One Thing</h2>

```text
AI changed not because any single model got smarter.
Three capabilities — large context, tool use, reasoning —
stacked together to turn AI from a "chat toy" into a "production tool."
```

<h2 id="next">Next Step</h2>

Now you know why AI is different. But you probably have a follow-up question:

"What can an Agent actually do? How is using one different from chatting with AI?"

The answer is in the next chapter: [Agent: From Chat to Work](/docs/concepts/what-is-agent)

If you want to understand how these changes affect cost: [Getting Started / How AI Cost Works](/docs/start/ai-cost-basics)

If you want to start using an Agent right now: [Runtime / Codex](/docs/runtime/codex)
