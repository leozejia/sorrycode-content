---
title: How AI Remembers What You Said
slug: overview
order: 1
summary: Tired of repeating yourself? Three ways to make AI remember your work style, design preferences, and project rules long-term.
section: agent-memory
section_title: Make AI Remember
section_order: 15
---

# How AI Remembers What You Said

After using AI for a while, the real problem is usually not "can it answer."

The real problems are:

```text
Sessions get too long
You repeat project rules every time
Context is lost when switching tools
Design style changes every time
Repeating the same requirements
```

This page teaches you how to make AI remember your requirements long-term.

<h2 id="three-ways">Three Types of "Memory"</h2>

AI can remember what you said in three ways:

### 1. Session Memory (Short-term)

**What it is:**  
Everything in the current conversation. Every message you send, every AI response, lives in this session's memory.

**Good for:**  
- Temporary tasks
- Context specific to this session
- Information you don't need next time

**Problems:**  
- Sessions get longer and more expensive
- Lost after closing
- Switching tools or starting a new session forgets everything

**How to manage:**  
See [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management)

---

### 2. File Memory (Long-term)

**What it is:**  
Write requirements into files and put them in your work folder. AI reads these files every time it enters.

**Good for:**  
- Long-term unchanging rules
- Requirements you want followed every time
- Context shared across sessions and tools

**Common files:**

| File | Purpose | Where to learn |
|------|---------|----------------|
| `AGENTS.md` / `CLAUDE.md` | Make AI remember project rules: which files not to change, what commands to use, what rules to follow | [Make AI Remember Project Rules](/docs/agent-memory/remember-rules) |
| `DESIGN.md` | Make AI remember design style: brand colors, fonts, components, visual style | [Make AI Remember Your Design Style](/docs/agent-memory/remember-design) |

**Benefits:**  
- Write once, works long-term
- Works across tools and sessions
- Can be shared with teams

---

### 3. Skill Memory (Reusable)

**What it is:**  
Turn repetitive workflows into Skills, teaching AI how to do specific types of tasks.

**Good for:**  
- Repeated tasks (generating images, code review, document layout)
- Work requiring stable processes
- Capabilities you want to reuse across projects

**How to do it:**  
See [Make AI Remember Work Methods](/docs/agent-memory/remember-skills)

---

<h2 id="when-to-use">When to Use Which</h2>

| Scenario | Use What |
|----------|----------|
| Temporary task, session-specific | Just say it, no need for files |
| Long-term rules, need to follow every time | Write `AGENTS.md` or `DESIGN.md` |
| Repetitive work, want standardization | Make it a Skill |
| Session too long, context exploded | See [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management) |

<h2 id="mental-model">Understand with One Diagram</h2>

```text
┌─────────────────────────────────────────┐
│     Current Session (Short-term)         │
│   "Make me a poster with Spring Festival │
│    theme this time"                      │
│   → Forgotten after closing              │
└─────────────────────────────────────────┘
           ↓ reads
┌─────────────────────────────────────────┐
│       File Memory (Long-term)            │
│   DESIGN.md: "Brand color is ink blue,   │
│               restrained style"          │
│   AGENTS.md: "Don't change config/ dir"  │
│   → Read every session                   │
└─────────────────────────────────────────┘
           ↓ invokes
┌─────────────────────────────────────────┐
│      Skill Memory (Work Methods)         │
│   SorryCode Image2: "How to generate     │
│                      images"             │
│   Waza: "How to review code"             │
│   → Triggered when needed                │
└─────────────────────────────────────────┘
```

<h2 id="quick-start">Quick Start</h2>

**If this is your first time learning these concepts, start here:**

### Step 1: Solve Your Current Problem

- Session too long? → [What to Do When Sessions Get Too Long](/docs/agent-memory/context-management)
- Repeating project rules every time? → [Make AI Remember Project Rules](/docs/agent-memory/remember-rules)
- Generated designs have inconsistent styles? → [Make AI Remember Your Design Style](/docs/agent-memory/remember-design)

### Step 2: Replace Verbal Explanations with Files

When you find yourself repeatedly explaining the same rules:

1. Create a new file (AGENTS.md or DESIGN.md)
2. Write those rules into it
3. Next time just say: "Read AGENTS.md first, then start"

### Step 3: Turn Repetitive Work into Skills

When you find yourself repeatedly doing the same type of task:

1. Find an existing Skill (see [Skills / Featured Skills](/docs/skills/featured-skills))
2. Or make your own (see [Make AI Remember Work Methods](/docs/agent-memory/remember-skills))

<h2 id="not-perfect">AI Memory Is Not Perfect</h2>

Important to understand:

- AI is not a database, **it forgets, misreads, and misorders priorities**
- File memory is just "read it once each time," not "permanently engraved"
- When sessions get too long, early content is forgotten or downweighted

Therefore:

- ✅ Write important rules into AGENTS.md / DESIGN.md
- ✅ Regularly clean up sessions, remove irrelevant content
- ✅ Before important tasks, explicitly remind AI: "Read DESIGN.md first"
- ❌ Don't expect AI to remember every detail
- ❌ Don't write temporary state into long-term files

<h2 id="next">What's Next</h2>

**If you're not sure where to start, read this first:**

[What to Do When Sessions Get Too Long](/docs/agent-memory/context-management)

Because whether you use Codex, Claude Code, or another agent runtime, you'll encounter the same question:

```text
Which content should stay for the agent?
Which content should be cleared?
```

**If you already understand session management, read next:**

- Developers → [Make AI Remember Project Rules](/docs/agent-memory/remember-rules)
- Designers → [Make AI Remember Your Design Style](/docs/agent-memory/remember-design)
- Want to make your own Skill → [Make AI Remember Work Methods](/docs/agent-memory/remember-skills)
