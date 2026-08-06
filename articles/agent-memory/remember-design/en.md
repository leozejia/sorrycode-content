---
title: Make AI Remember Your Design Style
slug: remember-design
order: 4
summary: Store brand colors, fonts, and visual constraints in DESIGN.md, then explicitly ask the agent to read it for design tasks.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# Make AI Remember Your Design Style

Design tasks often require the same reminders about brand colors, typography, layout, and prohibited styles. Put these stable requirements in `DESIGN.md` so different sessions and tools can read the same constraints.

`DESIGN.md` is not a universal protocol that every agent reads automatically. Reference it from project instructions, a Skill, or the current task.

<h2 id="what-is-it">What Is DESIGN.md</h2>

`DESIGN.md` is a text file written for agents. It can include:

- What feel the brand should have
- What colors, fonts, and sizes to use
- What buttons, cards, and forms should look like
- Which design patterns must not be used

It can supplement Figma or an existing design system, but it does not replace source designs, component libraries, or human review.

<h2 id="where">Where to Put It</h2>

Put it in the work folder that contains the relevant assets and outputs:

```text
my-work-folder/
  DESIGN.md
  assets/
  outputs/
```

<h2 id="who-reads-it">Who Reads It</h2>

Tools that can read it include:

- Design Skills that explicitly support the file
- File-capable agents such as Codex and Claude Code
- Design workbenches like Open Design

File access does not mean the agent will look for `DESIGN.md` on its own. Check the current tool or Skill documentation before relying on it.

<h2 id="what-to-write">What to Write</h2>

A complete DESIGN.md often includes:

- **Project Feel:** What feeling the project should convey, what to avoid
- **Brand Principles:** What to communicate, what not to communicate
- **Design Tokens:** Colors, typography, spacing, radius, shadow
- **Component Specs:** Button, card, form, navigation, dialog styles
- **Layout Principles:** Grid, responsiveness, density, whitespace, hierarchy
- **Interaction States:** hover, focus, loading, empty, error, success
- **Do / Don't:** Clear recommended and forbidden visual practices
- **Asset Locations:** Where logos, screenshots, brand images, icons are

<h2 id="avoid">What Not to Write</h2>

Don't put these in:

- API keys, passwords, or provider secrets
- Temporary tasks like "do homepage today"
- Unverifiable vague words like "needs to be very premium"
- Long business notes unrelated to design
- Outdated brand rules and old screenshots

If a sentence doesn't help AI make steadier visual decisions, leave it out.

<h2 id="starter">Minimal Template</h2>

Start with this short template:

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

- Generic AI styling
- Tiny unreadable text
- Broken or non-editable text in images
```

<h2 id="how-to-use">How to Make AI Use It</h2>

After putting `DESIGN.md` in the work folder, name it in the task:

```text
Read DESIGN.md first, then use Kami to turn this content into a one-pager. Before starting, tell me which design constraints you'll follow.
```

For long-term use, reference it from `AGENTS.md`, `CLAUDE.md`, or the project instructions supported by the current tool. Follow that agent's official documentation for the instruction file.

For an image task, you can say:

```text
Read DESIGN.md first, then use SorryCode Image2 to generate a product poster. Keep the existing project style and save to outputs/images/poster/.
```

<h2 id="relationship">How It Relates to Skills</h2>

Skills provide the task workflow. `DESIGN.md` stores visual constraints for the current project. Those constraints enter the current context only when the Skill or task reads the file.

<h2 id="not-perfect">DESIGN.md Is Not Perfect</h2>

- An agent may miss, misread, or ignore part of the file. Review important artifacts.
- Complex work still needs source assets, screenshots, or component specifications.
- Update the file when rules change, and remove outdated screenshots and requirements.

<h2 id="references">References</h2>

- Google Labs `design.md`: <https://github.com/google-labs-code/design.md>
- Open Design `DESIGN.md` examples: <https://github.com/VoltAgent/awesome-design-md>

<h2 id="next">What's Next</h2>

- Choose a design capability: [Skills / Creation and Design](/docs/skills/creation-design)
- Explore a design workbench: [Tools / Open Design](/docs/tools/open-design)
- Store development rules: [Make AI Remember Project Rules](/docs/agent-memory/remember-rules)
