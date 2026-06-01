---
title: What AI Actually Is
slug: what-is-ai
order: 1
summary: A single metaphor explains it all: AI is not magic, not a database, not a search engine. It's an intern who has read every book in the world but has a terrible memory. Understand this, and you understand the foundation of every AI tool.
section: concepts
section_title: Core Concepts
section_order: 5
---

# What AI Actually Is

You've probably heard a dozen names: GPT, Claude, DeepSeek, Qwen, Gemini. You've probably seen even more labels: large language models, generative AI, AGI, agents, neural networks.

The names don't matter. What matters is what this thing actually is, at its core.

<h2 id="scene">A Scene</h2>

You try AI for the first time. You open a webpage, type a sentence.

It responds with something coherent, natural, maybe even witty.

You think: does this thing actually have a brain?

Later, you ask it about something you know well. It answers with total confidence — but you can spot immediately that it's making things up.

You think: is this thing lying to me?

These two moments happen to everyone the first time they use AI.

Understand why they coexist, and you understand what AI actually is.

<h2 id="what-it-is">It's a "next-word predictor"</h2>

Strip away all the technical terms.

What AI does is remarkably simple: **given a sequence of text, it predicts the most likely next word.**

If you type "The weather today is", it predicts "sunny" or "rainy" or "cold" — depending on what came before.

That's it.

So why does it sometimes seem intelligent?

Because when it makes those predictions, it's not just looking at the last few words. It's cross-referencing everything it has ever read — every book, article, conversation, code file, and webpage it was trained on. It has learned the patterns of how humans organize language.

So when you ask "how do I negotiate a raise," the answer it gives isn't based on personal experience. It's because it has read countless articles on that topic and learned what humans typically say in that situation.

```text
AI's core capability = pattern matching + text continuation
It's not thinking. It's continuing text in patterns it has seen before.
```

<h2 id="metaphor">Think of It as a New Employee</h2>

This is the most important sentence in this chapter:

```text
AI is like an intern who has read every book in the world.
```

This single metaphor explains every puzzle you'll encounter.

**Incredibly well-read**: They've read every introductory textbook, every industry document. Ask about any field and they can engage.

**No common sense**: They don't know why your company stopped ordering from that supplier. They don't know your manager is in a bad mood this week. They don't know the last proposal was already rejected. None of that was in the books.

**Terrible memory**: Every time you talk to them, you need to re-tell them what you said last time. They don't "remember" your conversation — they re-read the transcript you provide at the start of each exchange.

**Never admits when they don't know**: Ask anything and they'll give you an answer. Some answers are things they truly know. Some are extrapolations from vaguely similar material. Some are two unrelated things stitched together — and they can't tell the difference.

```text
Three fundamental facts about AI:
1. It has read a lot, but knows nothing about your specific situation
2. It has no real memory — every conversation starts fresh
3. It never says "I don't know" — it continues text, it doesn't verify facts
```

<h2 id="token">What's a "Token" — Why Word Counts Don't Match</h2>

You might notice that AI billing shows different "word counts" than what you see.

That's because AI doesn't process text by the word. It processes `tokens`.

A token is roughly a small chunk of text. In English, about 4 characters or 0.75 words per token. In Chinese, roughly 1-2 tokens per character.

But these are rough estimates. Code, punctuation, spaces, JSON, Markdown tables — they all make token counts unintuitive.

You don't need to memorize conversion rates. You just need to know:

```text
The words you see ≠ the words AI processed
```

AI often produces a short reply after reading a mountain of background material, conversation history, and tool outputs. Those all count.

For a deeper explanation, see [How AI Cost Works](/docs/platform/ai-cost-basics).

<h2 id="memory">It Has No Real Memory</h2>

This is the most counterintuitive thing about AI.

You've been talking for half an hour and it remembers what you said at the start. You think it has "learned" about you.

But it hasn't remembered *you*. What actually happened: before each reply, **the system re-feeds your entire conversation history back to the model.**

Like working with an intern who has a terrible memory. Every time you say "let's continue," their assistant spreads out all their meeting notes in front of them. They scan everything, then respond.

They haven't "remembered" you. They've re-read the transcript.

This explains three phenomena:

