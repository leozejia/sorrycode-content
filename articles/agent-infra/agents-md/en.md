---
title: AGENTS.md
slug: agents-md
order: 2
summary: Project instructions read by Codex. Use it for project structure, test commands, code style, and working constraints.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# AGENTS.md

`AGENTS.md` is the project instruction file read by Codex.

Use it for project rules, test commands, code style, directory notes, and constraints. It is the project handbook for Codex.

This is an officially supported Codex mechanism, not a SorryCode-specific convention.

<h2 id="who-reads-it">Who Reads It</h2>

Codex reads the applicable `AGENTS.md` files.

Common locations:

```text
~/.codex/AGENTS.md
your-project/AGENTS.md
your-project/apps/web/AGENTS.md
```

Rules closer to the current working directory are more specific. A nested file can add to or override higher-level rules.

If a task touches multiple directories, Codex uses the applicable instructions for that working area and file scope. A nested `AGENTS.md` is useful when a subproject has its own rules, such as frontend, backend, scripts, or docs.

<h2 id="where">Where to Put It</h2>

Start at the project root:

```text
your-project/
  AGENTS.md
  README.md
  package.json
```

If a subdirectory needs different rules, add another one there:

```text
your-project/
  AGENTS.md
  frontend/
    AGENTS.md
```

Do not create many files on day one. Maintain one root file first, then split only when the rules really differ.

<h2 id="how-it-works">How It Takes Effect</h2>

After you put `AGENTS.md` in the project, Codex reads it while working in that project. You do not need to paste the whole file into every prompt.

For a first run, you can still be explicit:

```text
Read AGENTS.md first, then tell me this project's development and test rules.
```

<h2 id="what-to-write">What to Write</h2>

Good content:

- project structure
- install, test, and build commands
- code style and naming rules
- files or directories the agent should not change
- checks to run before finishing
- OS, encoding, or path notes

<h2 id="avoid">What Not to Write</h2>

Do not write:

- API keys, passwords, or tokens
- one-off tasks
- stale paths or commands
- unverifiable style wishes
- long background unrelated to the current tree

<h2 id="template">Small Template</h2>

```md
# AGENTS.md

## Project

This project is ...

## Commands

- Install:
- Test:
- Build:

## Code Style

- ...

## Do Not

- Do not ...
```

<h2 id="reference">Reference</h2>

- OpenAI Codex / AGENTS.md: <https://developers.openai.com/codex/guides/agents-md>
