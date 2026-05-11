---
title: DBSkill
slug: dbskill
order: 2
summary: A business diagnosis and content decision toolkit by dontbesilent. Use it to diagnose business questions, find benchmarks, review content direction, improve hooks and titles, and inspect execution blocks.
section: skills
section_title: Skills
section_order: 15
group_order: 30
group_title: Workflow
group: workflow
source_url: https://github.com/dontbesilent2025/dbskill
---

# DBSkill

`DBSkill` is an open-source business diagnosis toolkit by dontbesilent.

Use it when you are working on a product, content account, service, or business project and keep getting stuck on questions like “is this problem real,” “who should I learn from,” “why does this content not work,” or “why do I know what to do but still avoid doing it.”

It is closer to a set of business diagnostic tools than a normal writing assistant. Its value is not writing more text for you. Its value is helping you avoid spending effort on the wrong question.

<h2 id="what-is-it">What It Is</h2>

`DBSkill` is a collection of skills for business diagnosis, benchmark analysis, content diagnosis, hook and title work, execution diagnosis, concept deconstruction, and agent workspace migration.

You do not need to memorize every sub-skill. For the first run, remember the main entry point: `dbs`. Describe your problem and let it route you to the right diagnostic path.

<h2 id="who-is-it-for">Who It Is For</h2>

It is useful if you are:

- building a product, service, content account, or business project
- trying to decide whether a business question is real
- looking for benchmarks but unsure who is worth learning from
- diagnosing topics, short-video openings, or Xiaohongshu titles
- avoiding work even though you know what should be done
- confused by broad concepts like positioning, demand, growth, or category

If you only want image generation, document layout, or web-style presentation decks, start here instead:

- [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- [Skills / Kami](/docs/skills/kami)
- [Skills / Magazine Web PPT](/docs/skills/magazine-web-ppt)

<h2 id="install">Install</h2>

Make sure you have installed `Codex` or `Claude Code` first.

### Codex

```bash
npx skills add dontbesilent2025/dbskill -a codex -g -y
```

### Claude Code

```bash
npx skills add dontbesilent2025/dbskill -a claude-code -g -y
```

If your runtime is not ready yet, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="common-scenes">Common Use Cases</h2>

### You Do Not Know Which Tool to Use

```text
Use dbs to help me identify the biggest problem in my current project. First decide whether I should enter business diagnosis, benchmark analysis, content diagnosis, execution diagnosis, or concept deconstruction.
```

### Diagnose a Business Question

```text
Use dbs-diagnosis to diagnose my business model. I will describe what I am building. Do not rush into advice; first decide whether my question itself is valid.
```

### Find Benchmarks

```text
Use dbs-benchmark to help me find benchmarks. I want to build: ____. First filter out people I should not copy, then tell me who is actually worth learning from.
```

### Review Content Direction

```text
Use dbs-content to diagnose whether this topic is worth making and how I should make it. I will provide the topic and target platform first.
```

### You Know What to Do but Avoid Doing It

```text
Use dbs-action to diagnose why I know I should do this, but still have not started. Be direct about what I may be avoiding.
```

<h2 id="tool-map">How to Understand the Toolkit</h2>

You can think of it in four groups:

- Business judgment: `dbs`, `dbs-diagnosis`, `dbs-benchmark`
- Content growth: `dbs-content`, `dbs-hook`, `dbs-xhs-title`, `dbs-ai-check`
- Action and thinking: `dbs-action`, `dbs-slowisfast`, `dbs-deconstruct`, `dbs-chatroom`
- Agent workspace: `dbs-agent-migration`

Do not try to learn everything on day one. Start with `dbs` and let the agent route the task.

<h2 id="relationship">Relationship With Other Skills</h2>

- `DBSkill`: diagnose business questions, content direction, and execution blocks
- `Waza`: make AI coding workflows steadier
- `Kami`: turn material into polished documents, resumes, portfolios, and slides
- `SorryCode Image2`: generate images, covers, posters, and illustrations

A natural workflow is: use `DBSkill` to decide direction, then use `Kami`, `Magazine Web PPT`, or `SorryCode Image2` to make the final artifact.

<h2 id="common-issues">Common Issues</h2>

- Do I need to memorize all 13 skill names?
  No. Start with the `dbs` entry point and let it choose the path.
- Is it only for founders?
  It is strongest for business, content, startup, and personal project decisions. It is not the default tool for generic writing, layout, or image generation.
- Is the tone direct?
  Yes. It is a diagnostic toolkit, not an emotional support assistant.
- Can `dbs-action` replace therapy?
  No. It can help you observe execution blocks, but it is not psychological counseling, medical advice, or treatment.
- Can I use or repackage it commercially?
  Read the upstream license first. The project uses `CC BY-NC 4.0`; commercial use requires permission from the author.

<h2 id="references">References</h2>

- Official repository: <https://github.com/dontbesilent2025/dbskill>
- Author: dontbesilent
- License: `CC BY-NC 4.0`
