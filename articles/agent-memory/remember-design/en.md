---
title: Make AI Remember Your Design Style
slug: remember-design
order: 4
summary: Write a DESIGN.md file to make AI follow your brand colors, fonts, and visual style every time it generates images, decks, or web pages.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# Make AI Remember Your Design Style

## Are You Running Into These Problems

- ❌ Ask AI to generate 10 images, each one looks different
- ❌ Making PPT, posters, web pages, always repeating "use our brand colors"
- ❌ AI-generated designs look like "AI default templates"
- ❌ Switch agent or start a new session, previous design requirements all forgotten

**The solution is simple: write a file called DESIGN.md.**

Put it in your work folder, AI will read it before generating any design, automatically following your design requirements.

## 5-Second Overview

```text
Problem: AI doesn't remember my design requirements
Solution: Write a DESIGN.md file
Location: Work folder (together with your other files)
Effect: AI reads it automatically every time, keeps style consistent
```

<h2 id="comparison">With DESIGN.md vs Without DESIGN.md</h2>

### Without DESIGN.md

```text
You: Please generate a product poster
AI: (generates gradient background + futuristic font + neon colors)
You: No, our brand is restrained, use ink blue
AI: (regenerates, style still wrong)
You: Forget it, I'll fix it myself...
```

### With DESIGN.md

```text
You: Read DESIGN.md first, then generate a product poster
AI: Design guidelines loaded. Will use ink blue primary color, restrained layout, ample whitespace.
You: (Perfect on first try)
```

<h2 id="what-is-it">What Is DESIGN.md</h2>

DESIGN.md is a text file containing your design requirements:

- What feel the brand should have
- What colors, fonts, and sizes to use
- What buttons, cards, and forms should look like
- What designs absolutely cannot be used

**It's not a design spec for humans** (that's Figma or Design System).  
**It's design requirements for AI** (written in natural language AI can understand).

<h2 id="where">Where to Put It</h2>

Simplest way: put it in your work folder.

```text
my-work-folder/
  DESIGN.md          ← This file
  assets/            ← Your materials
  outputs/           ← AI generated results
  other files...
```

**No "project" concept needed.** Even if your files are scattered across desktop and downloads, you can:

1. Create a new folder
2. Throw common materials in
3. Write a DESIGN.md inside
4. Tell AI: "Enter this folder, read DESIGN.md, start working"

<h2 id="who-reads-it">Who Reads It</h2>

Typical readers include:

- Design skills (SorryCode Image2, Kami, Magazine Web PPT)
- Codex, Claude Code, and other agent runtimes
- Design workbenches like Open Design
- Agents that can read files and generate UI, images, PPT, or documents

It's not tied to one model or SorryCode-specific. Its value is letting different agents read the same design requirements.

<h2 id="problem">What Problem It Solves</h2>

Design tasks fail not because "agents can't make images," but because style is unstable:

- Repeating brand colors, fonts, and style every time
- Agent forgets what designs not to use
- Pages, posters, PPT, images each have different styles
- Switching agents in the same project loses visual rules
- Output looks like default templates, lacks project character

DESIGN.md turns these requirements into a readable file, reducing repeated verbal explanations.

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

<h2 id="advanced">Advanced Structure</h2>

For long-term projects, expand it like this:

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

<h2 id="how-to-use">How to Make AI Use It</h2>

After putting DESIGN.md in your work folder, just say:

```text
Read DESIGN.md first, then use Kami to turn this content into a one-pager. Before starting, tell me which design constraints you'll follow.
```

Or:

```text
Read DESIGN.md first, then use SorryCode Image2 to generate a product poster. Keep the existing project style and save to outputs/images/poster/.
```

<h2 id="relationship">How It Relates to Skills</h2>

Skills tell AI how to do a type of task, like image generation, document layout, or web-style presentations.

DESIGN.md tells AI what this project should look like.

Used together, division is clear: skills provide workflow, DESIGN.md provides style boundaries.

<h2 id="not-perfect">DESIGN.md Is Not Perfect</h2>

Important to understand:

- AI is not a designer, **it misreads, misunderstands, and misorders priorities**
- DESIGN.md is just "read once each time," not "permanently remember"
- If your requirements are complex, AI may only remember part

Therefore:

- ✅ Write core visual rules clearly
- ✅ Use Do / Don't to clarify boundaries
- ✅ Before important tasks, explicitly remind AI: "Read DESIGN.md first"
- ❌ Don't expect AI to perfectly reproduce Figma designs
- ❌ Don't write temporary thoughts into DESIGN.md

<h2 id="references">References</h2>

- Google Labs `design.md`: <https://github.com/google-labs-code/design.md>
- Open Design `DESIGN.md` examples: <https://github.com/VoltAgent/awesome-design-md>

<h2 id="next">What's Next</h2>

**If you want to use DESIGN.md to generate images, PPT, web pages:**

- See [Skills / Featured Skills](/docs/skills/featured-skills) to find suitable skills
- Or see [Tools / Open Design](/docs/tools/open-design) for complete design workbench

**If you want AI to remember project development rules:**

- See [Make AI Remember Project Rules](/docs/agent-memory/remember-rules)
