---
title: Use Multiple SorryCode Models in Codex
slug: codex-multi-model
order: 2
summary: Use OpenCodex to add models from the current SorryCode key group to the Codex App model picker.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# Use Multiple SorryCode Models in Codex

Codex App does not list every model in the current SorryCode group by default. If [Codex](/docs/runtime/codex) is already connected and you want to select models such as DeepSeek directly in the model picker, use OpenCodex.

OpenCodex runs a local proxy and writes available models into the catalog shared by Codex. It does not modify the Codex App binary.

<h2 id="prepare">Prepare a Compatible API Key</h2>

On the [API Key page](https://sorrycode.com/keys), choose a key whose group contains the models you need and supports the OpenAI-compatible Responses endpoint used here. You can reuse an existing compatible key; creating a separate key for Codex is optional for usage tracking, spending limits, or credential rotation.

The key group determines the model list. "All models" on this page means every model returned for the current group, not models from other groups.

Paste this key directly into OpenCodex. No environment variable is required.

<h2 id="install">Install OpenCodex</h2>

Quit Codex App first, then run these commands in a terminal:

```bash
npm install -g @bitkyc08/opencodex
ocx --version
ocx gui
```

`ocx gui` starts the local proxy and opens its dashboard. OpenCodex listens on `127.0.0.1:10100` by default.

If `npm` is missing, read [Environment / Node.js](/docs/environment/nodejs) first.

<h2 id="provider">Add SorryCode</h2>

Open `Providers` in the OpenCodex dashboard, choose `Add provider`, then choose a custom endpoint. Use these settings:

| Field | Value |
| --- | --- |
| Provider ID | `sorrycode` |
| Adapter | `openai-responses` |
| Base URL | `https://sorrycode.com` |
| API Key | A compatible SorryCode key with access to the target models |
| Responses Path | `/v1/responses` |
| Live Model Discovery | On |

After saving, open `Models`. Keep the SorryCode group set to `All on` instead of creating a short model allowlist. OpenCodex will fetch the models visible to the current key and publish them to Codex as `sorrycode/model-name`.

For example, if the current group includes DeepSeek, the model picker will show:

```text
sorrycode/deepseek-v4-flash
sorrycode/deepseek-v4-pro
```

<h2 id="service">Keep Codex App Ready</h2>

Codex App requests now pass through the local OpenCodex process. Install its background service so it starts at login and restarts after a crash:

```bash
ocx service install
ocx sync --restart-codex
ocx service status
```

On Windows, open PowerShell as Administrator when installing the background service. After the sync completes, reopen Codex App and select a `sorrycode/...` model from the model picker.

Only one tool should manage the Codex configuration and model catalog at a time. Disable any other provider manager before enabling OpenCodex.

<h2 id="troubleshoot">Models Are Missing</h2>

- OpenCodex cannot see the target model: check the SorryCode group assigned to this key
- OpenCodex sees it but Codex App does not: run `ocx sync --restart-codex`
- Codex reports a local connection error: run `ocx service status` and follow the repair action
- More diagnostics are needed: run `ocx doctor`

To restore the native Codex configuration without removing OpenCodex, run:

```bash
ocx restore
```

To remove the background service and restore native Codex, run:

```bash
ocx service uninstall
```

Upstream references: [OpenCodex repository](https://github.com/lidge-jun/opencodex), [installation guide](https://opencodex.me/getting-started/installation/), and [Codex App model picker guide](https://opencodex.me/guides/codex-app-models/).
