---
title: Claude Code
slug: claude-code
order: 1
summary: Understand Claude Code first, prepare your API key, finish one-click install, and start using it right away.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: anthropic
group_title: Anthropic
group_order: 20
---

# Claude Code

If you want a model to read your project, edit code, and run commands locally, this page is the shortest path.

For a first-time user, the main goal is to get the path working. Do not start with config files, and do not assume you need to learn a lot of terminal commands first.

> **Which path?**
>
> **→ One-Click Install (Recommended):** Click `Connect Tool` on the API key page → copy the command → paste it into your computer's terminal → done. For most people.
>
> **→ Manual Install:** Set up Node.js yourself, write config files. For users who want control over each step.
>
> The default flow below follows the one-click path.

<h2 id="what-is-claude-code">What Claude Code Is</h2>

- `Claude Code` is a terminal runtime / agent built for code work
- it can read your project, edit files, run commands, and answer code questions
- on SorryCode, you just point it at `{{ANTHROPIC_BASE_URL}}` and give it your API key

For a first setup, you do not need to understand `settings.json` or env vars up front. One-click install is enough.

Reference: [Claude Code official docs](https://code.claude.com/docs/en/overview)

> Beginner rule: `Claude Code` is a runtime, not a model. It is the default fit for Claude / Anthropic-compatible paths. Do not put `gpt-5.4` into Claude Code just to chase a new GPT model; cache hit rate and API usage can become inefficient. Read [Platform / Tools Are Not Models](/docs/concepts/tools-models-platform).

<h2 id="prepare-api-key">Prepare the API Key First</h2>

The install command needs to be tied to your API key, so do this first:

1. Sign in to the SorryCode console
2. Find `API Keys` inside the console
3. If you do not have one yet, create a new `sk-...`
4. Return to the list and prepare to click `Connect Tool` for that key

The quick link is `https://sorrycode.com/keys`, but the more important thing is knowing where this page sits inside the console.

If you have not done this yet, start with [Platform / Create API Key](/docs/platform/create-api-key).

If you also plan to use Codex, create a separate API key for Codex. Both keys still use the same balance, but usage records, group switching, spending limits, and troubleshooting become clearer.

<h2 id="one-click-install">⚡ One-Click Install (Recommended)</h2>

This is the default path. The console generates an install command for the current API key. Paste that command into the terminal on your own computer, and the installer will connect `Claude Code` to `{{ANTHROPIC_BASE_URL}}` and write the local config. After install, enter your project folder in a terminal and run `claude`.

### Step 1: Copy the Command in the Console

1. Open `https://sorrycode.com/keys`
2. Find the API key you prepared for Claude Code
3. Click `Connect Tool`
4. Choose `Claude Code`
5. Choose your operating system
6. Click `Copy`

The copied command is complete and already includes the current API key.

### Step 2: Paste It into Your Computer's Terminal

- Mac: press `Command + Space`, type `Terminal`, then press Enter
- Windows: press `Win`, type `PowerShell` or `Terminal`, then press Enter

After the terminal opens, paste the full command you copied and press Enter.

The one-click installer handles the dependencies needed for the Claude Code setup path. On macOS, it prepares `Node.js 22 LTS` and `Claude Code`; you do not need to learn Homebrew or Git first. Windows uses the Windows-specific installer. If you are not sure what PowerShell is, read [Environment / Windows PowerShell](/docs/environment/windows-powershell) first.

### Fallback: Copy a Generic Command Manually

If you cannot open the `Connect Tool` modal, use the generic command below. It does not include your API key, so the installer will stop and ask you to paste the `sk-...` value.

macOS / Linux:

```bash
curl -fsSL -o /tmp/sorrycode-claude.sh {{INSTALL_CLAUDE_SH_URL}} && bash /tmp/sorrycode-claude.sh --base-url "{{ANTHROPIC_BASE_URL}}" --source sorrycode-docs
```

Windows:

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-claude.bat {{INSTALL_CLAUDE_BAT_URL}} && %TEMP%\sorrycode-claude.bat --base-url {{ANTHROPIC_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>What the installer does</summary>

- on Windows, checks `Git for Windows`
- installs `Claude Code`
- writes `~/.claude/settings.json`
- writes the API key
- runs one minimal connectivity check
- on Windows, uses `ExecutionPolicy Bypass` only for this install process and does not permanently loosen your PowerShell policy

</details>

If you copied the command from `Connect Tool`, the installer usually does not need to ask for the API key again. If you use the generic command above, the installer blocks until you provide an `sk-...` key.

If the last step says the connectivity check failed, that does not always mean the install failed. Balance, permissions, or upstream network issues can still break the remote check even when the local install is already done.

<h2 id="start-claude-code">How to Start After Install</h2>

This one-click installer configures `Claude Code` only. It does not configure `Claude Desktop`.

If you want the model to read local projects, edit code, and run commands, enter your project folder and run:

```bash
claude
```

If you want to use Claude's graphical chat interface while sending requests through SorryCode, configure Claude Desktop's third-party inference gateway separately. Read [Runtime / Claude Desktop](/docs/runtime/claude-desktop) next.

If you prefer viewing project files and changes inside a visual editor, continue with [Tools / VS Code](/docs/tools/vscode).

<h2 id="first-prompt">What to Say First</h2>

Do not start with a huge refactor request. Use a safer first prompt:

```text
Look at this project structure first, then tell me which files I should read first.
```

Or:

```text
Do not change code yet. Explain what this project does and where the entry point is.
```

This confirms two things early:

- the runtime opened the correct project folder
- it can read the project and respond normally

<h2 id="install-skills-with-agent">Next: Let Claude Code Manage Skills</h2>

After Claude Code is running, you do not need to study `npx`, `Git`, or `Homebrew` yourself. Paste this into Claude Code and let it read the current SorryCode Skills docs, prepare the environment, and install, list, or remove the skills you need:

```text
Read the current SorryCode Skills entry first: https://sorrycode.com/docs/skills/featured-skills.md?locale=en. Assume my Mac has no development environment prepared. Check and prepare the required environment first, then decide which skills to install based on the current Skills docs, their categories, recommendation order, and my usage goals. Do not use an old fixed list. Before installing, listing, or removing skills, tell me what you plan to do. After installing, verify that Claude Code can recognize the installed skills. Before removing anything, run npx skills list --global to confirm the exact name. Report what succeeded, what failed, and the next step.
```

<h3 id="manual-install">Manual Install (Advanced)</h3>

Only use this path when you want control over every step.

1. Prepare [Environment / Node.js](/docs/environment/nodejs)
2. Install `Claude Code`

```bash
npm install -g @anthropic-ai/claude-code@latest
```

3. Write `~/.claude/settings.json`

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "{{ANTHROPIC_BASE_URL}}",
    "ANTHROPIC_AUTH_TOKEN": "your sk-...",
    "CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC": "1",
    "CLAUDE_CODE_ATTRIBUTION_HEADER": "0"
  }
}
```

`CLAUDE_CODE_ATTRIBUTION_HEADER` disables a dynamic attribution header that Claude Code injects at the start of every system prompt. This header contains a random hash that changes with every request, which completely breaks prompt caching on third-party API endpoints — cache hit rate drops from the normal 80%+ to 0%, meaning every request is billed at full price. Disabling it restores normal cache behavior and significantly reduces token costs.

Settings file location by platform:

- macOS / Linux: `~/.claude/settings.json`
- Windows: `%USERPROFILE%\.claude\settings.json`

4. If you are on native Windows and `Claude Code` cannot find `Git Bash`, add this:

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

One detail matters here:

- `ANTHROPIC_AUTH_TOKEN` is only Claude Code's field name
- the value inside it is still your SorryCode API key, which is the same `sk-...`

<h2 id="first-request">First Request</h2>

If you used one-click install, you usually do not need to send a manual request first.

Go to [Platform / First Request](/docs/platform/first-request) only when:

- the installer's final connectivity check failed
- you want to verify `API Key + Base URL + network` directly
- you are following the manual path

<h2 id="common-issues">Common Issues</h2>

- missing `node` or `npm`
  go to [Environment / Node.js](/docs/environment/nodejs)
- macOS gets blocked at the Apple installer, Homebrew, or Git
  go to [Environment / Node.js](/docs/environment/nodejs#macos)
- native Windows cannot find `Git Bash`
  add `CLAUDE_CODE_GIT_BASH_PATH` into `~/.claude/settings.json`
- `401 / 404 / 429`
  go to [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
- slow downloads or installer timeouts
  go to [Environment / Node.js](/docs/environment/nodejs#network)
- not sure where to create the API key
  go to [Platform / Create API Key](/docs/platform/create-api-key)
