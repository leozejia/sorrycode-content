---
title: Make AI Remember Project Rules
slug: remember-rules
order: 3
summary: Write an AGENTS.md or CLAUDE.md file to make AI remember which files not to change, what commands to use, and what rules to follow.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# Make AI Remember Project Rules

You have completed a few tasks. Now every new session starts with you re-explaining the project — where the files are, which commands to use, what not to touch. This is not the agent being stupid. It is you not writing the rules down.

The fix is simple: put a rules file in the project root. Codex reads `AGENTS.md`. Claude Code reads `CLAUDE.md`. **The writing rules and maintenance discipline are identical** — only the filename differs.

If you are dealing with long sessions, caching, and handoffs, start with [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management). This page only explains how to maintain the rules file itself.

<h2 id="where">Where to Put It</h2>

Project root:

```text
your-project/
  AGENTS.md    # for Codex
  # or
  CLAUDE.md    # for Claude Code
```

If you use both tools, maintain both files. The rule: **both files describe the same facts — never let them contradict each other.** Claude Code can also import an existing `AGENTS.md` from `CLAUDE.md` to reduce duplication; follow the official Claude Code docs for exact syntax. For beginners, keeping facts consistent matters more than advanced configuration.

<h2 id="what-to-write">What to Write</h2>

- what the project does
- directory structure
- install, test, and build commands
- code style and naming conventions
- files or directories the agent should not change
- checks to run before finishing
- recurring project pitfalls

Be concrete. Do not write "make the code elegant." Write "after changing the API schema, regenerate types and run pnpm test:types."

<h2 id="avoid">What Not to Write</h2>

- API keys, passwords, or tokens
- one-off tasks
- temporary TODOs
- long error logs
- stale paths or commands
- unverifiable abstract wishes

If a line will not make the next agent session more stable, do not put it here.

<h2 id="when-update">When to Update</h2>

The file is not write-once. Update it when:

- project structure or common commands change
- the agent repeatedly misunderstands the same project fact
- the team adopts a new rule
- a handoff contains a fact that should last

But do not paste the whole handoff into the rules file. Keep only durable rules, not temporary state.

<h2 id="handoff">What to Extract From a Handoff</h2>

A handoff is transfer state. The rules file is durable memory.

Good candidates:

```text
where source-of-truth files live
which commands are commonly used
which directories should not be touched
which old direction has been abandoned
which checks must run before finishing
```

Bad candidates:

```text
today's exact progress
raw error logs
ideas discussed but not chosen
a long self-summary written by an agent
```

<h2 id="template">Small Template</h2>

```md
# AGENTS.md  (or CLAUDE.md)

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
Read AGENTS.md (or CLAUDE.md) first.

Do not edit files yet. Tell me:
- what this project is
- the common commands
- which files or directories should not be changed casually
- which checks should run before finishing
```

Correct misunderstandings before asking the agent to work.

<h2 id="codex">For Codex Users</h2>

Codex reads `AGENTS.md`. Common locations:

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

The closer a file is to the current working directory, the more specific it is. Nested `AGENTS.md` files are useful for subproject rules. Codex also supports fallback names and override behavior — beginners do not need these on day one. Maintain one good root file first.

<h2 id="claude">For Claude Code Users</h2>

Claude Code reads `CLAUDE.md`. Common locations:

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
```

Project rules should live in the project. Use user-level memory (`~/.claude/CLAUDE.md`) for personal long-lived preferences. Do not keep project facts only in personal memory — they will disappear when the project moves to another person, machine, or environment.

<h2 id="reference">Reference</h2>

- OpenAI Codex / AGENTS.md: <https://developers.openai.com/codex/guides/agents-md>
- Claude Code / Memory: <https://docs.anthropic.com/en/docs/claude-code/memory>
