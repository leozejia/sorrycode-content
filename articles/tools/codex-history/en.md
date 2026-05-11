---
title: What to do when old Codex sessions disappear after switching providers
slug: codex-history
order: 7
summary: Use codex-history to find local Codex sessions and resume the right one.
section: tools
section_title: Tools
section_order: 28
updated_at: 2026-05-10
source_url: https://github.com/leozejia/codex-history
---

# What to do when old Codex sessions disappear after switching providers

After switching API providers, changing the base URL, or rerunning setup, you may hit a confusing problem: Codex still starts, but the session you were working on is no longer visible.

Do not start over immediately. Many sessions are still stored on your machine. They are just not showing up in the current entry point. `codex-history` solves this one problem: find local Codex sessions, then continue with `resume`.

## Recover an old session in two steps

First, list local sessions:

```bash
npx --yes codex-history@latest list
```

Here, `npx` runs the npm package temporarily without installing it into your project. `--yes` skips the npm confirmation prompt. `list` tells the tool to list historical sessions.

You will see recent Codex sessions. The output includes the session id, project path, provider, title, and ready-to-copy commands such as:

```bash
codex resume SESSION_ID
```

Second, copy that command and run it:

```bash
codex resume SESSION_ID
```

Replace `SESSION_ID` with the real id from the list.

## Pick instead of copying an id

If you just want to choose one from a list, run:

```bash
npx --yes codex-history@latest resume --pick
```

It opens a picker. Select the target session, press Enter, and the tool calls:

```bash
codex resume SESSION_ID
```

## Find the right session when there are too many

Search by title, path, first user message, or session id:

```bash
npx --yes codex-history@latest list --query sorrycode
```

Search and resume directly:

```bash
npx --yes codex-history@latest resume --pick --query sorrycode
```

Filter by project path:

```bash
npx --yes codex-history@latest resume --pick --cwd labs/sorrycode
```

Filter by provider:

```bash
npx --yes codex-history@latest resume --pick --provider openai
```

If switching providers is the reason you cannot find the old session, first check which providers appear in local history:

```bash
npx --yes codex-history@latest providers
```

## Turn on debug when nothing shows up

If the list is empty, or you suspect the tool is reading the wrong Codex state database, run:

```bash
npx --yes codex-history@latest list --debug
```

It prints the selected database, discovered candidate databases, and whether each candidate is compatible. By default, it looks under:

```text
~/.codex
```

If you know where the state database is, specify it manually:

```bash
npx --yes codex-history@latest list --db ~/.codex/state_5.sqlite
```

You can also use an environment variable:

```bash
CODEX_STATE_DB=~/.codex/state_5.sqlite npx --yes codex-history@latest list
```

## What fork means

`resume` continues the original session.

`fork` copies a historical session into a new context so you can try a different direction while keeping the original branch intact:

```bash
npx --yes codex-history@latest fork --pick
```

It ultimately calls:

```bash
codex fork SESSION_ID
```

## What it does not do

`codex-history` only reads the local Codex state database. It does not write to Codex SQLite databases and does not upload your session content.

It cannot restore something that no longer exists remotely, and it is not a token or cost analytics tool. It solves one specific problem: the local session exists, but you cannot find the current entry point to resume it.

## Common commands

```bash
# List recent sessions
npx --yes codex-history@latest list

# Pick a session to resume
npx --yes codex-history@latest resume --pick

# Search by keyword, then resume
npx --yes codex-history@latest resume --pick --query sorrycode

# Search by project path, then resume
npx --yes codex-history@latest resume --pick --cwd labs/sorrycode

# Show provider distribution
npx --yes codex-history@latest providers

# Show database discovery details
npx --yes codex-history@latest list --debug
```

## Open source links

```text
https://github.com/leozejia/codex-history
```

```text
https://www.npmjs.com/package/codex-history
```
