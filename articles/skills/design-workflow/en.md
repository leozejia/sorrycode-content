---
title: How to Use Design Skills
slug: design-workflow
order: 2
summary: Design, decks, images, and writing are subjective deliverables. Use skills to create a strong starting point, then iterate with your own judgment instead of expecting one prompt to finish the work.
section: skills
section_title: Skills
section_order: 15
---

# How to Use Design Skills

SorryCode provides methods and tools. It does not define the final taste for you.

Design, decks, images, writing, one-pagers, and covers are subjective deliverables. Different people will disagree: one person thinks the text is too small, another thinks the layout is too empty, one likes an editorial look, another wants a restrained business style.

A design skill is not a one-prompt final-output machine. Its value is to help the agent produce a structured starting point that you can keep shaping. You still own the goal, the audience, the context, the tradeoffs, and the final result.

<h2 id="mindset">Use the Right Mindset</h2>

Do not treat a design skill as an outsourced designer. Do not treat the agent as the final judge of taste.

A better workflow is:

1. You provide the goal, audience, context, assets, and constraints
2. The skill helps the agent create a first draft or route
3. You judge what is wrong
4. The agent revises specific parts based on your feedback
5. Repeated preferences become your own `DESIGN.md`, references, or skill

One prompt can start the work. It should not be expected to finish the work.

<h2 id="three-feedback-types">Split Feedback Into Three Types</h2>

When something feels wrong, first decide what kind of problem it is.

| Type | Examples | What to do |
| --- | --- | --- |
| Quality issue | Text is too small, contrast is weak, image is blurry, layout overflows, export fails | Ask the agent to fix it directly |
| Context issue | Wrong for projection, wrong for executives, wrong for sales, off-brand | Add audience, occasion, and constraints |
| Preference issue | You want it simpler, louder, more editorial, more restrained, closer to a reference | State the direction; turn repeated preferences into rules |

This matters because “the style is bad” is not actionable enough. The agent needs to know whether it failed the quality floor, missed the context, or simply chose a taste direction you do not want.

<h2 id="how-to-iterate">How to Iterate Faster</h2>

Do not restart the whole artifact every time. Narrow the scope and state the standard.

```text
Do not rebuild the whole deck. Only revise slides 3-6:
1. Increase type size until it is readable on a projector
2. Keep the current structure
3. Reduce decorative elements
4. Shift the style from editorial to more restrained and business-like
5. After editing, list which slides changed
```

If you are not sure what is wrong, ask the agent to diagnose first.

```text
Do not edit yet. Review this deck and split the issues into:
1. Quality issues
2. Context issues
3. Preference disagreements

List only the top 3 issues in each group, then ask me which group to fix first.
```

<h2 id="choose-path">Choose the Route Before the Tool</h2>

For design work, do not start with “which skill is strongest?” Start with the deliverable.

| Deliverable | Start with |
| --- | --- |
| Covers, posters, illustrations, product visuals | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| One-pagers, resumes, reports, white papers, portfolios | [Kami](/docs/skills/kami) |
| Web-style presentation decks with a clear visual direction | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |
| App prototypes, motion, infographics, design variants, expert critique | [Huashu Design](/docs/skills/huashu-design) |
| Editing an existing PowerPoint file | [PPTX](/docs/skills/pptx) |
| Code-based, maintainable, reviewable decks | [Tools / Open Slide](/docs/tools/open-slide) |

If this is your first presentation attempt, use [Village / Make a Sharing Deck](/docs/village/share-ppt). It gives you a default path without requiring you to compare every tool first.

<h2 id="make-it-yours">Turn Your Taste Into Rules</h2>

If you keep repeating feedback like this, stop adding it manually every time:

- Type must be readable on a projector
- Avoid heavy gradients
- Do not make it look like a marketing poster
- Chinese headings need more breathing room
- The deck should feel closer to a consulting report
- Every cover must keep a specific brand color

Those are not one-off prompts. They are long-lived rules.

The lightest version is a `DESIGN.md`. It can store brand colors, fonts, references, banned styles, delivery formats, and acceptance criteria. Next: [Agent Infrastructure / DESIGN.md](/docs/agent-infra/design-md).

If you use the same workflow repeatedly, turn it into your own skill. Next time, you can name the skill and let the agent start with your method.

<h2 id="first-prompt">First Prompts</h2>

If you are not sure which skill to use:

```text
I want to create a design deliverable that can be sent to other people. First decide whether I should use SorryCode Image2, Kami, Guizang PPT Skill, PPTX, Huashu Design, or Open Slide. Do not generate yet. Ask me for the goal, audience, context, assets, and style preference first.
```

If you already have a draft:

```text
Review this draft first. Do not rebuild it. Split the problems into quality issues, context issues, and preference issues, then propose the smallest useful revision.
```

If you want to capture your own rules:

```text
Here are my revision notes from several design drafts. Turn them into a DESIGN.md and separate long-lived rules, optional preferences, and task-specific requirements.
```
