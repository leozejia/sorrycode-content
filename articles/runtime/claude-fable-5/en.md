---
title: How to Use Claude Fable 5
slug: claude-fable-5
order: 2
summary: Use Claude Fable 5 for difficult long-running work, choose effort intentionally, and review prompts and Skills written for older models.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: anthropic
group_title: Anthropic
group_order: 20
---

# How to Use Claude Fable 5

`claude-fable-5` is Anthropic's model for demanding reasoning and long-horizon agent work. It is intended for work that used to take a person hours or days, or required several handoffs to complete.

If Claude Code is not connected yet, start with [Models & Runtimes / Claude Code](/docs/runtime/claude-code). This page does not repeat installation or API key setup. It explains when to choose Fable 5 and how to give it a task.

<h2 id="when-to-use">When to Choose Fable 5</h2>

| Task | Recommendation |
| --- | --- |
| Large refactors, difficult debugging, cross-repository research | Good fit |
| Complete projects that run for hours and require self-verification | Good fit |
| Complex code review, documents, or enterprise workflows | Good fit |
| A small copy edit, format conversion, or short question | Start with a lighter model |
| Offensive cybersecurity or some life sciences work | May trigger a safety refusal |

Do not evaluate Fable 5 only with a simple exercise. Give it a real, bounded task that previously needed several rounds of work. That is where its long-run execution, verification, and delegation become useful.

<h2 id="first-run">Shortest Working Path</h2>

1. Connect Claude Code and verify the API key and network path.
2. Select `claude-fable-5` in an entry point that supports model selection.
3. Start most tasks at `high` effort.
4. State the goal, context, approval boundaries, completion criteria, and evidence requirements.
5. Let the model work end to end, then adjust effort based on time and results.

Use this for a first run:

```text
I am working on [project or larger goal] for [the people who will use it].

Read [source-of-truth files or folders] and produce [specific deliverable].

You may perform:
- [allowed local and reversible actions]

Stop before:
- [destructive actions, external writes, or a real scope change]

Completion criteria:
- [checkable result]
- [tests or verification that must pass]

Before reporting progress, audit every claim against a tool result from this session. State explicitly when a step has not been verified.
```

<h2 id="effort">Choose an Effort Level</h2>

| Effort | Good fit |
| --- | --- |
| `low` | Routine, low-risk work where interaction speed matters |
| `medium` | Normal work that needs some reasoning but not a long run |
| `high` | Default starting point for most Fable 5 tasks |
| `xhigh` | Capability-sensitive tasks with demanding verification |

Higher effort can produce stronger reasoning and verification. It can also gather too much context, revisit decisions, or tidy work that was never requested.

If the result is correct but the run is much slower than needed, lower effort first. Do not keep adding system-prompt patches such as "do not overthink" or "do not overplan."

<h2 id="prompting">Keep the Prompt Short, Not Empty</h2>

Fable 5 follows instructions strongly. One clear direction often works better than a long list of banned behaviors.

Keep:

- why the work matters
- source-of-truth files or data
- actions already authorized
- actions that require confirmation
- the definition of done
- evidence required for completion claims

Review or remove:

- repeated versions of the same preference
- narrow prohibitions written for older models
- instructions to reproduce full internal reasoning
- tools and examples unrelated to the current task

A lean prompt is not missing context. It is a short, complete task contract.

<h2 id="long-runs">Ground Progress in Evidence</h2>

Anthropic recommends grounding status claims in tool results from the current session. Add this to long-running tasks:

```text
Before reporting progress, audit each claim against tool results from this session.
Only report work supported by evidence.
Report failed tests as failed, skipped steps as skipped, and unverified work as unverified.
```

This rule controls completion claims. It does not prescribe how the model should think, so it is useful as a durable rule.

<h2 id="boundaries">State Autonomy Boundaries Once</h2>

Fable 5 is more willing to continue on its own, and it may take actions that were not requested. Define the boundary by request type:

- Questions, discussion, diagnosis, and review return an assessment without applying a fix.
- Explicit change requests authorize local, reversible work inside the stated scope.
- Deletion, restarts, external configuration changes, messages, and scope expansion require evidence and user confirmation.

Do not repeat "ask me first" for every tool. One compact policy lets the model continue safe work and stop where confirmation is actually needed.

<h2 id="subagents">When to Use Subagents</h2>

Fable 5 is stronger at parallel delegation. Use subagents only when work can split into independent streams, such as:

- reading separate repositories
- checking independent sources
- separating implementation, testing, and independent verification

The main agent should keep working and intervene when a subagent lacks context or leaves the task boundary. Work that depends on one rapidly changing shared state is a poor fit for forced parallelism.

<h2 id="memory">Store Only Verified Lessons</h2>

Long-running agents can use a dedicated notes folder, but they should not create status ledgers throughout the repository.

Store one verified lesson per file with a one-line summary at the top. Do not copy facts already present in the repository or chat history. Update or delete a note when later evidence disproves it.

For session length, caching, and handoffs, continue with [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management).

<h2 id="migration">Migrate Old Prompts and Skills</h2>

Anthropic explicitly warns that Skills written for older models can be too prescriptive and may reduce Fable 5 output quality.

Do not clear every rule at once. Use this migration loop:

1. Select 3 to 5 real, repeatable tasks.
2. Save the baseline result, including success, completeness, evidence, time, and cost.
3. Remove one group of repeated instructions, old examples, or unrelated tools.
4. Run the same tasks again.
5. Keep the deletion when default performance improves. Restore a rule when a measured regression returns.

See [How to Write Project Rules for Strong Models](/docs/agent-memory/strong-model-project-rules) for the full audit method.

<h2 id="refusal">Handle Refusals</h2>

Fable 5 runs safety classifiers for some cybersecurity, life sciences, and internal-reasoning extraction requests. The API may return `stop_reason: "refusal"`.

Check whether the request falls inside a restricted area. Benign work can also be misclassified. Integrations that need automatic recovery can follow Anthropic's guidance and configure a fallback model such as Claude Opus 4.8. Do not retry the same request forever without changing it.

<h2 id="next">Next Step</h2>

- Connect Claude Code: [Models & Runtimes / Claude Code](/docs/runtime/claude-code)
- Manage long sessions: [Agent Infrastructure / What to Do When Sessions Get Too Long](/docs/agent-memory/context-management)
- Audit project rules: [Agent Infrastructure / How to Write Project Rules for Strong Models](/docs/agent-memory/strong-model-project-rules)

<h2 id="reference">References</h2>

- Anthropic / Prompting Claude Fable 5: <https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5>
- Anthropic / Introducing Claude Fable 5 and Claude Mythos 5: <https://platform.claude.com/docs/en/about-claude/models/introducing-claude-fable-5-and-claude-mythos-5>
