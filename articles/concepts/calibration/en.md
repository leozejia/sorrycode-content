---
title: "When to Trust AI and When Not To"
slug: calibration
order: 6
summary: The most dangerous thing about AI isn't that it makes mistakes — it's that it looks equally confident whether right or wrong. Build calibration: in domains you know, review AI's output. In domains you don't, cross-check. Never use AI's confidence to judge its correctness. This is the most important skill of the AI era.
section: concepts
section_title: Core Concepts
section_order: 5
---

# When to Trust AI and When Not To

The previous five chapters taught you: what AI is, why it's different now, how Agent works, how to give instructions, and how to manage memory.

But all of this revolves around one assumption: **AI will get things right.**

The problem: sometimes it doesn't. And the real trouble isn't that it's wrong — it's that when it's wrong, it looks exactly as confident as when it's right.

<h2 id="core-problem">The Most Dangerous Thing About AI Isn't That It Makes Mistakes</h2>

Humans make mistakes. AI does too. That's not surprising.

What's strange: when humans are uncertain, they usually show it. Their tone wavers. They use words like "maybe," "probably," "I think." You can hear the uncertainty.

AI doesn't do this.

```text
AI's tone when wrong = AI's tone when right
You cannot judge whether it's stating facts or fabricating by how it sounds.
```

This is one of the most fundamental differences between AI and humans.

Humans know when they're uncertain. AI doesn't. It just continues text — continuing "established fact" and continuing "fabricated content" are, to AI, the exact same operation.

```text
AI's confidence level has zero relationship to AI's correctness.
This is the most important sentence in this entire book.
```

<h2 id="three-rules">Three Rules</h2>

If you can't judge by tone, what do you do?

Three rules.

**Rule 1: In domains you know, you review AI**

You've done your job for ten years. You know it better than AI. This is your home turf.

Let AI produce drafts, organize data, propose approaches. But you make the final call.

```text
In domains you don't know, AI is a tutor.
In domains you do know, AI is an assistant.
```

You're the quality inspector. AI is the operator. You glance at its output and know immediately whether it's right.

**Rule 2: In domains you don't know, cross-check**

AI gives you an answer in an unfamiliar field. It sounds supremely confident. It cites data. It gives specific advice.

Don't take it at face value. Do at least one thing:

```text
Ask another AI the same question.
Where two AIs contradict each other — that's where you can't trust either directly.
```

Or an even simpler method: ask AI to argue against its own conclusion.

```text
"Analyze this problem from the opposite perspective.
If this approach were to fail, what would be the most likely reason?"
```

If AI can produce a reasonable counterargument, its analysis has some depth. If it hedges or dodges — its earlier conclusion was likely just "continuing" a nice-sounding answer, not actually analyzing.

**Rule 3: Never use confidence to judge correctness**

Say it again: AI's confidence has nothing to do with its correctness.

This doesn't mean AI is unreliable or unusable. It means you must treat it differently from how you treat humans.

```text
With humans: hesitant tone → probably uncertain → ask more
With AI: tone is meaningless → check facts and logic → verify yourself
```

<h2 id="spot-failure">How to Spot When AI Is Making Things Up</h2>

A few signals. When you see them, be suspicious.

**Signal 1: Overly specific without a source**

AI says "According to Q3 2023 data on industrial valve shipments in South China, year-over-year growth was 12.7%."

If you didn't give it this data — it's fabricating. AI can't query databases. It can only continue text. When a number is too specific and unsourced, it's probably made up.

**Signal 2: Dodging the core question**

You ask "Between approach A and approach B, which fits our scenario better?" AI responds with a long paragraph, but on closer inspection — it never actually compares them. It says nice things about both.

That's avoidance. It doesn't know how to choose, but it won't say "I don't know."

**Signal 3: Logical gaps**

AI's opening and closing might read smoothly, but the logic in the middle is broken.

For example: "Because costs are rising, we should lower prices." This cause and effect is backwards — rising costs usually mean raising prices, not lowering them. AI may have just stitched "cost" and "price" together as related words, without actually reasoning.

**Signal 4: The answer changes when you rephrase**

This is the most effective detection method.

Take the same question. Ask it again from a different angle. If AI's answer becomes inconsistent — it probably fabricated a plausible-sounding answer the first time.

<h2 id="reasoning-vs-standard">When to Use Reasoning Models</h2>

We covered the difference between reasoning and standard models earlier: one thinks first then speaks, the other thinks while speaking.

The calibration rule extends here:

```text
Standard model: best for tasks where you can tell at a glance whether the output is right.
                Examples: translation, summarization, polishing, draft writing.

Reasoning model: best for tasks where you care whether the answer is genuinely correct.
                 Examples: math, code logic, complex analysis, multi-step reasoning.
```

For everyday writing and conversation, the reasoning model's slowness and cost aren't worth it. But when you need rigorous logic, those extra seconds and tokens are money well spent.

<h2 id="emotional">Admit This: AI Will Intimidate You</h2>

Nearly everyone, the first time they seriously use AI, goes through the same experience:

It's so articulate. It can quote sources. It can write poetry. It can explain quantum mechanics. It seems like it knows everything.

At this point, a thought might creep in: **it's smarter than me.**

This thought is dangerous.

Not because it's false. Because it makes you surrender your judgment.

```text
You're not talking to someone smarter than you.
You're talking to an intern who has read more books than you
but has zero practical experience.
More knowledgeable than you ≠ better judgment than you.
More articulate than you ≠ better thinking than you.
```

You've done your job for ten years. Your industry understanding, your instinct for people, your nose for risk — AI doesn't have these. And won't.

AI is your tool. You are the one using the tool.

```text
A hammer is harder than your hand. You still don't let the hammer decide where to drive the nail.
Similarly, AI being more articulate than you doesn't mean you hand over your judgment.
```

<h2 id="calibration-skill">Calibration Is a Trainable Skill</h2>

It's like learning to drive. At first, you're fumbling — unsure when to brake, when to accelerate. After enough time, your body just knows.

Using AI is the same.

At first, you'll be intimidated. Gradually, you'll start spotting when AI is making things up. Eventually, you'll predict it before it even happens — "this is a domain where it has no data. It's probably going to fabricate."

```text
Calibration isn't knowledge. It's experience.
The more you use it, the sharper your judgment gets.
```

<h2 id="remember">Remember One Thing</h2>

```text
AI will never tell you when it doesn't know.
You have to learn to spot when it's making things up.
Confidence does not equal correctness —
for AI, these two things are completely unrelated.
```

<h2 id="next">Next Step</h2>

You've learned how to manage memory and calibrate your judgment. Now there's one last decision:

**With so many tools and models out there, how do you choose?**

Next chapter: [Tools, Models, Platforms — Stop Confusing Them](/docs/concepts/tools-models-platform)