```text
1. Longer conversations get slower (more and more text to re-read each time)
2. Longer conversations cost more (more input tokens consumed)
3. AI may start repeating itself late in long chats (too much context, losing focus)
```

It also explains why starting a fresh conversation is sometimes the better move.

For managing context properly, read [How to Manage AI's Memory](/docs/concepts/what-is-context).

<h2 id="hallucination">Why It Sometimes Makes Things Up</h2>

People call AI's fabrications "hallucinations."

But that term is misleading — it makes it sound like a bug, like the AI "glitched."

The truth: fabrication is not a bug. It's an inherent capability.

Remember, AI's essence is "continue the text." It was trained to be an extremely good continuation predictor. When you ask "how tall is Mount Everest," its training data contains plenty of "Mount Everest is 8,848.86 meters" — it just repeats that.

But when you ask "what did I eat for lunch yesterday," that information isn't in its training data. What does it do? It still continues — because that's what it does. It might fabricate "you probably had noodles or rice," because that's a plausible continuation of "what did someone eat for lunch."

```text
AI doesn't say "I don't know."
It just continues — sometimes with facts, sometimes with fabrications.
It can't tell the difference.
```

This is why you need to verify: in domains you know well, review its output critically. In domains you don't know, cross-check with other sources.

Read [When to Trust AI and When Not To](/docs/concepts/calibration) for a full treatment.

<h2 id="reasoning">Reasoning Models vs Standard Models</h2>

You may have noticed that some AI models show "thinking..." before responding, while others don't.

These are two different ways of working.

| Type | Plain-English explanation | When to use |
| --- | --- | --- |
| Standard model | Think while speaking — you ask, it answers directly | Daily conversation, translation, summarization, simple writing |
| Reasoning model | Think first, then speak — internally explores possibilities, picks the best answer | Math, logic, coding, complex analysis |

Reasoning models aren't "smarter." They're "slower but more careful."

Like with employees: some are quick, answering as you speak — great for everyday communication. Others need to work things out on paper before responding — better for tasks that need careful thinking.

```text
Not slower is better, not faster is better.
The right thinking style depends on the task.
```

<h2 id="not">What AI Is Not</h2>

Three "nots" to prevent the most common false expectations.

```text
AI is not a database.
— You can ask "what are common stainless steel grades" and it will tell you. But you can't expect it to remember "which batch of material your factory used on March 15th." It doesn't have that record.

AI is not a search engine.
— It can synthesize public knowledge from its training. But if you ask "today's copper price," it only knows up to its training cutoff date. It won't actively search the web — unless the tool you're using has search configured.

AI is not a person.
— It has no intentions, no emotions, it doesn't actually "like" you or get "angry." It's continuing text according to instructions. When it says "I understand," it doesn't truly understand — it's just continuing text with a word humans use in that context.
```

<h2 id="why-care">Why Understanding This Matters</h2>

You might think: I work in a factory, I work in an office filling spreadsheets — I don't need to understand AI's internals.

And you're right. You don't need to understand the engine to drive a car. You don't need to understand neural networks to use AI.

What you need is to understand AI's **behavioral patterns**:

```text
When can it help you?
When might it fail you?
Why does the same AI sometimes work well and sometimes not?
```

The answers to all three are buried in this chapter's core insight:

```text
AI is fundamentally a "next-word predictor."
It doesn't think, doesn't remember, doesn't verify — it just continues text.
But because it has read an enormous amount, its continuation behavior
appears intelligent in many situations.
```

Understand this one sentence, and you won't be scared by headlines about "AI replacing humans." Nor will you give up entirely after one bad hallucination.

<h2 id="remember">Remember One Thing</h2>

```text
AI is not mysterious.
It's an intern who has read every book in the world —
knowledgeable, forgetful, and never admits when they don't know.
How you treat it is not awe. It's management.
```

<h2 id="next">Next Step</h2>

Now you know what AI is. But you probably have one more question:

"I tried AI back in 2023. It felt underwhelming. Why is everyone saying AI can actually do things now?"

The answer is in the next chapter: [Why AI Is Different Now](/docs/concepts/why-now)

If you want to understand costs first: [Platform / How AI Cost Works](/docs/platform/ai-cost-basics)

If you already know what AI is and want to start using it: [Getting Started / First Time Using SorryCode](/docs/start/first-step)
