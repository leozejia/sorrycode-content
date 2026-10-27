---
title: FAQ
slug: common-errors
order: 6
summary: Look up connection errors, missing Node.js, PowerShell, and encoding issues when you need them.
section: start
section_title: Getting Started
section_order: 1
---

# FAQ

With the default Magpie setup, first confirm that Magpie is running, **Connect** is enabled for the target agent, and you reopened the agent after setup. Do not run an old connector over this configuration.

## Missing models or an unrecognized agent

- Click **Fetch Models** again in the Magpie provider settings, save, and select the models you need.
- Confirm that the agent is installed and the Magpie entry matches the actual client. WorkBuddy and WorkBuddy AI, and the different Cursor client types, are not interchangeable.
- Update and reopen Magpie. Do not copy another tool's configuration into an unsupported client.

## 401 Unauthorized / API KEY REQUIRED

`API KEY REQUIRED` means the server did not receive supported authentication information. It does not mean the balance is empty. Other `401` errors can also indicate an invalid or disabled key.

Check that the provider's key in Magpie is complete, active, and belongs to the selected group. Then confirm that the request actually goes through Magpie. Old connectors, manual settings, or environment variables may point the agent elsewhere. Do not paste your key into chat for troubleshooting.

The provider Base URL in Magpie points to SorryCode. The agent may connect to a local Magpie gateway URL instead. These addresses can coexist; do not overwrite one with the other to make them match.

## 403 / unavailable model

Check whether the key's group exposes the requested model. Fetch the current model list in Magpie and choose from it instead of copying model names from an old guide. Fetch models again after changing groups.

## 404 Not Found

Check the provider Base URL against the [Magpie guide](/docs/agents/magpie). Do not append `/v1` twice or include a full request path. For manual API calls, check each protocol and path separately rather than applying one URL rule to every endpoint.

## 429 / quota problems

Check the account balance and key spending limit, then reduce request frequency and concurrency. Rate limiting and insufficient balance are different causes.

<h2 id="network">Timeout / TLS / interrupted connection</h2>

Confirm that Magpie is running, then check whether your network or proxy can reach the provider URL. Reinstalling repeatedly is not a network fix. For an interrupted paid image request, check whether it already completed before submitting another.

<h2 id="nodejs">Missing node, npm, or npx</h2>

Magpie and desktop agents do not require Node.js first. Check it only when a Skill explicitly needs it:

```bash
node --version
npm --version
npx --version
```

If these show version numbers, you usually do not need another installation. Follow the Skill's version requirements. If an agent is already working, send it the Skill guide and ask it to check the environment and explain proposed changes first.

If Node.js is missing, download the current LTS macOS or Windows installer from the [official website](https://nodejs.org/en/download), install with the default options, reopen the terminal, and check again. You do not need Homebrew for this. If you already manage Node.js another way, do not add another installation. Check your network and proxy for download timeouts rather than repeatedly changing versions.

<h2 id="windows-powershell">Windows command or script errors</h2>

Press `Win`, search for Windows PowerShell, and open it. In Windows Terminal, confirm that the active tab runs PowerShell. Copy the complete command for the stated shell. Do not mix cmd, Git Bash, WSL, or macOS / Linux syntax.

<h3 id="execution-policy">A script is blocked by execution policy</h3>

Read the error and confirm that the source is trusted. If you need to run a local `.ps1`, allow it only for the current window:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

This setting ends when the window closes. You do not need a permanent system policy change. On managed devices, follow your administrator's policy instead of bypassing organization controls.

<h3 id="encoding">Chinese text or JSON encoding problems</h3>

A common cause is a Windows console code page / PowerShell encoding mismatch. Write JSON to a UTF-8 file without BOM, then send it with `curl.exe --data-binary "@file.json"`. Do not use inline multiline JSON. [First Request](/docs/start/first-request) has complete PowerShell file-writing examples.

## Still failing

Record the agent and Magpie versions, time, full error, and request ID. Hide the key and personal information. Use a [manual API check](/docs/start/first-request) only when you need to separate gateway and client failures.
