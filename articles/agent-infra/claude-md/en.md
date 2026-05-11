---
title: CLAUDE.md
slug: claude-md
order: 3
summary: Memory and instruction file read by Claude Code. Use it for project context, common commands, and long-lived collaboration rules.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# CLAUDE.md

`CLAUDE.md` is the memory and instruction file read by Claude Code.

Use it for project context, common commands, long-lived preferences, and collaboration rules. Like `AGENTS.md`, it reduces repeated explanation.

This is an officially supported Claude Code memory mechanism, not a SorryCode-specific convention.

<h2 id="who-reads-it">Who Reads It</h2>

Claude Code reads applicable `CLAUDE.md` files.

Common locations:

```text
~/.claude/CLAUDE.md
your-project/CLAUDE.md
your-project/apps/web/CLAUDE.md
```

Use the Claude Code official docs as the source of truth for exact loading behavior. The stable public recommendation is: keep one maintained `CLAUDE.md` at the project root.

<h2 id="where">Where to Put It</h2>

The safest default is the project root:

```text
your-project/
  CLAUDE.md
  README.md
```

Use user-level memory for personal long-lived preferences. Use the project `CLAUDE.md` for project rules.

<h2 id="how-it-works">How It Takes Effect</h2>

Claude Code loads available memory during the session. On the first run in a project, you can ask it to confirm:

```text
Read CLAUDE.md first, then tell me the common commands and important notes for this project.
```

If you edit `CLAUDE.md`, future sessions should use the new content. If you are unsure whether the current session has refreshed it, ask Claude Code to read it again.

<h2 id="what-to-write">What to Write</h2>

Good content:

- what the project is
- common development, test, and build commands
- code style and directory conventions
- common pitfalls and things to avoid
- important business rules
- collaboration preferences

<h2 id="avoid">What Not to Write</h2>

Do not write:

- API keys, tokens, or passwords
- one-off tasks or temporary TODOs
- stale commands
- long meeting notes
- information unrelated to agent work

<h2 id="template">Small Template</h2>

```md
# CLAUDE.md

## Project Context

This project is ...

## Common Commands

- Test:
- Build:

## Working Rules

- ...

## Avoid

- ...
```

<h2 id="relationship">Relationship With AGENTS.md</h2>

If you use both Codex and Claude Code, maintain both `AGENTS.md` and `CLAUDE.md`.

Keep facts consistent. Put shared project rules in both files when needed, and runtime-specific rules in the matching file.

<h2 id="reference">Reference</h2>

- Claude Code / Memory: <https://code.claude.com/docs/en/memory>
