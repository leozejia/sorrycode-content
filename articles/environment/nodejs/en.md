---
title: Node.js
slug: nodejs
order: 1
summary: Prepare Node.js only when a specific Skill or tool requires it.
section: environment
section_title: Environment
section_order: 40
---

# Node.js

Magpie and desktop agents do not require you to install Node.js first. Use this page only when a Skill or tool explicitly needs `node`, `npm`, or `npx`.

If an agent is already working, send it the Skill's installation guide and ask it to check the environment and explain proposed changes first.

<h2 id="why-nodejs">Check whether it is already installed</h2>

Run in a terminal:

```bash
node --version
npm --version
npx --version
```

If all three show version numbers, you usually do not need another installation. Follow the version requirements of the tool you are installing.

<h2 id="macos">macOS</h2>

Open the [Node.js download page](https://nodejs.org/en/download), choose the current LTS macOS installer, and install it. Reopen the terminal and check the versions again.

You do not need to install Homebrew for this step. If you already manage Node.js another way, ask the agent to check the existing setup instead of adding another installation.

<h2 id="windows">Windows</h2>

Choose the current LTS Windows installer on the [Node.js download page](https://nodejs.org/en/download) and install with the default options. Close and reopen PowerShell, then check the versions.

<h2 id="powershell">PowerShell errors</h2>

If `npm` reports a script execution policy restriction, read [Windows PowerShell](/docs/environment/windows-powershell#execution-policy). Do not permanently relax system policy.

<h2 id="network">Slow downloads or network errors</h2>

Check that you can reach the tool's official download page and GitHub. Try another network or check your proxy before retrying. A timeout does not establish an API key problem, and repeatedly installing different versions is not a network fix.

If it still fails, give the agent the full error and the guide for the tool you want to install.

<h2 id="next">Next</h2>

Return to the [Skill](/docs/skills/featured-skills) you want to install. If you have not connected an agent yet, start with [Configure SorryCode in Magpie](/docs/agents/magpie).
