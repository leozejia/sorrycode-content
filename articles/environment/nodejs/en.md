---
title: Node.js
slug: nodejs
order: 1
summary: Shared environment troubleshooting for macOS and Windows. Use it for manual setup or when one-click install gets blocked.
section: environment
section_title: Environment
section_order: 40
---

# Node.js

For most CLIs, Node.js is not optional. It is the base layer. On macOS, you may also hit the `Command Line Tools / Homebrew / Git` layer.

But this page is not the default beginner entry.

If you only want to get `Codex` or `Claude Code` running, go back to the runtime page and use one-click install first. Read this page closely only when you want manual control or when the install is blocked at the `Apple installer / Homebrew / Git / node / npm` layer.

<h2 id="why-nodejs">Why Node.js Matters</h2>

- many CLIs are Node.js programs underneath
- if `node` or `npm` is missing, the runtime often cannot install at all
- when this layer is broken, gateway or API key issues are easy to misdiagnose

This page mainly helps when:

- `node` is missing
- `npm` is missing
- macOS shows an Apple system installer
- macOS asks for your computer password
- CLI installation fails with environment errors
- on Windows, you are not sure which shell to use or the script gets blocked; in that case, read [Windows PowerShell](/docs/environment/windows-powershell) first

<h2 id="macos">macOS</h2>

On macOS, one-click install tries to prepare three layers:

1. `Apple Command Line Tools`
2. `Homebrew / Git`
3. `Node.js 22 LTS / npm`

You do not need to understand these first. Use the one-click command on the runtime page.

### Apple Command Line Tools

If the terminal says `Apple Command Line Tools` are required, an Apple system installer may appear.

Do this:

1. Click Install
2. Wait for it to finish
3. Keep the SorryCode terminal open

If you cancel the dialog or it never finishes, rerun the same SorryCode one-click command.

### Homebrew / Git

`Homebrew` is the common macOS tool installer. `Git` is used to install community Skills from GitHub.

The one-click installer tries to prepare both. If Homebrew asks you to press Enter, press Enter. If Terminal asks for a password, enter your Mac login password. Password characters are not shown while typing.

If your network cannot access GitHub, community Skills may still fail to install. SorryCode does not mirror those upstream repositories; switch network or proxy yourself.

### Node.js 22 LTS

SorryCode one-click install first tries to install `Node.js 22 LTS` into your user directory, so you do not need to handle Node manually.

If install finished but a new Terminal still says `node -v`, `npm -v`, or `codex` cannot be found, macOS usually has not loaded the command path.

Press `Command` + `Space`, type `Terminal`, press Enter, paste this full command, then press Enter:

```bash
grep -q 'HOME/.local/sorrycode-node/bin' ~/.zprofile 2>/dev/null || cat >> ~/.zprofile <<'EOF'
# >>> SorryCode managed PATH >>>
export PATH="$HOME/.local/sorrycode-node/bin:$HOME/.npm-global/bin:/opt/homebrew/bin:/usr/local/bin:$HOME/.local/bin:$PATH"
# <<< SorryCode managed PATH <<<
EOF
grep -q 'HOME/.local/sorrycode-node/bin' ~/.zshrc 2>/dev/null || cat >> ~/.zshrc <<'EOF'
# >>> SorryCode managed PATH >>>
export PATH="$HOME/.local/sorrycode-node/bin:$HOME/.npm-global/bin:/opt/homebrew/bin:/usr/local/bin:$HOME/.local/bin:$PATH"
# <<< SorryCode managed PATH <<<
EOF
source ~/.zprofile
```

Then close Terminal, open it again, and run:

```bash
node -v
npm -v
codex --version
```

Only install manually if one-click install fails:

Recommended priority:

1. the official Node.js installer
2. `Homebrew`

### Official Installer

This is the safest path for beginners:

- Open the [Node.js download page](https://nodejs.org/en/download)
- Download the `LTS` build
- Run the installer and finish the setup
- Close and reopen Terminal after installation
- Run `node -v` and `npm -v` again

Reference: [Node.js official download page](https://nodejs.org/en/download)

### Homebrew

If you already know what Homebrew is, you can also use:

```bash
brew install node
```

This manual Homebrew command installs Homebrew's default Node version. It is not the same as SorryCode's user-directory `Node.js 22 LTS` path.

<h2 id="windows">Windows</h2>

Recommended priority:

1. the official Node.js installer
2. `winget`

### Official Installer

- Open the [Node.js download page](https://nodejs.org/en/download)
- Download the `LTS` build
- Run the installer and finish the setup

### winget

```powershell
winget install OpenJS.NodeJS.LTS
```

<h2 id="powershell">PowerShell</h2>

For one-click install, you usually do not need to handle PowerShell execution policy yourself.

The SorryCode Windows install path uses `ExecutionPolicy Bypass` only for the current install process. It does not permanently change your machine policy.

Only think about manual policy changes when you are running local `.ps1` files yourself and the policy is the thing blocking you.

If your goal is only to install a runtime, do not treat this as a default prerequisite.

<h2 id="verify-install">Verify the Install</h2>

Run:

```bash
node -v
npm -v
```

If both commands print versions, this layer is ready.

The safer version choice is:

- Node.js `22 LTS`

For a first setup, do not start with the newest experimental branch.

<h2 id="network">Network Issues</h2>

Only switch the npm registry when downloads are clearly slow.

Switch to the China mirror:

```bash
npm config set registry https://registry.npmmirror.com
```

Reset to the official registry:

```bash
npm config set registry https://registry.npmjs.org
```

If this layer is ready, go back to:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)
- [Tools / CC-Switch](/docs/tools/cc-switch)
