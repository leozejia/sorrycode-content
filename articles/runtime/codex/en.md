---
title: Codex
slug: codex
order: 1
summary: Understand Codex first, prepare your API key, finish one-click install, and start using it right away.
section: runtime
section_title: Runtime
section_order: 10
---

# Codex

If you want a model to read your project, edit code, and run commands locally, this page is the shortest path.

For a first-time user, the main goal is to get the path working. Do not start with config files, and do not assume you need to learn a lot of terminal commands first.

<h2 id="what-is-codex">What Codex Is</h2>

- `Codex` is a terminal runtime / agent built for code work
- it can read your project, edit files, run commands, and answer code questions
- on SorryCode, you just point it at `{{API_BASE_URL}}` and give it your API key

For a first setup, you do not need to understand `config.toml`, `auth.json`, or env vars up front. One-click install is enough.

Reference: [OpenAI Codex official repository](https://github.com/openai/codex)

> Beginner rule: `Codex` is a runtime, not a model. It is the default fit for GPT / OpenAI-compatible paths. Do not put Claude models into Codex casually; if you are unsure, read [Platform / Runtimes and Models](/docs/platform/runtime-models).

<h2 id="prepare-api-key">Prepare the API Key First</h2>

The installer will ask for your API key during the flow, so do this first:

1. Sign in to the SorryCode console
2. Find `API Keys` inside the console
3. If you do not have one yet, create a new `sk-...`
4. Keep it nearby, because the installer will ask for it right away

The quick link is `https://sorrycode.com/keys`, but the more important thing is knowing where this page sits inside the console.

If you have not done this yet, start with [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="one-click-install">One-Click Install</h2>

This is the default path. The installer connects `Codex` to `{{API_BASE_URL}}` and writes the local config. After install, use `Codex App` to open your project.

### macOS / Linux

The one-click installer handles required dependencies automatically. On macOS, it checks `Command Line Tools / Homebrew / Git`, then installs `Node.js 22 LTS` and `Codex CLI`.

Open Terminal first: press `Command` + `Space`, type `Terminal`, then press Enter.

Copy the full command below, return to the Terminal input area, press `Command` + `V` to paste it, then press Enter once.

If an Apple system installer appears, click Install and keep the terminal open. If Homebrew asks you to press Enter, press Enter. If the terminal asks for a password, enter your Mac login password; typed password characters are not shown.

```bash
curl -fsSL -o /tmp/sorrycode-codex.sh {{INSTALL_SH_URL}} && bash /tmp/sorrycode-codex.sh --base-url "{{API_BASE_URL}}" --source sorrycode-docs
```

### Windows

Press `Win`, type `PowerShell` or `Terminal`, open it, and paste this. If you are not sure what PowerShell is, read [Environment / Windows PowerShell](/docs/environment/windows-powershell) first:

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-codex.bat {{INSTALL_BAT_URL}} && %TEMP%\sorrycode-codex.bat --base-url {{API_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>What the installer does</summary>

- checks `Node.js / npm`
- on macOS, checks `Command Line Tools / Homebrew / Git`
- installs `Codex CLI`
- writes `~/.codex/config.toml`
- writes `~/.codex/auth.json`
- runs one minimal connectivity check
- on Windows, uses `ExecutionPolicy Bypass` only for this install process and does not permanently loosen your PowerShell policy

</details>

The installer blocks until you provide an `sk-...` key.

If the last step says the connectivity check failed, that does not always mean the install failed. Balance, permissions, or upstream network issues can still break the remote check even when the local install is already done.

<h2 id="start-codex">How to Start After Install</h2>

For beginners, use `Codex App` by default.

Use this path:

1. Finish the one-click install on this page
2. Open the Codex App page: <https://developers.openai.com/codex/app>
3. Download and install `Codex App`
4. Open `Codex App`
5. Choose the project folder you want to work on
6. Send your first message

If you prefer viewing project files and changes inside a visual editor, continue with [Tools / VS Code](/docs/tools/vscode).

If the Codex App plugin entry is grey, or `/plugins` cannot find Chrome, Computer Use, Browser, or HyperFrames, continue with [Codex App Plugin Setup](/docs/runtime/codex-plugins).

<h2 id="cli-fallback">Fallback: Use the Terminal</h2>

If you do not use `Codex App`, you can enter the project folder in a terminal yourself, then run Codex commands.

Advanced users can remember three commands:

```bash
codex
```

Start a new Codex session.

```bash
codex resume
```

Show resumable sessions.

```bash
codex resume --last
```

Resume the latest session directly.

If Codex has not yet built in the newest released model name, start it with an explicit model:

```bash
codex -m gpt-5.5
```

`gpt-5.5` is only an example. Use the models currently available in [Platform / Runtimes and Models](/docs/platform/runtime-models) and your console.

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

<h2 id="manual-install">Manual Install</h2>

Only use this path when you want control over every step.

1. Prepare [Environment / Node.js](/docs/environment/nodejs)
2. Install `Codex CLI`

```bash
npm install -g @openai/codex@latest
```

3. Write `~/.codex/config.toml`

```toml
model_provider = "OpenAI"
model = "gpt-5.4"
review_model = "gpt-5.4"
model_reasoning_effort = "xhigh"
disable_response_storage = true
network_access = "enabled"

[model_providers.OpenAI]
name = "OpenAI"
base_url = "{{API_BASE_URL}}"
wire_api = "responses"
requires_openai_auth = true
```

4. Write `~/.codex/auth.json`

```json
{
  "OPENAI_API_KEY": "your sk-..."
}
```

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
- `401 / 404 / 429`
  go to [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
- slow downloads or installer timeouts
  go to [Environment / Node.js](/docs/environment/nodejs#network)
- not sure where to create the API key
  go to [Platform / Create API Key](/docs/platform/create-api-key)
