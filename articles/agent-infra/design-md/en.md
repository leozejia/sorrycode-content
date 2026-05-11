---
title: What Is DESIGN.md
slug: design-md
order: 4
summary: DESIGN.md is a design context file for agents. It captures product goals, brand principles, design tokens, components, layout rules, and things to avoid.
section: agent-infra
section_title: Agent Infrastructure
section_order: 32
---

# What Is DESIGN.md

`DESIGN.md` is a design context file for agents.

It sits in the same family as `AGENTS.md` and `CLAUDE.md`: long-lived project context that an agent can read before doing work. `AGENTS.md` and `CLAUDE.md` usually describe project rules and working conventions. `DESIGN.md` describes what the product should look and feel like.

Google Labs has published an alpha `design.md` specification and CLI, so this is best described as an emerging design-agent convention. It is not a finalized industry standard, but it is already concrete enough to document and use.

<h2 id="who-reads-it">Who Reads It</h2>

Typical readers include:

- design-focused skills
- Codex, Claude Code, and other agent runtimes
- design workbenches such as Open Design
- agents that generate UI, images, slides, or documents from project files

It is not tied to one model or to SorryCode. Its value is that different agents can read the same design context.

<h2 id="problem">What It Solves</h2>

Design tasks fail when context drifts:

- you repeat the same colors, fonts, and style rules every time
- the agent forgets what not to use
- pages, posters, decks, and images do not share a visual language
- switching agent runtimes loses the project’s design rules
- outputs look like generic templates

`DESIGN.md` turns those rules into a readable project file.

<h2 id="where">Where to Put It</h2>

The common location is the project root:

```text
your-project/
  DESIGN.md
  AGENTS.md
  README.md
  assets/
  outputs/
```

Large projects can use more specific files such as `apps/web/DESIGN.md`, but the public docs should recommend one root file first.

<h2 id="what-to-write">What to Write</h2>

A complete `DESIGN.md` often includes:

- product goals: who the product serves and what the core experience is
- brand principles: what the product should communicate
- design tokens: colors, typography, spacing, radius, shadow, motion
- components: buttons, cards, forms, navigation, dialogs, states
- layout principles: grid, responsiveness, density, whitespace, hierarchy
- interaction states: hover, focus, loading, empty, error, success
- accessibility: contrast, keyboard navigation, semantic structure
- Do / Don’t: clear visual rules
- asset locations: logos, screenshots, brand images, icons

<h2 id="avoid">What Not to Write</h2>

Do not put these in `DESIGN.md`:

- API keys, passwords, or provider secrets
- short-lived tasks such as “do the homepage today”
- vague style words with no rules behind them
- long business notes unrelated to design decisions
- stale brand rules or outdated screenshots

If a sentence does not help the agent make a steadier design decision, leave it out.

<h2 id="starter">Small Starter Template</h2>

Start with this:

```md
# DESIGN.md

## Project Feel

The project should feel calm, clear, and credible. Avoid exaggerated sci-fi styling.

## Colors

- Primary: ink blue
- Supporting: warm white, light gray
- Avoid: high-saturation neon colors

## Typography and Layout

- Keep body text readable
- Make headings clear, not decorative
- Use enough whitespace

## Images and Assets

- Put input assets in `assets/`
- Put outputs in `outputs/`

## Avoid

- generic AI styling
- tiny unreadable text
- broken or non-editable text in images
```

<h2 id="advanced">Advanced Structure</h2>

For a long-lived project, expand it like this:

```md
# DESIGN.md

## Product Context

## Brand Principles

## Design Tokens

### Colors

### Typography

### Spacing

### Radius and Shadow

## Components

### Buttons

### Cards

### Forms

### Navigation

## Layout

## Interaction States

## Accessibility

## Assets

## Do

## Don't
```

<h2 id="how-to-use">How to Use It</h2>

After you put `DESIGN.md` in the project folder, say:

```text
Read DESIGN.md first, then use Kami to turn this content into a one-pager. Before starting, tell me which design rules you will follow.
```

Or:

```text
Read DESIGN.md first, then use SorryCode Image2 to generate a product poster. Keep the existing project style and save it to outputs/images/poster/.
```

<h2 id="relationship">How It Relates to Skills</h2>

A skill tells the agent how to do a class of work, such as image generation, document layout, or web-style presentation decks.

`DESIGN.md` tells the agent what this project should look like.

Use both together: the skill gives the workflow, and `DESIGN.md` gives the style boundary.

<h2 id="references">References</h2>

- Google Labs `design.md`: <https://github.com/google-labs-code/design.md>
- Open Design `DESIGN.md` examples: <https://github.com/VoltAgent/awesome-design-md>
