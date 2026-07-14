---
title: First Time Using SorryCode
slug: first-step
order: 1
summary: Create an API key, choose and install a workbench, run your first task — three steps to get started with SorryCode, under 10 minutes from signup to AI doing real work.
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

Not sure if this fits you? [Who SorryCode Is For](/docs/start/who-is-sorrycode-for). Want to understand costs? [How AI Cost Works](/docs/start/ai-cost-basics).

<h2 id="step-1">Step 1: Create an API Key</h2>

An API Key is your access card. Without it, tools cannot reach SorryCode.

1. Go to [sorrycode.com/keys](https://sorrycode.com/keys)
2. Click "Create API Key"
3. Name it after the tool you'll use, like "Codex" or "Claude Code"
4. Select "Default Group"
5. Leave other options as default
6. Click create, copy the string starting with `sk-...`

**Keys display only once. Copy and save it now.**

Recommend creating separate keys for Codex and Claude Code. Balance is shared, but records are separate for easier management and troubleshooting.

If you hit issues during creation, see [Create API Key](/docs/start/create-api-key) for detailed instructions.

<h2 id="step-2">Step 2: Choose and Install a Workbench</h2>

A workbench is where AI does work on your computer. It reads files, writes files, executes commands, and calls tools.

### Which Workbench?

SorryCode supports two mainstream workbenches:

| Workbench | Good For | Where to Go |
|-----------|----------|-------------|
| **Codex** | Mainly use GPT models, or not sure | [Install Codex](/docs/runtime/codex) |
| **Claude Code** | Mainly use Claude models | [Install Claude Code](/docs/runtime/claude-code) |

**Not sure? Install Codex.** It's the simplest entry point for beginners, has a visual app, and also supports command line.

### Quick Install

Both workbenches support one-click installation:

1. Return to `https://sorrycode.com/keys`
2. Find the key you just created, click `Connect Tool` on the right
3. In the popup, select `Codex` or `Claude Code`, then select your system
4. The copied command already includes your current API Key

Then open your computer's terminal:

- Mac: Press `Command + Space`, type `Terminal`, press Enter
- Windows: Press `Win`, type `PowerShell` or `Terminal`, press Enter

Paste the entire copied command and press Enter.

**After installation:**

- **Codex users:** Download and open [Codex App](https://developers.openai.com/codex/app), or type `codex` command in terminal
- **Claude Code users:** Type `claude` command in terminal to start

### Detailed Installation and Usage Guides

If one-click installation hits issues, or you want to learn more:

- **Codex users:** See [Runtime / Codex](/docs/runtime/codex)
  - Includes: installation, starting Codex App, command line usage, plugin configuration
- **Claude Code users:** See [Runtime / Claude Code](/docs/runtime/claude-code)
  - Includes: installation, command line usage, plugin configuration

**Windows users note:** If installation prompts permission issues, first see [Windows PowerShell](/docs/environment/windows-powershell).

<h2 id="step-3">Step 3: Start the Workbench and Run Your First Task</h2>

Installation complete. Now make it work.

### Start the Workbench

**Codex users:**

Method 1 (recommended for beginners):
1. Open Codex App
2. Select your project folder
3. Type task in the input box

Method 2 (command line):
1. Navigate to project folder in terminal
2. Type `codex` to start
3. Enter task

**Claude Code users:**

1. Navigate to project folder in terminal
2. Type `claude` to start
3. Enter task

### First Task

Don't start by having it modify important files. Run a small task to verify everything works.

**If you have a code project:**

```text
Don't change code yet. Look at this project and tell me what it does and which files I should read first.
```

**If you don't have a code project:**

Create an "AI Workspace" folder on your desktop, enter it, start the workbench, then say:

```text
Help me write a personal introduction draft in this folder. Ask me 5 necessary questions first, don't generate the final version directly.
```

**If you want to generate images:**

Say this directly in Codex App:

```text
Generate a clean warm podcast cover about AI coding for beginners. Keep the layout simple and leave enough room for a title.
```

Use [Skills / SorryCode Image2](/docs/skills/sorrycode-image2) only when you need to edit a local image, choose an output folder, or save generation diagnostics.

**Task completed?** You're already ahead of 90% of users.

<h2 id="step-4">Step 4: Expand by Task</h2>

Some tasks work directly in a Codex App conversation, while others need a Skill. Skill install commands can change with Codex, Claude Code, and upstream repositories, so this starter page does not keep a fixed command list.

| What You Want | Start Here |
| --- | --- |
| Handle Word / Excel / PPT / PDF | [Office Docs](/docs/skills/office-docs) |
| Make one-pagers, resumes, portfolios, long documents | [Kami](/docs/skills/kami) |
| Generate images, posters, covers | [GPT Image 2](/docs/runtime/gpt-image-2) |
| Make web-based slide decks | [Guizang PPT Skill](/docs/skills/magazine-web-ppt) |

Open the matching page and follow its default path. Only choose a Codex or Claude Code install command when the task actually needs a Skill. Restart the workbench after installing skills.

More skills at [Skills / Featured Skills](/docs/skills/featured-skills).

<h2 id="common-issues">Common Issues</h2>

### Command Not Found After Installation

**Codex:**
- Check if installed: `which codex`
- If not, re-run one-click install command
- Or just use Codex App (no command line needed)

**Claude Code:**
- Check if installed: `which claude`
- If not, re-run one-click install command

### API Key Error

Check:
1. Did you correctly copy the complete key starting with `sk-...`
2. Does your account have available balance
3. Was the key correctly configured during installation

Detailed troubleshooting: [Codex Common Issues](/docs/runtime/codex#common-issues) or [Claude Code Common Issues](/docs/runtime/claude-code#common-issues).

### Not Sure Whether to Use Codex or Claude Code

- **Use GPT models (like GPT-4, o1):** Use Codex
- **Use Claude models (like Claude 3.5 Sonnet):** Use Claude Code
- **Not sure:** Install Codex, it's more beginner-friendly

You can install both — they can coexist.

<h2 id="what-next">What Next</h2>

Follow your goal:

### Want to Learn Workbenches In-Depth

- Codex users: [Runtime / Codex](/docs/runtime/codex)
  - Learn Codex App usage, plugin management, command line tips
- Claude Code users: [Runtime / Claude Code](/docs/runtime/claude-code)
  - Learn command line usage, plugin management, advanced features

### Want to Understand Plugins and Skills

- [Plugins vs Skills - What's the Difference](/docs/runtime/plugins-vs-skills)
  - Plugins provide tools, Skills teach methods
- [Skills / Featured Skills](/docs/skills/featured-skills)
  - Browse all available Skills

### Want Systematic Learning

- [Core Concepts / What AI Actually Is](/docs/concepts/what-is-ai) - Understand AI from scratch
- [Make AI Remember](/docs/agent-memory/overview) - Long-term context management
- [How AI Cost Works](/docs/start/ai-cost-basics) - Understand billing

### Hit Issues

- [Codex Documentation](/docs/runtime/codex) - Complete Codex guide
- [Claude Code Documentation](/docs/runtime/claude-code) - Complete Claude Code guide
- [Troubleshoot / Common Errors](/docs/troubleshoot/common-errors) - General troubleshooting

<h2 id="remember">All You Need to Remember</h2>

- **API Key** = your access card — create it, copy it, save it
- **Codex / Claude Code** = workbenches — pick one and install
- **Codex App** or `codex` / `claude` command starts the workbench
- **Skills** = capability packs — install what your task needs
- Completing one small task beats reading ten tutorials

**Stuck?** Go directly to the detailed guide for your workbench:
- [Codex Complete Guide](/docs/runtime/codex)
- [Claude Code Complete Guide](/docs/runtime/claude-code)
