---
title: Open Design
slug: open-design
order: 4
summary: An open-source design workbench that combines local agent CLIs, skills, DESIGN.md design systems, and artifact preview.
section: tools
section_title: Tools
section_order: 28
source_url: https://github.com/nexu-io/open-design
---

# Open Design

`Open Design` is an open-source design workbench.

It is not a single skill and it is not the default beginner path for SorryCode. It is a full design environment that combines local agent CLIs, skills, `DESIGN.md` design systems, project files, and artifact preview.

If you already understand `Codex / Claude Code + Skills` and want to study AI design workflows, Open Design is worth reading.

<h2 id="what-is-it">What It Is</h2>

The core idea:

```text
agent runtime + SKILL.md + DESIGN.md + artifact preview = design workbench
```

Open Design detects local agent CLIs such as Codex, Claude Code, Gemini CLI, and OpenCode, then lets those agents generate webpages, prototypes, decks, posters, motion pieces, and other artifacts inside a design task environment.

It also ships design systems and skills, so a user can combine a design system, a task skill, and a brief into one generation flow.

<h2 id="why-recommend">Why We Recommend It</h2>

We recommend it because it shows the direction of AI design workbenches:

- `DESIGN.md` manages design context
- `SKILL.md` manages task workflow
- local agent CLIs perform real file operations
- preview panes render artifacts
- project folders preserve outputs for further editing

This helps explain the whole `Creation and Design` direction.

<h2 id="requirements">Requirements</h2>

Open Design currently fits users who are comfortable with local setup.

The upstream quickstart states:

- Node.js: `~24`
- pnpm: `10.33.x`
- macOS, Linux, and WSL2 are the primary paths
- optional local agent CLI: Codex, Claude Code, Gemini CLI, and others

This differs from SorryCode’s current one-click Node 22 LTS path, so it should not be the default first step for beginners.

<h2 id="how-to-start">How to Start</h2>

If you want to study it, follow the upstream instructions:

```bash
corepack enable
pnpm install
pnpm tools-dev run web
```

Open the local URL printed by the terminal, then choose a skill, design system, and agent.

Use the official repository as the source of truth: <https://github.com/nexu-io/open-design>

<h2 id="relationship">Relationship With SorryCode</h2>

- `SorryCode`: helps you create an API key and run the runtime/model path.
- `Skills / Creation and Design`: recommends installable design skills.
- `Agent Infrastructure / DESIGN.md`: explains design context files.
- `Open Design`: shows how these concepts combine into a design workbench.

If you only want to generate an image, make a one-pager, or build a deck, start with [Skills / Creation and Design](/docs/skills/creation-design).
