---
title: How to Manage Long-Lived Context
slug: context-management
order: 2
summary: Long sessions, cache, context files, and handoffs are different things. Keep durable truth and clear historical debt.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# How to Manage Long-Lived Context

An agent can keep working in one session for a long time. That does not mean every old detail should stay there forever.

At first, long sessions feel great.

The agent remembers what changed, knows which files matter, and you do not need to repeat the same background every time. Cache hit rate may also look high, which makes the session feel cheaper the longer it runs.

But there is a trap:

```text
a high cache hit rate is not the same as a healthy session.
```

Caching only means some input was reused. It does not decide whether that input is still correct.

If the reused content is project rules, it is an asset.

If it is old conclusions, failed attempts, stale paths, or temporary logs, it is historical debt.

<h2 id="three-places">Start With Three Places</h2>

Long-running agent work needs at least three layers:

| Place | What belongs there |
| --- | --- |
| Current session | The active task, recent errors, temporary evidence |
| Context files | Durable rules, project structure, common commands, stable preferences |
| Handoff | A transfer note before releasing a session |

Do not use chat history as a database.

Chat is for movement. Files are for durable truth. Handoffs are for switching sessions.

<h2 id="context-files">What Belongs in Context Files</h2>

If a piece of information will be reused, do not explain it again every time.

For coding, put it in [AGENTS.md](/docs/agent-infra/agents-md) or [CLAUDE.md](/docs/agent-infra/claude-md).

For design, put it in [DESIGN.md](/docs/agent-infra/design-md).

Good durable content includes:

- what the project does
- directory structure
- common install, test, and build commands
- code style and naming rules
- important business rules
- design style and things to avoid
- files the agent should not change
- checks to run before finishing

These are stable assets.

<h2 id="do-not-store">What Not to Store</h2>

Do not put these into `AGENTS.md / CLAUDE.md / DESIGN.md`:

- API keys, tokens, or passwords
- one-off tasks
- temporary TODOs
- long error logs
- abandoned plans
- stale paths or commands
- summaries the agent wrote and later disproved
- long background unrelated to the project

If a line will not make the next task more stable, do not put it in a durable context file.

<h2 id="cache">Cache Is Not Free Memory</h2>

Prompt caching can make repeated context cheaper and faster, but it is not free.

Pricing changes by model, provider, and runtime. Beginners do not need to memorize a price table. Remember this:

```text
input, output, and cached input may have different prices.
```

So do not only look at “90% cache hit rate.”

Also ask:

```text
is this cached content still moving the task forward?
```

If it still helps, keep it.

If it only drags old noise into the next turn, clear it.

<h2 id="when-release">When to Release a Session</h2>

Release the session when you see these signs:

```text
the direction changed
the agent keeps citing old conclusions
the session contains lots of logs and failed attempts
you can no longer tell which instruction it should follow
```

Do not just close the session. Ask for a handoff first.

<h2 id="handoff">Ask for a Handoff Before Releasing</h2>

Copy this:

```text
I am going to release this session.

Please review the health of the current project documents and prepare a handoff for your successor.

The handoff should include:
- current goal
- confirmed facts
- abandoned directions
- key files and links
- only the context needed for the next step
- old information that should no longer be used

End with one sentence that lets the successor quickly align with the project.
```

The most important line is:

```text
old information that should no longer be used
```

Many handoffs only say what happened. The more important part is what has expired.

A new session can easily be polluted by old conclusions. If you do not mark them, the next agent may treat every historical line as usable context.

<h2 id="after-handoff">What to Do After the Handoff</h2>

After you have a handoff:

1. Move durable rules into `AGENTS.md / CLAUDE.md / DESIGN.md`.
2. Leave temporary logs, failed attempts, and abandoned plans in the old session.
3. Start a new session.
4. Ask the new agent to read the relevant context files and handoff first.

You can start with:

```text
Read AGENTS.md / CLAUDE.md and this handoff first.

Do not edit files yet. First tell me:
- current goal
- confirmed conclusions
- old directions that should not be used
- what you plan to do next
```

If it misunderstands the project state, correct it before continuing.

<h2 id="default-rule">Default Rule</h2>

For long-running agent work:

```text
stable information goes into files
temporary evidence gets discarded after use
complex work needs checkpoints
new direction means new session
```

More context is not always better. Good context helps the next step avoid old mistakes.

