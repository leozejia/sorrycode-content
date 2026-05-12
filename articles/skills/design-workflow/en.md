---
title: How to Use Design Skills
slug: design-workflow
order: 2
summary: Design, decks, images, and writing usually need iteration. Use skills to create an editable first draft, then guide the agent with specific feedback.
section: skills
section_title: Skills
section_order: 15
---

# How to Use Design Skills

Design skills help you move from a blank page to a usable first draft, then make the next revisions easier to direct.

Decks, images, writing, one-pagers, covers, and product visuals rarely become final after one prompt. They usually need adjustment based on audience, context, brand, reading format, and personal preference. That does not mean the skill failed. It is a normal part of design work.

The clearer your feedback is, the easier it is for the agent to revise in the right direction.

<h2 id="what-it-solves">What It Solves First</h2>

The hard part of design work is often not drawing or layout. It is getting from a vague request to something concrete enough to discuss.

A skill helps by:

1. getting you started without a blank page
2. giving the agent a stable process, such as asking questions, proposing a route, and saving files
3. producing a version you can react to
4. keeping revisions local instead of rebuilding everything each time
5. turning repeated preferences into long-lived rules

So the first result is not always the endpoint. More often, it is the first useful version you can judge and improve.

<h2 id="why-iterate">Why Iteration Is Normal</h2>

The same content can need different design choices in different contexts.

| Context | What tends to matter more |
| --- | --- |
| Projected talk | Type size, contrast, and page rhythm |
| Client reading | Structure, credibility, and completeness |
| Social cover | First-glance recognition and title clarity |
| Internal report | Restraint, accuracy, and scanability |
| Personal portfolio | Memorability and expressive tone |

If that context is missing, the agent can only create a reasonable default. Iteration moves the result from “usable by default” toward “right for this situation.”

<h2 id="three-feedback-types">Split Feedback Into Three Types</h2>

When something feels wrong, split the feedback first.

| Type | Examples | How to respond |
| --- | --- | --- |
| Quality issue | Text is too small, contrast is weak, image is blurry, layout overflows, export fails | Point to the issue and ask the agent to make it usable |
| Context issue | Wrong for projection, wrong for clients, wrong for sales, off-brand | Add audience, occasion, brand, and delivery constraints |
| Preference issue | You want it simpler, more restrained, more striking, closer to a reference | Give a direction or reference; turn repeated preferences into rules |

This is more useful than saying “the style is bad.” The agent does not have to guess what you care about. It can revise based on the type of problem.

<h2 id="how-to-iterate">How to Iterate Faster</h2>

Narrow the scope first, then state the standard. Many revisions do not need a full rebuild.

```text
Do not rebuild the whole deck. Only revise slides 3-6:
1. Increase type size until it is readable on a projector
2. Keep the current structure
3. Reduce decorative elements
4. Shift the style from editorial to more restrained and business-like
5. After editing, list which slides changed
```

If you are not sure what is wrong yet, ask the agent to review first.

```text
Do not edit yet. Review this deck and split the issues into:
1. Quality issues
2. Context issues
3. Preference issues

List only the top 3 issues in each group, then ask me which group to fix first.
```

<h2 id="choose-path">Choose the Route Before the Tool</h2>

For design work, start with the deliverable, then choose the skill or tool.

| Deliverable | Start with |
| --- | --- |
| Covers, posters, illustrations, product visuals | [SorryCode Image2](/docs/skills/sorrycode-image2) |
| One-pagers, resumes, reports, white papers, portfolios | [Kami](/docs/skills/kami) |
| Web-style presentation decks with a clear visual direction | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |
| App prototypes, motion, infographics, design variants, expert critique | [Huashu Design](/docs/skills/huashu-design) |
| Editing an existing PowerPoint file | [PPTX](/docs/skills/pptx) |
| Code-based, maintainable, reviewable decks | [Tools / Open Slide](/docs/tools/open-slide) |

If this is your first presentation attempt, use [Village / Make a Sharing Deck](/docs/village/share-ppt). It gives you a default path without asking you to compare every tool first.

<h2 id="make-it-yours">Write Down Stable Preferences</h2>

If you keep asking for similar revisions, turn them into long-lived rules:

- Type must be readable on a projector
- Avoid heavy gradients
- Do not make it look like a marketing poster
- Chinese headings need more breathing room
- The deck should feel closer to a consulting report
- Every cover should keep a specific brand color

The lightest version is a `DESIGN.md`. It can store brand colors, fonts, references, banned styles, delivery formats, and acceptance criteria. Next: [Agent Infrastructure / DESIGN.md](/docs/agent-infra/design-md).

If you use the same workflow repeatedly, consider turning it into your own skill. Next time, you can name that skill and let the agent start with your method.

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
