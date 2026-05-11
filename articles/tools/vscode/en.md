---
title: VS Code
slug: vscode
order: 3
summary: An optional visual project workspace. Open folders, inspect files and diffs, and install Codex / Claude Code extensions when needed.
section: tools
section_title: Tools
section_order: 28
source_url: https://code.visualstudio.com/
---

# VS Code

`VS Code` is a free project editor.

For a beginner, think of it as a project file browser + code editor + change viewer. It is not `Codex`, and it is not `Claude Code`. It is a visual workspace that can host extensions for those tools.

If you have not started `Codex` or `Claude Code` yet, you do not need VS Code first. The SorryCode default path is: run one-click install, then use the official desktop app to open your project.

<h2 id="when-to-use">When to Use It</h2>

Use VS Code when:

- you do not like staying in the terminal all the time
- you want a sidebar that shows project files
- you want to see what the AI changed more clearly
- you want one window for editing files, reviewing diffs, and using extensions
- you can already start `Codex` or `Claude Code`, and now want a more visual workspace

Do not make it your first required step. For a first-time user, getting the runtime working matters more.

<h2 id="install-vscode">Install VS Code</h2>

1. Open the VS Code website: <https://code.visualstudio.com/>
2. Click `Download` and install the version for your system
3. Open VS Code
4. Click `File / Open Folder...`
5. Choose the project folder you want to work on

Official setup guide: <https://code.visualstudio.com/docs/setup/setup-overview>

<h2 id="install-extensions">Install Extensions</h2>

VS Code extensions are installed from the `Extensions` panel on the left side.

The simplest path:

1. Open VS Code
2. Click the `Extensions` icon in the left sidebar
3. Search for the extension name
4. Open the extension detail page
5. Confirm it is official or from a trusted source
6. Click `Install`

Official extension guide: <https://code.visualstudio.com/docs/getstarted/extensions>

<h2 id="codex-extension">Codex Extension</h2>

If you want to use Codex inside VS Code, start with OpenAI's official IDE Extension docs:

- Codex IDE Extension: <https://developers.openai.com/codex/ide>

Recommended order:

1. Finish one-click install in [Runtime / Codex](/docs/runtime/codex)
2. Download and open `Codex App`, and confirm it can choose your project
3. Install VS Code
4. Install the Codex IDE extension by following OpenAI's official docs
5. If the extension asks for sign-in, authorization, or setup, follow the extension prompt

Do not assume the VS Code extension always reads every SorryCode setting automatically. If it asks for sign-in, authorization, or configuration, follow the official extension flow.

<h2 id="claude-code-extension">Claude Code Extension</h2>

If you want to use Claude Code inside VS Code, start with the official Claude Code VS Code docs:

- Claude Code VS Code: <https://code.claude.com/docs/en/vs-code>

Recommended order:

1. Finish one-click install in [Runtime / Claude Code](/docs/runtime/claude-code)
2. Download `Claude Desktop`, or confirm `claude` can start from your terminal
3. Install VS Code
4. Install the Claude Code extension by following the official docs
5. If the extension asks for sign-in, authorization, or setup, follow the extension prompt

<h2 id="mental-model">Three-Line Mental Model</h2>

- `Codex / Claude Code`: the agent runtime that performs the work
- `Skills`: instructions the agent can read and follow
- `VS Code`: the visual workspace for files, diffs, and extensions

So VS Code does not replace `Codex` or `Claude Code`. It makes the project and changes easier to see.

<h2 id="first-use">First Use</h2>

For your first run:

1. Open the project folder in VS Code
2. Check the file tree on the left and confirm it is the right project
3. Open `README`, `package.json`, or the project entry file
4. Open the relevant extension, or keep using `Codex App / Claude Desktop`
5. Ask the agent to explain the project before changing files

Copy this first prompt:

```text
Do not change files yet. Read the current project first, then tell me what it does, where the entry point is, and which files I should read first.
```

<h2 id="common-issues">Common Issues</h2>

- Is VS Code required?
  No. It is an optional visual workspace.
- How is it different from Codex App?
  `Codex App` is Codex's own desktop app. `VS Code` is a general editor that can install different extensions and is useful for viewing files and diffs.
- Will extensions automatically work with SorryCode after install?
  Not always. Finish the SorryCode runtime setup first; if an extension asks for sign-in or configuration, follow the official extension docs.
- Should I learn VS Code or Codex first?
  Get `Codex` or `Claude Code` running first. VS Code is a later option for making the workflow more visual.

<h2 id="next">Next</h2>

- Want Codex: [Runtime / Codex](/docs/runtime/codex)
- Want Claude Code: [Runtime / Claude Code](/docs/runtime/claude-code)
- Want to understand Skills: [Skills / What Skills Are](/docs/skills/featured-skills)
