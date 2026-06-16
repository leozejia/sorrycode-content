---
title: First Time Using SorryCode
slug: first-step
order: 1
summary: Create an API key, install a workbench, and run your first task — three steps to get started with SorryCode, under 10 minutes from signup to AI doing real work.
section: start
section_title: Getting Started
section_order: 1
---

# First Time Using SorryCode

This page does one thing: gets you from "never heard of SorryCode" to "AI just finished your first task" in under 10 minutes.

<h2 id="before">Before You Start</h2>

You need a SorryCode account. If you do not have one, sign up at [sorrycode.com](https://sorrycode.com).

SorryCode is an API platform. You top up a balance here, create keys, and hand those keys to AI tools. The tools then call models using your balance.

The mental model:

```text
one balance + separate API keys by tool + multiple AI tool entries
```

Not sure if this fits you? [Who SorryCode Is For](/docs/platform/who-is-sorrycode-for). Want to understand pricing? [How AI Cost Works](/docs/platform/ai-cost-basics).

<h2 id="step-1">Step 1: Create an API Key</h2>

An API key is your access card. Without it, tools cannot enter SorryCode.

1. Open [sorrycode.com/keys](https://sorrycode.com/keys)
2. Click "Create API Key"
3. Name it after the tool you are setting up, e.g. "Codex" or "Claude Code"
4. Set the group to "Default"
5. Leave the rest as default, click create
6. Copy the string that starts with `sk-...`

**The key is shown only once. Copy and save it now.**

Create separate keys for Codex and Claude Code if you use both. The balance is shared, but separate keys keep usage records and troubleshooting clearer.

If you run into issues, see [Create API Key](/docs/platform/create-api-key) for the detailed guide.

<h2 id="step-2">Step 2: Install a Workbench</h2>

A workbench is where AI does work on your computer. It reads files, writes files, runs commands, and calls tools.

**Which one?**

```text
You primarily use GPT models → install Codex
You primarily use Claude models → install Claude Code
Not sure → install Codex, the simplest beginner entry
```

**How to install:**

Go back to `https://sorrycode.com/keys`, find the key you just created, and click `Connect Tool`.

In the modal, choose `Codex` or `Claude Code`, then choose your operating system. The copied command already includes the current API key.

Then open the terminal on your own computer:

- Mac: press `Command + Space`, type `Terminal`, then press Enter
- Windows: press `Win`, type `PowerShell` or `Terminal`, then press Enter

Paste the full command you copied and press Enter. When the installer finishes, the workbench is connected.

If the install gets stuck, see the detailed guides for [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code). Windows users: read [Windows PowerShell](/docs/environment/windows-powershell) first.

<h2 id="step-3">Step 3: Run Your First Task</h2>

The workbench is installed. Now make it do something.

Do not start by editing important files. Run a small test first.

**If you have a code project:**

Open the project folder in the terminal, launch the workbench, and copy this:

```text
Do not edit code yet. Look at this project and tell me what it does, and which files I should read first.
```

**If you do not have a code project:**

Create an "AI Workspace" folder on your desktop, open it in the terminal, launch the workbench, and copy this:

```text
Help me draft a personal intro in the current folder. Ask me five necessary questions first. Do not generate the final version yet.
```

**If you want to generate an image:**

Install the image skill first:

```bash
npx skills add linxiverse/sorrycode-image2 -g -y
```

Then say:

```text
Use SorryCode Image2 to generate a clean warm Chinese podcast cover about AI coding for beginners. Check the API key first. If it is missing, tell me how to set it.
```

Task complete? You now know more than 90% of people.

<h2 id="step-4">Step 4: Install the Matching Skill</h2>

A Skill is a capability pack for your workbench. Install the one that matches your task.

| What you want to do | Which Skill | Command |
| --- | --- | --- |
| Work with Word, Excel, PPT, or PDF | Office Docs | `npx skills add linxiverse/office-docs -g -y` |
| Create one-pagers, resumes, portfolios, long docs | Kami | `npx skills add tw93/kami -g -y` |
| Generate images, posters, covers | Image2 | `npx skills add linxiverse/sorrycode-image2 -g -y` |
| Make web-based slide decks | Guizang PPT | `npx skills add op7418/guizang-ppt-skill -g -y` |

More Skills: [What Are Skills](/docs/skills/featured-skills) and [Creation and Design](/docs/skills/creation-design).

<h2 id="what-next">What Next</h2>

Follow your goal:

- Learn AI concepts systematically: start with [Core Concepts](/docs/concepts/what-is-ai)
- Go deeper with agent workflows: [Agent Infrastructure](/docs/agent-infra/overview)
- Understand where your money goes: [How AI Cost Works](/docs/platform/ai-cost-basics)
- Hit an error: check the [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code) guide

<h2 id="remember">All You Need to Remember</h2>

- API Key = your access card — create it, copy it, save it
- Codex / Claude Code = workbenches — one command to install
- Skills = capability packs — install what your task needs
- Completing one small task beats reading ten tutorials
