---
title: CLAUDE.md
slug: claude-md
order: 4
summary: Memory and instructions read by Claude Code. Keep durable project facts here, not temporary session state.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# CLAUDE.md

`CLAUDE.md` is the memory and instruction file read by Claude Code.

Its job is simple: when Claude Code enters a project, it should not need to relearn who you are, what the project is, how to test it, and which mistakes to avoid.

But it is easy to misuse.

`CLAUDE.md` is not a temporary task list. It is not a trash can for old sessions. It should hold durable project facts and stable collaboration rules.

If you are dealing with long sessions, caching, and handoffs, start with [How to Manage Long-Lived Context](/docs/agent-infra/context-management). This page only explains how to maintain `CLAUDE.md`.

<h2 id="who-reads-it">Who Reads It</h2>

Claude Code reads applicable memory.

Common locations:

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
your-project/apps/web/CLAUDE.md
```

Use the official Claude Code docs as the source of truth for exact loading behavior. For most beginners, the stable recommendation is to maintain one `CLAUDE.md` at the project root.

<h2 id="where">Where to Put It</h2>

Project rules should live in the project:

```text
your-project/
  CLAUDE.md
  README.md
```

Use user-level memory for personal long-lived preferences. Do not keep project facts only in personal memory, or they will disappear when the project moves to another person, machine, or runtime.

<h2 id="what-to-write">What to Write</h2>

Good content:

- what the project is
- common development, test, and build commands
- code style and directory conventions
- common pitfalls and things to avoid
- important business rules
- collaboration preferences
- checks to run before finishing

Make it executable. Do not write “be careful.” Write “after changing the payment flow, check the regression tests under tests/payments.”

<h2 id="when-update">When to Update It</h2>

Update `CLAUDE.md` when:

- the project structure changes
- common commands change
- Claude Code repeatedly misunderstands the same project fact
- a handoff contains a rule that should last
- collaboration rules change

Do not update durable memory for a one-off task. If the information will not matter after this task, keep it in the session or handoff.

<h2 id="handoff">What to Extract From a Handoff</h2>

A handoff is transfer state. `CLAUDE.md` is durable memory.

Good candidates for `CLAUDE.md`:

```text
where source-of-truth files live
which old direction has been abandoned
which command is currently valid
which directories need care
which checks must run before finishing
```

Bad candidates:

```text
the full session story
raw error logs
temporary guesses
short-lived TODOs
details of abandoned plans
```

<h2 id="avoid">What Not to Write</h2>

Do not write:

- API keys, tokens, or passwords
- one-off tasks or temporary TODOs
- stale commands
- long meeting notes
- long error logs
- information unrelated to agent work

If a line will make a future Claude Code session carry wrong old context, do not write it.

<h2 id="template">Small Template</h2>

```md
# CLAUDE.md

## Project Context

This project is ...

## Common Commands

- Test:
- Build:

## Source of Truth

- ...

## Working Rules

- ...

## Avoid

- ...
```

<h2 id="first-prompt">First Prompt</h2>

Start like this:

```text
Read CLAUDE.md first.

Do not edit files yet. Tell me:
- what this project is
- the common commands
- which rules must be followed
- which old directions should no longer be used
```

Correct misunderstandings before continuing.

<h2 id="agents">Relationship With AGENTS.md</h2>

If you use both Codex and Claude Code, maintain both [AGENTS.md](/docs/agent-infra/agents-md) and `CLAUDE.md`.

Keep facts consistent. Wording can differ by runtime.

The official Claude Code docs support importing other files into memory. That means `CLAUDE.md` can reference an existing `AGENTS.md` to reduce duplication. Follow the Claude Code docs for exact syntax.

<h2 id="reference">Reference</h2>

- Claude Code / Memory: <https://docs.anthropic.com/en/docs/claude-code/memory>
