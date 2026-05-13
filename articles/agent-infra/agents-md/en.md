---
title: AGENTS.md
slug: agents-md
order: 3
summary: Project instructions read by Codex. Keep durable rules here, not chat history, one-off tasks, or abandoned conclusions.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# AGENTS.md

`AGENTS.md` is the project instruction file read by Codex.

It is not a longer prompt. It is not a trash can for chat history.

Use it for stable rules Codex needs every time it works in the project: structure, commands, code style, working boundaries, and final checks.

If you are dealing with long sessions, caching, and handoffs, start with [How to Manage Long-Lived Context](/docs/agent-infra/context-management). This page only explains how to maintain `AGENTS.md`.

<h2 id="who-reads-it">Who Reads It</h2>

Codex reads the applicable `AGENTS.md` files.

Common locations:

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

The closer a file is to the current working directory, the more specific it is. A nested `AGENTS.md` is useful when a subproject has its own rules, such as frontend, backend, scripts, or docs.

The official Codex docs also mention fallback names and override behavior. Beginners do not need to start there. Maintain one good root file first.

<h2 id="where">Where to Put It</h2>

Start at the project root:

```text
your-project/
  AGENTS.md
  README.md
  package.json
```

If a subdirectory has clearly different rules, add another one there:

```text
your-project/
  AGENTS.md
  frontend/
    AGENTS.md
```

Do not create many files on day one. The more files you add, the easier it is for rules to conflict.

<h2 id="what-to-write">What to Write</h2>

Good content:

- what the project does
- directory structure
- install, test, and build commands
- code style and naming rules
- files or directories the agent should not change
- checks to run before finishing
- OS, encoding, or path notes
- recurring project pitfalls

Be concrete. Do not write “make the code elegant.” Write “after changing the API schema, regenerate types and run pnpm test:types.”

<h2 id="when-update">When to Update It</h2>

`AGENTS.md` is not write-once.

Update it when:

- the project structure changes
- test, build, or release commands change
- the team adopts a new code rule
- the same pitfall appears repeatedly
- a handoff contains a fact that should last

Do not paste the whole handoff into `AGENTS.md`. Keep only durable rules.

<h2 id="handoff">What to Extract From a Handoff</h2>

A handoff usually contains a lot of temporary state. Only move the reusable parts.

Good candidates for `AGENTS.md`:

```text
where the source of truth lives
which commands are commonly used
which directories should not be touched
which old direction has been abandoned
which checks must run before finishing
```

Bad candidates:

```text
today's exact progress
full error logs
ideas discussed but not chosen
a long self-summary written by an agent
```

<h2 id="avoid">What Not to Write</h2>

Do not write:

- API keys, passwords, or tokens
- one-off tasks
- temporary TODOs
- long error logs
- stale paths or commands
- unverifiable style wishes
- long background unrelated to the current tree

If a line will not make the next Codex task more stable, do not put it here.

<h2 id="template">Small Template</h2>

Start with this:

```md
# AGENTS.md

## Project

This project is ...

## Commands

- Install:
- Test:
- Build:

## Source of Truth

- ...

## Working Rules

- ...

## Do Not

- Do not ...
```

<h2 id="first-prompt">First Prompt</h2>

After the file exists, start like this:

```text
Read AGENTS.md first.

Do not edit files yet. Tell me:
- what this project is
- the common commands
- which files or directories should not be changed casually
- which checks should run before finishing
```

Correct misunderstandings before asking the agent to work.

<h2 id="claude">Relationship With CLAUDE.md</h2>

If you use both Codex and Claude Code, maintain both `AGENTS.md` and [CLAUDE.md](/docs/agent-infra/claude-md).

Keep facts consistent. Do not let the two files contradict each other.

Claude Code can also reference an existing `AGENTS.md` from its memory file; follow the official Claude Code docs for exact syntax. For beginners, consistency matters more than advanced configuration.

<h2 id="reference">Reference</h2>

- OpenAI Codex / AGENTS.md: <https://developers.openai.com/codex/guides/agents-md>
