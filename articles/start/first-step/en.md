---
title: First Time Using SorryCode
slug: first-step
order: 1
summary: First time using SorryCode? Decide whether it fits you, create API keys by tool, then choose Codex, Claude Code, Skills, or another entry.
section: start
section_title: Getting Started
section_order: 1
---

# First Time Using SorryCode

You probably did not come to SorryCode to study APIs or memorize model names.

You likely want AI to help you finish something concrete: understand a project, edit a file, generate an image, organize an article, make slides, or turn an idea into a usable plan.

SorryCode connects those tools to models.

Use this first mental model:

```text
one balance + separate API keys by tool + multiple AI tool entries
```

You create keys here, give them to `Codex`, `Claude Code`, or a `Skill`, and those tools can call models using your SorryCode balance.

That kind of key is called an `API Key`. It usually starts with `sk-...`. You can think of it like an access card: without it, the tool cannot enter SorryCode; with it, the tool can start working.

If you use both Codex and Claude Code, create separate API keys for them. The balance is still shared, but usage records, group switching, spending limits, and troubleshooting become clearer.

If you are not sure whether SorryCode fits you, start with [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for).

<h2 id="three-words">Understand Three Words First</h2>

You do not need the full concept stack on day one. Start with this:

| Word | Beginner meaning |
| --- | --- |
| `API` | the channel tools use to talk to models |
| `API Key` | the key proving this is your account using the channel |
| `SorryCode` | where you create the key, manage balance, and connect tools to models |

When you chat with AI in a browser, you type into a web page.

Tools like `Codex`, `Claude Code`, and `Skills` do not click web pages like humans do. They need a software-to-software way to request a model. That way is called an `API`.

As a beginner, you do not need to write API requests first. Create an API key, give it to the tool, and let the agent handle the rest.

<h2 id="runtime-skills">Workbenches and Capability Packs</h2>

You can think of `Codex` and `Claude Code` as AI workbenches. The model does the thinking; the workbench reads files, edits files, runs commands, and keeps working on a task.

`Skills` are capability packs installed into the workbench. An image skill, office document skill, or slide skill tells the agent what process to follow, which tools to use, and where to save the result.

So the beginner path is:

```text
Create an API key → Install one workbench → Install the Skill for your task
```

<h2 id="step-1">Step 1: Create an API Key</h2>

Do this first:

1. Open `API Keys` in the console
2. Create a new `sk-...` key for the tool you are setting up
3. Copy it and keep it nearby

If you cannot find the page, open: `https://sorrycode.com/keys`

The detailed guide is [Platform / Create API Key](/docs/platform/create-api-key). You do not need to read all of it first; just create the `sk-...` key you need.

<h2 id="step-2">Step 2: Choose Your Entry</h2>

Different goals have different first steps:

| What you want to do | Start here |
| --- | --- |
| Decide whether SorryCode fits you | [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for) |
| Understand where AI cost comes from | [Platform / How AI Cost Works](/docs/platform/ai-cost-basics) |
| Ask AI to read projects, edit files, and run commands | [Runtime / Codex](/docs/runtime/codex) |
| Use the Claude path for project work | [Runtime / Claude Code](/docs/runtime/claude-code) |
| Generate or edit images | Install a runtime first, then read [Skills / SorryCode Image2](/docs/skills/sorrycode-image2) |
| Work with Word, Excel, PowerPoint, or PDF | Install a runtime first, then read [Skills / Office Docs](/docs/skills/office-docs) |
| Write direct HTTP requests | [Platform / First Request](/docs/platform/create-api-key) |
| Use a more visual file and diff workspace | [Tools / VS Code](/docs/tools/vscode) |

If you have no idea what to choose, start with `Codex`. It is the most direct beginner entry for the GPT path.

<h2 id="step-3">Step 3: Match Tools and Models</h2>

`Codex` and `Claude Code` are not models. They are workbenches. `GPT` and `Claude` are models.

Beginner default:

```text
Use GPT models through Codex first.
```

```text
Use Claude models through Claude Code first.
```

Do not chase a new model name by putting it into a random workbench. It may run, but cache behavior and API usage may become inefficient.

For details, read [Platform / Tools Are Not Models](/docs/concepts/tools-models-platform).

<h2 id="step-4">Step 4: Install for Your Computer</h2>

This page does not copy install commands. Install commands live on the runtime pages so you do not copy an outdated version.

Continue based on your choice:

- GPT / Codex path: [Runtime / Codex](/docs/runtime/codex)
- Claude Code path: [Runtime / Claude Code](/docs/runtime/claude-code)
- Windows terminal help: [Environment / Windows PowerShell](/docs/environment/windows-powershell)
- Manual Node.js setup: [Environment / Node.js](/docs/environment/nodejs)

<h2 id="step-5">Step 5: Run One Small Task</h2>

After installation, do not start with a large change. Use a small task to confirm the agent can work.

If you have a code project, copy this:

```text
Do not change code yet. Look at this project and tell me what it does, and which files I should read first.
```

If you do not have a code project, create an `AI Workspace` folder on your desktop and copy this:

```text
Help me draft a personal intro in the current folder. Ask me five necessary questions first. Do not generate the final version yet.
```

If you want to generate an image, install [Skills / SorryCode Image2](/docs/skills/sorrycode-image2) first, then copy this:

```text
Use SorryCode Image2 to generate a clean warm Chinese podcast cover about AI coding for beginners. Check the API key first; if it is missing, tell me how to set it.
```

<h2 id="what-next">What to Do Next</h2>

Choose by goal:

- Read a project: [Village / Read a Project](/docs/runtime/codex)
- Edit the first file: [Village / Edit Your First File](/docs/runtime/codex)
- Generate an image: [Village / Generate Your First Image](/docs/skills/sorrycode-image2)
- Make a product intro: [Village / Product Intro](/docs/skills/kami)
- Work with office files: [Skills / Office Docs](/docs/skills/office-docs)
- Decide whether SorryCode fits you: [Platform / Who SorryCode Is For](/docs/platform/who-is-sorrycode-for)
- Understand AI cost: [Platform / How AI Cost Works](/docs/platform/ai-cost-basics)
- Understand tools and models: [Platform / Tools Are Not Models](/docs/concepts/tools-models-platform)
- Understand `AGENTS.md / CLAUDE.md / DESIGN.md / MCP / Skills`: [Agent Infrastructure](/docs/agent-infra/overview)

<h2 id="remember">Remember These</h2>

- `API` is the channel
- `API Key` is the key
- `Codex / Claude Code` are workbenches
- `Skills` are capability packs
- `SorryCode` connects these tools to models through one balance
