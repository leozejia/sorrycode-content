---
title: Waza
slug: waza
order: 1
summary: A full engineering-habits skill pack. Use it to think before building, debug by root cause, design with direction, learn from sources, write naturally, and check before shipping.
section: skills
section_title: Skills
section_order: 15
group_order: 30
group_title: Workflow
group: workflow
source_url: https://github.com/tw93/Waza
---

# Waza

`Waza` is not one tool. It is a full pack of engineering habits.

If `Kami` helps you ship finished documents and `SorryCode Image2` helps you generate images, `Waza` helps with the deeper question: how do you work with an agent without letting the task drift?

<h2 id="what-is-waza">What Waza Is</h2>

AI can make you faster, but speed does not automatically make the work steadier.

Common failure modes look like this:

- building before the problem is clear
- asking the agent to patch a bug before finding the root cause
- making UI without a design direction
- reading sources but only collecting summaries
- finishing a task without checking the diff and risks

`Waza` turns these engineering moves into reusable skills. It helps you pause at the right moments and move through the task with a better process.

<h2 id="why-recommend">Why We Recommend the Whole Pack</h2>

We recommend `Waza` as a pack because the skills cover the points where AI collaboration most often goes wrong.

It helps you build habits like:

- think before implementation
- debug by root cause, not guesses
- design with a committed direction
- turn sources into output
- check your work before someone else has to

For beginners, this is more important than memorizing another model flag. Models change; these habits keep paying off.

<h2 id="what-changes">What Changes After Installing It</h2>

You do not need to memorize every skill. Start with these situations:

- before building a feature, use Waza to pressure-test the plan
- when something breaks, use Waza to find the root cause first
- when building a page, use Waza to set the visual direction
- when reading long materials, use Waza to turn them into usable understanding
- before finishing a task, use Waza to check the work

The point is not writing a few more lines of code. The point is avoiding wasted loops.

<h2 id="install">Install</h2>

First make sure `Codex` or `Claude Code` is installed.

### Codex

```bash
npx skills add tw93/Waza -a codex -g -y
```

### Claude Code

```bash
npx skills add tw93/Waza -a claude-code -g -y
```

If you have not installed a runtime yet, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

`Waza` is a pack and may install multiple child skills. If you no longer need it, run `npx skills list --global`, copy the actual names, then remove them one by one with `npx skills remove --global skill-name`.

<h2 id="common-scenes">5 Common Scenes</h2>

### Before Building

```text
Use Waza's think workflow to review this feature plan. Do not write code yet. Find the boundaries, risks, and smallest implementation path first.
```

### Debugging

```text
Use Waza's hunt workflow to investigate this issue. Find the root cause before changing code.
```

### Interface Design

```text
Use Waza's design workflow for this page. Start with a clear visual direction before implementation.
```

### Reading Sources

```text
Use Waza's read / learn workflow to read this source and turn it into key points, structure, and conclusions I can use.
```

### Before Shipping

```text
Use Waza's check workflow to review this change. Focus on drift, omissions, risks, and missing validation.
```

<h2 id="first-prompt">First Prompt</h2>

If you do not know where to start, say:

```text
I want to use Waza to move through this task more steadily. Decide whether I should use think, hunt, design, read, learn, write, or check right now, then tell me the next step.
```

<h2 id="relationship">How It Relates to Other Skills</h2>

- `Kami`: finished documents, resumes, portfolios, and slide decks
- `SorryCode Image2`: images, covers, posters, and illustrations
- `Waza`: engineering workflow and task quality

They do not replace each other. A natural path is to use `Waza` to think clearly first, then use `Kami` or `SorryCode Image2` to produce the final artifact.

<h2 id="common-issues">Common Issues</h2>

- Do I need to memorize every skill name?
  No. Start with three habits: think before building, find root cause before fixing, check before finishing.
- Is Waza only for engineers?
  It is strongest for engineering work, but reading, learning, writing, and editing also benefit from it.
- I already use Kami. Do I still need Waza?
  Yes. `Kami` improves the final artifact. `Waza` improves the process.
- Why install it from upstream?
  Waza is a community-maintained skill collection. Installing from upstream keeps the source clear and follows the author’s updates.
