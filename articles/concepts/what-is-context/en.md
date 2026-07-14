---
title: "How to Manage AI's Memory"
slug: what-is-context
order: 5
summary: After a long chat, AI starts talking nonsense? It didn't get dumber — the context got dirty. Think of AI's context as your desk: stable rules pinned to the wall, current task on the desk, junk in the trash. Managing context matters more than writing perfect prompts.
section: concepts
section_title: Core Concepts
section_order: 5
---

# How to Manage AI's Memory

You may have had this experience:

You've been talking to AI for an hour. It started strong, but the longer you go, the worse it gets. It starts repeating itself. It references solutions you already rejected. It fixates on some irrelevant detail.

You think: did it get dumber?

It didn't get dumber. Its desk got messy.

<h2 id="desk">Think of It as a Desk</h2>

Every time AI responds to you, the system spreads a pile of material in front of it:

```text
- System instructions (what role it plays, how to work)
- Your conversation history (from the first message to now)
- The files you provided
- Results from the tools it called
- Project rule files (if configured)
```

This entire pile is called "context."

AI looks at everything on this desk, then decides what to say next.

```text
Context = everything AI can see before it responds to you.
```

<h2 id="limited">The Desk Has a Size Limit</h2>

This desk isn't infinite.

Every AI model has a "context window" — the maximum amount it can see at once. In 2025, mainstream models have context windows around 200K tokens, roughly the length of a short novel.

Sounds huge? It fills up fast.

A project with dozens of code files, a two-hour conversation history, several rounds of tool output — these add up quickly and can max out the window.

When context nears the limit, the system must "truncate" — throw out the earliest messages, keeping only the most recent.

Like a desk where new papers keep piling up. Old ones get pushed off. Eventually, AI "forgets" the important things you said at the start.

<h2 id="dirty">Worse: Context Gets Dirty</h2>

A full context window isn't even the biggest problem.

The biggest problem is: **context gets dirty.**

Dirty context looks like this:

```text
- You had AI try three approaches. Two failed. Their records are still in the conversation.
- It referenced data you later dismissed.
- The chat is stuffed with error logs, failed attempts, expired judgments.
- You said "no no, start over," but it still remembers your contradictory earlier instructions.
```

When AI sees this mess, it doesn't actively judge "this is obsolete, this is contradictory." It tries to take everything into account — and gets more confused as a result.

```text
Clean context: AI sees information that is accurate, consistent, and relevant.
Dirty context: AI sees information mixed with outdated, contradictory, irrelevant content.
```

This is why starting a fresh conversation sometimes makes AI perform better — the new desk is clean.

<h2 id="where-to-put">Three-Layer Management: Wall, Desk, Trash</h2>

Managing context isn't complicated. Divide information into three layers:

**Wall (long-term rules)**

Pinned to the wall in front of the desk, always visible. AI sees this every time it works.

Good for: what this project is, common commands, code style, brand guidelines, files not to touch.

How to implement: use config files like `AGENTS.md` or `CLAUDE.md`.

This chapter won't expand on how to write config files. The [Agent Advanced](/docs/agent-memory/overview) section covers it in full.

**Desk (current task)**

On the desk surface. Things directly relevant to the current task.

Good for: this session's goal, the approach under discussion, just-received data, your recent feedback.

This accumulates naturally in conversation. The key: **if it's not relevant to the current task, get it off the desk.**

**Trash (discard)**

Abandoned approaches, failed attempts, expired judgments, contradictory old instructions — clear these out so AI doesn't see them.

How to clear? Simple: start a new conversation.

Or, more professionally: ask AI to write a handoff — a condensed note of what's worth keeping — then feed the handoff into a fresh conversation.

<h2 id="when-reset">When to Start a New Conversation</h2>

When these signals appear, don't keep pushing:

```text
- Direction changed: you started with data analysis, now you're making slides
- AI is referencing old solutions you already rejected
- The conversation is stuffed with error logs and failed attempts
- You can't even tell anymore which instruction it should follow
- Its responses are repeating, digressing, or fixating on a detail
```

These signals mean the context is dirty. Continuing to correct it in this conversation is worse than starting fresh.

<h2 id="save-vs-throw">What to Keep, What to Discard</h2>

A table to make it clear:

| Keep (write to file or handoff) | Discard (reset with new conversation) |
| --- | --- |
| Project purpose, directory structure | One-off task records |
| Common commands and checklists | Temporary TODOs |
| Code style and naming conventions | Long error logs |
| Durable business rules | Old approaches that were rejected |
| Confirmed design specs | Expired paths and commands |
| Files you must not touch | Self-contradictory summaries AI wrote then abandoned |

One-sentence judgment:

```text
If it'll be useful next time you work → write to a file.
If it only matters for this task → keep in conversation.
If it's outdated or wrong → clear it.
```

<h2 id="cost">Context Also Affects Cost</h2>

Remember what [How AI Cost Works](/docs/start/ai-cost-basics) covered?

AI consumption breaks down into three categories: input (what it reads), output (what it generates), cache (what it reuses).

Context directly determines input volume. Every time AI responds, it re-reads your entire conversation history. The longer the conversation, the higher the cost per reply.

```text
Dirty context doesn't just degrade AI performance.
It makes you pay more.
```

Managing context well is the same thing as saving money and improving output.

<h2 id="remember">Remember One Thing</h2>

```text
AI's performance doesn't depend on how powerful it is.
It depends on how clean the information it "sees" right now is.
Good context isn't about having more. It's about having the right things.
```

<h2 id="next">Next Step</h2>

You've learned how to manage AI's memory. But there's an even bigger question:

**How do you know if AI is telling the truth or making things up?**

Next chapter: [When to Trust AI and When Not To](/docs/concepts/calibration)

For a deep dive on long-term context management: [Agent Advanced / How to Manage Long-Lived Context](/docs/agent-memory/context-management)

For understanding how context affects cost: [Getting Started / How AI Cost Works](/docs/start/ai-cost-basics)
