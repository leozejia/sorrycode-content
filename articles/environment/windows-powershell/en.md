---
title: Windows PowerShell
slug: windows-powershell
order: 2
summary: The Windows terminal entry for SorryCode one-click install: how to open it, paste commands, and avoid shell or encoding mistakes.
section: environment
section_title: Environment
section_order: 40
---

# Windows PowerShell

If you are on Windows, use `PowerShell` or `Windows Terminal` for SorryCode one-click install.

You do not need to learn the command line first. Copy the full install command from the SorryCode console, open the terminal, paste it, and press Enter.

<h2 id="open">How to Open It</h2>

1. Press the `Win` key
2. Type `PowerShell` or `Terminal`
3. Open `Windows PowerShell` or `Windows Terminal`
4. Paste the `Windows` one-click install command from the SorryCode console or docs
5. Press Enter once

If you are unsure, open `Windows Terminal` first. If it is not installed, open `Windows PowerShell`.

<h2 id="install">How to Paste the Installer</h2>

Prefer the API key page first: click `Connect Tool`, choose `Codex` or `Claude Code`, choose `Windows`, then copy the full command from the modal.

If you cannot open the console modal, go to `Runtime / Codex` or `Runtime / Claude Code`, find the generic command under `Windows`, and copy the whole command.

Do not copy only half of it. Do not split it into multiple lines yourself.

- Install Codex: [Runtime / Codex](/docs/runtime/codex)
- Install Claude Code: [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="dont-mix-shells">Do Not Mix Shells</h2>

Windows has several command-line entry points:

| Name | Can you paste SorryCode Windows commands directly? |
| --- | --- |
| `PowerShell` | Yes |
| `Windows Terminal` | Yes, usually running PowerShell inside |
| `cmd` | Do not rewrite commands manually; the docs already wrap them with `cmd /c` |
| `Git Bash` | Do not paste PowerShell commands there |
| `WSL` | Do not paste Windows commands there; it behaves more like Linux |

Beginner rule:

```text
Run Windows docs commands in PowerShell / Windows Terminal.
```

<h2 id="execution-policy">Execution Policy</h2>

If you see `ExecutionPolicy` or “script cannot run”, do not permanently loosen your system policy first.

SorryCode's Windows one-click install only uses temporary `Bypass` for the current install process. It does not permanently change your machine policy.

If you are copying the Windows one-click command from a Runtime page, you usually do not need to run the commands below manually.

Use this section only when you are manually running a local `.ps1` file, or when support explicitly asks you to handle execution policy.

### Allow the Current Window Temporarily

This only affects the current PowerShell window. It stops working after you close the window, so prefer this first:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Allow Local Scripts for the Current User

This affects the current Windows user. Use it only when you understand the tradeoff or someone is guiding you:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

If it still fails, send the full error to the community or support instead of copying other long-term policy commands from the internet.

<h2 id="encoding">Encoding and JSON</h2>

Windows terminals can hit `console code page / PowerShell encoding mismatch`, which may break Chinese text, JSON, or file contents.

That is why SorryCode Windows examples usually:

- avoid inline complex JSON
- write `request.json` first
- save it as UTF-8 without BOM
- let `curl` read the file

If you are a beginner, you do not need to learn these terms. Copy the PowerShell examples as written, and do not convert macOS / Linux commands into Windows commands yourself.

<h2 id="next">Next</h2>

- Install Codex: [Runtime / Codex](/docs/runtime/codex)
- Install Claude Code: [Runtime / Claude Code](/docs/runtime/claude-code)
- Prepare Node.js: [Environment / Node.js](/docs/environment/nodejs)
