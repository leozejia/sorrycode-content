---
title: Windows PowerShell
slug: windows-powershell
order: 2
summary: Open PowerShell, copy Windows commands, and avoid shell and encoding mismatches.
section: environment
section_title: Environment
section_order: 40
---

# Windows PowerShell

The default Magpie GUI setup does not require a terminal. Use this page only when installing terminal tools or Skills, or troubleshooting manually.

<h2 id="open">Open PowerShell</h2>

Press `Win`, search for “Windows PowerShell,” and open it. If you use Windows Terminal, confirm that the active tab is running PowerShell.

<h2 id="install">Copy a command</h2>

Copy the complete command labeled for Windows PowerShell, paste it, and press Enter. For Claude Code, follow the Windows path in its [official installation guide](/docs/agents/claude-code). Do not run an old SorryCode connector over Magpie's settings.

<h2 id="dont-mix-shells">Do not mix shell syntax</h2>

PowerShell, cmd, Git Bash, and WSL are different environments. Windows Terminal is a terminal window; not every tab runs PowerShell. Do not paste macOS or Linux commands directly into PowerShell.

<h2 id="execution-policy">A script is blocked by execution policy</h2>

Check that the script source is trusted and read the error first. If you need to run a local `.ps1`, allow it only for the current window:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

This setting ends when the window closes. You do not need a permanent system policy change. On managed devices, follow your administrator's policy instead of bypassing organization controls.

<h2 id="encoding">Chinese text and JSON encoding</h2>

A common cause is a Windows console code page / PowerShell encoding mismatch. Write JSON to a UTF-8 file without BOM, then send it with `curl.exe`. Do not squeeze multiline JSON into an inline command.

[First Request](/docs/start/first-request) includes complete PowerShell file-writing examples. Use them without mixing cmd or Bash syntax. Hide keys and personal information before sharing errors.

<h2 id="next">Next</h2>

Return to [Claude Code](/docs/agents/claude-code) or the [Skill](/docs/skills/featured-skills) you are installing. If model access is not configured yet, start with [Magpie](/docs/agents/magpie).
