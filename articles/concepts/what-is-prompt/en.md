---
title: "Talking to AI Is Not Spellcasting"
slug: what-is-prompt
order: 4
summary: The internet is full of "god-tier prompt templates," making it seem like you need to learn a new language to talk to AI. The truth: a prompt is just a work order — be clear about what you want, what you don't want, what "done" looks like, and the background context. Good prompts are iterated, not written in one shot.
section: concepts
section_title: Core Concepts
section_order: 5
---

# Talking to AI Is Not Spellcasting

A particular genre of content is wildly popular online:

```text
"10 god-tier prompts you need!"
"This prompt will 10x your AI output!"
"Bookmark this: the ultimate prompt template collection!"
```

It makes it seem like talking to AI requires learning a new language — memorizing incantations like a wizard.

It doesn't.

<h2 id="what-it-is">A Prompt Is Just a Work Order</h2>

Think about how you assign a task to a colleague.

You don't say "make a good report." You say:

```text
"Can you pull together this month's sales data?
Break it down by product line, calculate month-over-month growth,
and flag any anomalies in red. On my desk by end of day tomorrow."
```

Three sentences. Four pieces of critical information:

```text
1. What to do: compile sales data, categorize by product, calculate growth
2. How to do it: flag anomalies in red
3. What "done" looks like: on my desk by tomorrow
4. Background context: this month, sales data (they know where to find it)
```

Instructions to AI follow the exact same structure.

```text
Good Prompt = Task + Boundaries + Success Criteria + Background
```

Those "god-tier prompts" online look long and complex not because AI needs complexity. It's because the person who wrote them included all the background, boundaries, and success criteria explicitly.

You can do the same.

<h2 id="four-parts">The Four Elements</h2>

Break any task into four parts, and your prompt won't miss the mark:

**1. Task description — what I want**

Be as specific as possible. Not "write me a report," but "write a quarterly summary under 500 words, for my department director."

**2. Boundaries — what I don't want**

Telling AI what NOT to do is often more useful than telling it what to do.

For example: "Don't use technical jargon — this is for the sales team. Keep it under one page. Don't mention competitor names."

**3. Success criteria — what "done" looks like**

AI doesn't know when it's "finished." Tell it: what format, what length, which sections to include.

For example: "Output as a Markdown file with three sections: performance overview, problem analysis, next quarter plan."

**4. Background context — what you need to know**

AI has no common sense. It doesn't know your context. It can only work with the information you give it.

For example: "We targeted 5 million last quarter and achieved 4.2 million. The main reason was a key client delaying their contract in March. The team has 8 people."

```text
You don't need to fill all four for every prompt.
But when AI's response misses the mark,
check yourself — which of the four did you skip?
```

<h2 id="examples">Two Examples, Side by Side</h2>

**Vague instruction:**

```text
Write me a product intro.
```

AI doesn't know what your product is, who it's for, how long, what style. It guesses. The guess is probably not what you wanted.

**Clear instruction:**

```text
Write a product intro. The product is an industrial stainless steel valve, targeted at factory purchasing managers. Under 300 words. Don't just list technical specs — explain what the customer saves. Don't mention pricing. Plain text, no tables.
```

The difference: the first one will need five rounds of corrections. The second one might hit the mark on the first try.

<h2 id="iterate">Good Prompts Are Iterated, Not Written</h2>

This is the most important mindset shift.

```text
Don't expect to write the perfect prompt on your first attempt.
Version 1 of a prompt = starting the conversation, not the final command.
```

When you assign a task to a new employee, the first explanation rarely lands perfectly. They might misunderstand. You clarify: "No, what I meant was..." They adjust. After a round or two, you're aligned.

AI works the same way.

Round one: you give a rough outline. It produces a draft.

Round two: you say "this part is wrong, change it to..." It adjusts.

Round three: you say "good, now adjust the overall tone..." It adjusts again.

After three rounds, what you get is usually better than anything you could have produced with a single perfect prompt.

```text
Good prompts are iterated.
You don't need to get it right in one shot.
You just need to say "what's wrong" after each response.
```

This is why [How Agent Works](/docs/concepts/what-is-agent) emphasizes the "command → plan → feedback → iterate" loop — it's the same principle as writing prompts.

<h2 id="not-magic">Why "God-Tier Prompts" Stop Working</h2>

You may have experienced this: you copy a supposedly amazing prompt from the internet, and AI's response is completely off.

The reason: **a prompt's effectiveness depends on context.**

Same prompt, different AI model, different background, different task scenario — completely different result.

A prompt designed for writing ad copy won't help you find a code bug.

An English prompt translated directly into Chinese might work differently — because the model's training data has different distributions across languages.

```text
Learn from other people's prompts, but don't copy them.
You know your task, your audience, and your standards
better than anyone else.
Your prompt should work better than any template.
```

<h2 id="for-real-people">Three Scenarios for People Who Don't Code</h2>

You're not a programmer, but you'll likely encounter these scenarios:

**Scenario 1: Writing documents**

```text
Write meeting minutes.
Topic: Q2 sales strategy adjustment
Attendees: Sales director, three regional managers
Key conclusions: North China needs more headcount. South China's price-cut strategy isn't working — discontinue.
Format: four sections — Background, Discussion, Conclusions, Next Steps — each under 200 words.
Don't use AI-generated clichés. Make it read like a human wrote it.
```

**Scenario 2: Organizing information**

```text
Below is a transcript from an interview recording. Organize it into three parts:
1. Key points (no more than 5)
2. Questions worth following up on (no more than 3)
3. One-sentence summary
Don't add information not present in the original. Don't evaluate whether the views are correct.
[paste text]
```

**Scenario 3: Writing PPT content**

```text
Write an outline for a PowerPoint deck.
Title: 2025 H1 Production Department Review
Audience: Plant manager and department heads
Duration: 15 minutes
Must include: output data, quality issues, equipment maintenance, H2 plan
Bullet points only per slide, no full sentences. No more than 12 slides total.
Avoid buzzwords and corporate jargon.
```

These three examples share one trait: none of them are one-sentence commands. Each includes the task, boundaries, success criteria, and background.

But you don't need to memorize a format. You just need to ask yourself each time:

```text
Does AI know what I want?
Does AI know what "done" looks like?
Does AI know what NOT to do?
Does AI have enough background information?
```

<h2 id="remember">Remember One Thing</h2>

```text
A prompt isn't a magic spell. It's a work order.
You don't need to learn a new language.
You just need to write down what you'd say
when assigning a task to a colleague.
```

<h2 id="next">Next Step</h2>

Now you know how to give AI clear instructions. But there's another problem:

Why do even clear instructions sometimes fail after a long conversation?

The answer is in the next chapter: [How to Manage AI's Memory](/docs/concepts/what-is-context)

If you want to practice right now: [Village / Edit Your First File](/docs/village/edit-first-file)
