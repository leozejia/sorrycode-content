---
title: Grok
slug: grok-cli
order: 1
summary: Understand Grok first, prepare your API key, finish one-click install, and start using it right away.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: xai
group_title: xAI
group_order: 30
---

# Grok

If you want to use Grok locally to read a project, edit code, and run commands while sending requests through SorryCode, this page is the shortest path.

For a first-time user, the main goal is to get the path working. Do not start with config files, and do not assume you need to learn a lot of terminal commands first.

> **Which path?**
>
> **→ One-Click Install (Recommended):** Click `Connect Tool` on the API key page → copy the command → paste it into your computer's terminal → done. For most people.
>
> **→ Generic Installer Command:** Still uses the SorryCode installer, but asks you to paste a Grok-group key during setup. Use it when the `Connect Tool` modal is unavailable.
>
> The default flow below follows the one-click path.

<h2 id="what-is-grok">What Grok Is</h2>

- `Grok` is a local terminal runtime / agent from xAI
- it can work with you in the terminal, read projects, answer questions, and run local tasks
- on SorryCode, you just point it at `{{API_BASE_URL}}` and give it your API key

For a first setup, you do not need to understand the internal fields in `~/.grok/config.toml`. One-click install is enough.

Reference: [xAI Grok official installer](https://x.ai/cli/install.sh)

> Beginner rule: `Grok` is a runtime, not a model. It is the default fit for Grok / xAI-compatible paths. Do not put GPT or Claude models into Grok casually; if you are unsure, read [Getting Started / Tools Are Not Models](/docs/concepts/tools-models-platform).

<h2 id="prepare-api-key">Prepare the API Key First</h2>

The install command needs to be tied to your API key, so do this first:

1. Sign in to the SorryCode console
2. Find `API Keys` inside the console
3. If you do not have one yet, create a new `sk-...`
4. Make sure this key can use a Grok group
5. Return to the list and prepare to click `Connect Tool` for that key

The quick link is `https://sorrycode.com/keys`, but the more important thing is knowing where this page sits inside the console.

If you have not done this yet, start with [Getting Started / Create API Key](/docs/start/create-api-key).

If you also plan to use Codex, Claude Code, or SorryCode Image2, create a separate API key for each purpose. Multiple keys still use the same balance, but each key should use the group that matches its purpose.

<h2 id="one-click-install">⚡ One-Click Install (Recommended)</h2>

This is the default path. The console generates an install command for the current API key. Paste that command into the terminal on your own computer, and the installer will connect `Grok` to `{{API_BASE_URL}}`, write the local config, and set the default model to `grok-4.5`. After install, reopen the terminal and run `grok`.

### Step 1: Copy the Command in the Console

1. Open `https://sorrycode.com/keys`
2. Find the API key you prepared for Grok
3. Click `Connect Tool`
4. Choose `Grok`
5. Choose your operating system
6. Click `Copy`

The copied command is complete and already includes the current API key.

### Step 2: Paste It into Your Computer's Terminal

- Mac: press `Command + Space`, type `Terminal`, then press Enter
- Windows: press `Win`, type `PowerShell` or `Terminal`, then press Enter

After the terminal opens, paste the full command you copied and press Enter.

The one-click installer calls xAI's official installer, writes `~/.grok/config.toml`, and stores the selected Grok-group key separately. It does not overwrite the Image2 key used by SorryCode Image2. Windows uses the Windows-specific installer. If you are not sure what PowerShell is, read [Environment / Windows PowerShell](/docs/environment/windows-powershell) first.

### Fallback: Copy a Generic Command Manually

If you cannot open the `Connect Tool` modal, use the generic command below. It does not include your API key, so the installer will stop and ask you to paste the `sk-...` value.

macOS / Linux:

```bash
curl -fsSL https://sorrycode.com/install/sorrycode-grok.sh | bash -s -- --base-url "{{API_BASE_URL}}" --source sorrycode-docs
```

Windows:

```powershell
cmd /c "curl -fsSL -o %TEMP%\sorrycode-grok.bat https://sorrycode.com/install/sorrycode-grok.bat && %TEMP%\sorrycode-grok.bat --base-url {{API_BASE_URL}} --source sorrycode-docs"
```

<details>
<summary>What the installer does</summary>

- checks whether `grok` is already installed
- if not, calls xAI's official installer
- backs up an existing `~/.grok/config.toml`
- writes the SorryCode `~/.grok/config.toml`
- sets the default model to `grok-4.5`
- stores the selected Grok-group key separately without overwriting keys used by other tools
- on Windows, uses `ExecutionPolicy Bypass` only for this install process and does not permanently loosen your PowerShell policy

</details>

If you copied the command from `Connect Tool`, the installer usually does not need to ask for the API key again. If you use the generic command above, the installer blocks until you provide an `sk-...` key.

If the current terminal still cannot find `grok` after install, close it and open a new one. Many installers update the shell path for new sessions, so the old window may not see the command immediately.

<h2 id="start-grok">How to Start After Install</h2>

Enter the project folder you want to work on, then run:

```bash
grok
```

If you keep multiple Grok configs, specify the SorryCode path explicitly:

```bash
grok -m sorrycode-grok
```

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

<h2 id="manual-install">When You Need Manual Control</h2>

Public setup does not require you to synchronize config fields or environment variables by hand. When you need control over the install steps, run xAI's official installer first, then run the generic SorryCode installer command above. The SorryCode installer detects an existing `grok` command and only adds the gateway config and the selected Grok-group key.

If the config is damaged, return to the API key page and generate a new install command from the Grok key. Do not copy a key from Codex, Claude Code, or SorryCode Image2 to repair Grok.

<h2 id="media">Where to Call Images and Video</h2>

The custom `base_url` in `~/.grok/config.toml` covers text, Responses, and search. Grok CLI's built-in image and image-to-video tools use a separate media client and do not inherit that address.

That means:

- keep using Grok CLI for text and search;
- use the REST API in [Grok Image Generation](/docs/runtime/grok-image) for images;
- use the REST API in [Grok Video Generation](/docs/runtime/grok-video) for text-to-video, image-to-video, and polling;
- do not give a SorryCode key to Grok CLI's built-in media tools, or the official xAI endpoint will reject it as invalid.

<h2 id="first-request">First Request</h2>

If you used one-click install, you usually do not need to send a manual request first.

Go to [Getting Started / First Request](/docs/start/first-request) only when:

- `grok` cannot respond normally after install
- you want to verify `API Key + Base URL + network` directly
- you are following the manual path

<h2 id="common-issues">Common Issues</h2>

- cannot find `grok`
  close the terminal, open a new one, then run `grok`
- `401 / 404 / 429`
  go to [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
- not sure where to create the API key
  go to [Getting Started / Create API Key](/docs/start/create-api-key)
- not sure how to choose between Grok, Codex, and Claude Code
  go to [Getting Started / Tools Are Not Models](/docs/concepts/tools-models-platform)
- built-in image or video tools report `Incorrect API key provided`
  the text configuration is still valid; use [Grok Image Generation](/docs/runtime/grok-image) or
  [Grok Video Generation](/docs/runtime/grok-video)
