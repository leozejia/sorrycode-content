---
title: Codex App Plugin Setup
slug: codex-plugins
order: 1
summary: Manually configure ~/.codex/config.toml when the Codex App plugin entry is grey, or /plugins cannot find Chrome, Computer Use, Browser, or HyperFrames.
section: runtime
section_title: Runtime
section_order: 10
---

# Codex App Plugins Greyed Out? Configure Them Manually

> Tip: if you do not want to read every detail, click "Copy Markdown" in the top right and send this page to your agent, such as Codex or Claude Code. Ask it to inspect and update your local config.
>
> You can say:
>
> ```text
> Read this document, check my ~/.codex/config.toml, and configure the common Codex App plugins for me. Before changing anything, tell me which files you will edit.
> ```

This page solves one problem:

**The plugin entry in Codex App is grey, or `/plugins` cannot find the plugin you want. What should you edit manually?**

Shortest answer: edit this file.

```text
~/.codex/config.toml
```

## Step 1: Open the Config File

The config file lives here:

```text
~/.codex/config.toml
```

If you do not want to find it yourself, ask Codex or Claude Code to open it:

```text
Open ~/.codex/config.toml and check my Codex plugin configuration.
```

If the file does not exist, ask the agent to create it.

## Step 2: Add the Plugin Config

Add this block to `~/.codex/config.toml`:

```toml
[plugins."browser-use@openai-bundled"]
enabled = true

[plugins."chrome@openai-bundled"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true

[plugins."hyperframes@openai-curated"]
enabled = true
```

Save the file.

## Step 3: Restart Codex App

After changing the config, fully quit Codex App and open it again.

Do not only close the window.

On macOS, right-click Codex in the Dock and choose Quit, or quit Codex from the menu bar.

After reopening, enter a project and click the plugin menu next to the input box.

If you can see these items, the config is working:

- Browser
- Chrome
- Computer Use
- HyperFrames

## Step 4: Call Plugins Directly

After the plugins appear, you do not need to use the grey sidebar entry.

Call them from the input box.

### Let Codex Operate Real Chrome

```text
@Chrome open X and read this post for me
```

Use this for websites that need your logged-in browser, such as X, GitHub, Gmail, Stripe, or Google Cloud Console.

### Let Codex Operate the Desktop

```text
@Computer open System Settings and check screen recording permissions
```

Use this for system settings, desktop apps, and permission checks.

### Let Codex Make Video and Motion

```text
@HyperFrames make a 10-second product intro video
```

Use this for HTML video, product demos, and motion compositions.

If you want to make a real video workflow, continue with [Tools / HyperFrames](/docs/tools/hyperframes).

### Let Codex Test Local Web Pages

```text
@Browser open http://localhost:3000 and test the login flow
```

Use this for local projects, localhost, screenshots, forms, and web QA.

## Why Not `/plugins`

If Codex App or Codex CLI `/plugins` works for you, use the official path.

But if you are reading this page, you probably hit one of these cases:

- The Codex App sidebar plugin entry is grey.
- `/plugins` cannot find the plugin you want.
- Plugins such as HyperFrames already exist in the local cache but do not show up.
- The plugin UI and the real config state do not match.

In this case, the direct thing to check is `~/.codex/config.toml`.

## HyperFrames Is Easy to Name Wrong

The HyperFrames config is:

```toml
[plugins."hyperframes@openai-curated"]
enabled = true
```

Do not write:

```toml
[plugins."hyperframes@plugins"]
enabled = true
```

The config needs the marketplace name, not the local folder name.

Use this marketplace name:

```text
openai-curated
```

## Chrome Needs the Extension and Native Host

Chrome needs two pieces:

1. Codex Chrome Extension.
2. Codex native host.

Codex Chrome Extension URL:

```text
https://chromewebstore.google.com/detail/codex/hehggadaopoacecdllhhajmbjkdcmajg
```

You can think of the native host as the local bridge between Codex and Chrome.

Without that bridge, Codex may show the Chrome plugin, but `@Chrome` can still fail when you actually call it.

If the Chrome Web Store says the extension is not available in your region, switch to a reachable region or network first. Do not assume "not found in the store" means the extension does not exist.

If `@Chrome` cannot connect, ask your agent:

```text
Check whether the Codex Chrome Extension and native host are working. Do not read my cookies, passwords, or private browser data.
```

## Chrome Usage Notes

Before using `@Chrome`, make sure the Codex extension in Chrome is connected.

Example call:

```text
@Chrome open Salesforce and update the customer record from these notes
```

When Codex uses the Chrome plugin, it often opens a dedicated tab group in the background. It can read pages, fill forms, click buttons, and validate across tabs.

For sensitive actions, such as submitting forms, downloading files, or accessing personal information, the agent should pause and ask you to confirm.

If file upload or download fails, open:

```text
chrome://extensions/
```

Find the Codex extension, open Details, and enable:

```text
Allow access to file URLs
```

This path is for Google Chrome. Do not assume Edge, Arc, or other Chromium browsers are equivalent.

## Computer Use Needs System Permissions

If `@Computer` appears but cannot operate the screen, macOS permissions are usually missing.

Check here:

```text
System Settings -> Privacy & Security -> Screen Recording
System Settings -> Privacy & Security -> Accessibility
```

Grant access to Codex or Codex Computer Use related items, then restart Codex App.

## Check Old Browser Automation Last

If the config is correct, Codex App has been restarted, and the Chrome extension plus native host are working, but `@Chrome` still hangs, then check old browser automation tools.

Ask your agent to look for old processes first:

```bash
ps -axo pid,ppid,comm,args | rg -i 'agent-browser|browser-use|\.agent-browser|\.browser-use'
```

Old state may live here:

```text
~/.agent-browser
~/.browser-use
```

Not everyone has these tools. If you previously installed older browser automation tools such as `agent-browser`, `browser-use`, or something similar, check their processes and state directories.

Only clean them up after you confirm you no longer need those old tools.

Do not delete unfamiliar directories first.

## Final Check

Confirm these three things in order:

1. `~/.codex/config.toml` contains the plugin config.
2. Codex App has been fully quit and reopened.
3. The plugin menu next to the input box shows Browser, Chrome, Computer Use, or HyperFrames.
