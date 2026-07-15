---
title: How to Write Project Rules for Strong Models
slug: strong-model-project-rules
order: 6
summary: Audit AGENTS.md, CLAUDE.md, and always-on Skills. Keep project facts, permissions, and verification while testing the removal of older-model constraints.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# How to Write Project Rules for Strong Models

Old `AGENTS.md`, `CLAUDE.md`, and Skills do not expire when the model changes. A stronger model may follow every stale rule more carefully, so repeated constraints, conflicting preferences, and older-model patches can all affect the result.

The goal is not the fewest possible rules. Use the minimum correct design: keep what the model cannot infer reliably from the task and what directly affects correctness.

For a first rules file, read [Make AI Remember Project Rules](/docs/agent-memory/remember-rules). For the structure and purpose of Skills, read [Make AI Remember Work Methods](/docs/agent-memory/remember-skills). This page focuses on auditing existing rules after a model upgrade.

<h2 id="keep">What to Keep</h2>

| Rule type | Why it stays |
| --- | --- |
| Project goal and user boundary | Code alone does not reveal business intent |
| Source-of-truth files and directory ownership | Prevents edits to generated, mirrored, or stale copies |
| Install, test, build, and release commands | Makes results reproducible and verifiable |
| Data, permission, and external-write boundaries | Limits irreversible or high-risk actions |
| Product requirements and domain rules | These facts may not exist in public knowledge |
| Completion criteria and evidence requirements | Prevents unverified completion claims |
| Reliable scripts, templates, and tool entry points | Moves deterministic work into tools |

These rules connect the model to external facts and deterministic verification. A stronger model still cannot guess production constraints, source ownership, or acceptance criteria.

<h2 id="review">What to Review</h2>

| Rule type | Common problem |
| --- | --- |
| Several versions of the same preference | Repeats context and can conflict |
| Long persona and tone definitions | Affects every task even when irrelevant |
| Step-by-step corrections for older models | Strong models mechanically follow unnecessary steps |
| Generic Skills that trigger on every task | One method crowds out task-specific judgment |
| Too many positive and negative examples | The model imitates examples instead of solving the task |
| Stale paths, commands, and tool descriptions | Sends the agent toward an older system |
| Requests for full chain-of-thought output | Can trigger refusals and does not replace external verification |

Do not keep a rule because it sounds professional. It should carry a project fact, control a real risk, or fix a repeatable measured gap.

<h2 id="minimum-correct-design">A Minimal Change Is Not Always the Minimum Correct Design</h2>

"Less is more" is a design preference, not an absolute command.

If the current direction is wrong, making the smallest change inside it preserves the wrong structure. Use a rule like this:

```text
Prefer the minimum correct design.

When the current direction is correct, keep the change focused.
When the current direction is wrong, explain the evidence and target structure, then complete the necessary refactor.
Do not preserve a wrong abstraction only to reduce the diff, and do not use a refactor to expand into unrelated scope.
```

This controls both failure modes. The model does not keep patching a wrong direction, and "first principles" does not become permission for an unlimited rewrite.

<h2 id="audit">Audit With Representative Tasks</h2>

Do not delete most rules based on a reading impression. Compare the same tasks before and after each change.

1. Choose 3 to 5 real tasks covering routine edits, difficult fixes, and long-running work.
2. Save a baseline: completion, omissions, evidence, time, tokens, and cost.
3. Group rules into project facts, permissions, verification, style preferences, older-model patches, tools, and Skills.
4. Remove or merge one group at a time.
5. Run the same tasks with the same input and completion criteria.
6. Keep the deletion when results improve or stay equal. Restore the smallest necessary rule when a stable regression returns.

Token reduction is only one signal. Also check:

```text
The deliverable is correct.
Fewer required details are missing.
Claims cite real evidence.
No unauthorized action occurred.
No unrelated refactor appeared.
The same verification still passes.
```

<h2 id="skills">How to Treat Skills</h2>

Skills are still useful for:

- stable workflows for a specific deliverable
- domain knowledge the model cannot retrieve on its own
- tasks that require fixed scripts, templates, or assets
- error-prone operations that need repeatable verification

A Skill should not be always-on when it:

- only expresses general engineering taste
- treats one method as the default answer to every task
- repeats behavior already provided by the runtime
- has not been tested on real tasks but must be inherited by every subagent

Keep optional capabilities on demand. Install them permanently or expand their scope only after a real gap appears repeatedly.

<h2 id="template">A Short, Complete Project Rules Template</h2>

```md
# Project

What this project does and who uses it.

## Source of Truth

- Code source:
- Content source:
- Generated files that should not be edited directly:

## Commands

- Install:
- Test:
- Build:

## Authorization

- Local and reversible actions that are already allowed:
- External, destructive, or paid actions that require confirmation:

## Design Rule

- Prefer the minimum correct design.
- When the current direction is wrong, explain the evidence and complete the necessary refactor instead of preserving a wrong abstraction.
- Do not expand into unrelated scope.

## Verification

- Checks required before completion:
- State explicitly when verification is unavailable:

## Do Not

- Do not commit secrets or private data.
- Do not modify:
```

This is not a form that must be filled. Delete any section that has no real content. Do not keep empty headings.

<h2 id="ask-agent">Ask the Agent for a Read-Only Audit First</h2>

Copy this:

```text
Perform a read-only audit of AGENTS.md, CLAUDE.md, user-level rules, and automatically triggered Skills for this project.

Classify each rule as:
- project fact
- permission or risk boundary
- verification requirement
- preference, duplicate, or older-model patch

Every recommendation must include evidence and likely impact. Do not edit files yet.

Then choose 3 to 5 representative tasks and design a baseline. Later changes must modify one rule group at a time and rerun the same tasks.
```

Approve the audit before allowing edits. This prevents a large cleanup from deleting useful methods, scripts, and safety boundaries together.

<h2 id="model-guides">Model-Specific Guidance</h2>

- Claude Fable 5 emphasizes long runs, evidence-backed progress, autonomy boundaries, subagents, and memory. Anthropic also warns that older Skills can be too prescriptive. Continue with [How to Use Claude Fable 5](/docs/runtime/claude-fable-5).
- GPT-5.6 Sol emphasizes leaner prompts, reasoning effort, tool-routing boundaries, and evaluation on representative tasks. Continue with [How to Use GPT-5.6 Sol](/docs/runtime/gpt-5-6-sol).

<h2 id="default-rule">Default Test</h2>

```text
Write down facts the model cannot access.
Write down boundaries where unauthorized action can cause loss.
Write down verification the result must pass.
Do not reteach general judgment the model already handles reliably.
Validate every deletion on the same real tasks.
```

<h2 id="reference">References</h2>

- Anthropic / Prompting Claude Fable 5: <https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5>
- OpenAI / GPT-5.6 model guidance: <https://developers.openai.com/api/docs/guides/latest-model>
