---
title: "Where to Start"
slug: where-to-start
order: 8
summary: All the concepts are covered. Now three paths: just curious — try web chat AI first. Have a specific task — install an Agent and complete one deliverable. Ready to go deep — create your project rules file. Completing one small task beats reading ten tutorials.
section: concepts
section_title: Core Concepts
section_order: 5
---

# Where to Start

You've read the previous seven chapters. By now you know:

- AI is an intern who has read every book in the world but has a terrible memory
- Three breakthroughs turned it from a "chat toy" into a "production tool"
- Agent isn't a smarter chatbot — it's an "employee" that operates your computer
- A prompt isn't a magic spell — it's a work order covering four things
- Managing context matters more than perfect prompts — wall, desk, trash
- AI's confidence doesn't equal correctness — review in domains you know, cross-check in domains you don't
- Model is brain, workbench is body, platform is infrastructure — pick the workbench first

Now the last question: **what do I actually do first?**

<h2 id="three-paths">Three Paths</h2>

Different people take different paths. First, identify yourself:

```text
A. I just want to get a feel for it. Not sure about installing anything.
B. I have a specific task I want done. I'm tired of doing it manually.
C. I want to make AI a systematic part of my daily workflow.
```

<h2 id="path-a">Path A: Just Curious</h2>

**You don't need to install anything.**

Open any AI chat webpage — ChatGPT, Claude, whichever. Apply what you learned in [Talking to AI Is Not Spellcasting](/docs/concepts/what-is-prompt):

1. Think of a small task from your work (write an email, summarize text, translate a document)
2. Be clear: what you want, what you don't want, what "done" looks like, what background context matters
3. Send it. Look at the result.
4. Tweak one part of your instruction. Send again. Notice the difference.

After these four steps, you already know how to use AI better than 90% of people.

```text
Path A goal: experience one "clear instruction → correct result" moment.
Time: 10 minutes.
Nothing to install.
```

<h2 id="path-b">Path B: Have a Task, Want It Done</h2>

You have a specific task you want AI to help with. Organizing reports. Writing documents. Making slides. Analyzing data.

**You need the full pipeline: install workbench → install skill → complete one task.**

**Step 1: Pick a workbench**

```text
Using GPT models → install Codex
Using Claude models → install Claude Code
Not sure → install Codex, currently the simplest beginner entry
```

Specific installation steps are in [Runtime / Codex](/docs/runtime/codex) or [Runtime / Claude Code](/docs/runtime/claude-code). Installation is usually one command, done in minutes.

**Step 2: Install a Skill**

A Skill is a capability pack for your Agent. Install the one matching your task:

| What you want to do | Which Skill to install |
| --- | --- |
| Process Word / Excel / PPT / PDF | [Office Docs](/docs/skills/office-docs) |
| Generate images, posters, covers | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| Create one-pagers, resumes, portfolios | [Kami](/docs/skills/kami) |
| Make web-based slide decks | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |

**Step 3: Complete one task**

Don't start with something complex. Pick something small and take it end to end.

Example: "Take this Excel report, aggregate the data by month, generate three trend charts, and output a PDF."

Copy this sentence to your Agent. It will read the file, propose a plan, wait for your confirmation, then execute.

```text
Path B goal: install a workbench, complete your first task.
Time: 30-60 minutes (installation + first task).
Critical: skipping the plan review = wasting time and money.
```

<h2 id="path-c">Path C: Make It Systematic</h2>

You've already completed several tasks. You want to make AI a daily tool.

**You need to establish project rules.**

Create a folder for your work. Inside it, create an `AGENTS.md` (if using Codex) or `CLAUDE.md` (if using Claude Code).

In this file, write:

```text
- What this project is
- Directory structure
- Common commands and tools
- Code/writing style rules
- Which files not to touch
- What to check before completing a task
```

Then, before every session, ask your Agent to read this file first.

For more management techniques, see [Agent Advanced](/docs/agent-infra/overview).

```text
Path C goal: create your first project rules file.
Time: 20 minutes for version 1. Update gradually over time.
Critical: only write durable rules. Don't write temporary tasks into the file.
```

<h2 id="dont">Three Things Not to Do</h2>

Whatever path you choose, remember three "don'ts":

```text
1. Don't chase model names.
   Chase tasks. Completing one thing matters more than knowing ten model names.

2. Don't try too many tools at once.
   Pick one workbench. Install it. Complete one task. Then consider switching.

3. Don't try to learn everything at once.
   You don't need to master all seven chapters today.
   Learn as you go. Route first, then load.
```

<h2 id="recap">What This Book Covered</h2>

Seven chapters. One theme:

```text
How to train "an intern who has read every book in the world
but has a terrible memory" into an "employee" who can do work for you.
```

The path was:

```text
Understand it (Chapters 1-3)
→ Command it (Chapters 4-6)
→ Choose it (Chapter 7)
→ Start using it (You are here)
```

<h2 id="remember">Remember One Thing</h2>

```text
Complete one small task.
It beats reading ten tutorials.
```

<h2 id="next">Next Step</h2>

Pick your path:

Path A: Open any AI chat webpage. Apply the "four elements" you learned. Try once.

Path B: Go to [Getting Started / First Time Using SorryCode](/docs/start/first-step). Create an API key. Install a workbench.

Path C: Go to [Agent Advanced](/docs/agent-infra/overview). Learn how to establish project rules.

If you're still unsure whether SorryCode is right for you: [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for)
