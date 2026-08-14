---
title: Use Other Models in Codex
slug: codex-multi-model
order: 2
summary: Use DeepSeek and other models in Codex CLI or App through SorryCode's OpenAI-compatible API.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# Use Other Models in Codex

After you finish the [Codex setup](/docs/runtime/codex), Codex CLI and App share `~/.codex/config.toml` and the provider and authentication settings already on your machine. To switch models within the current API key group, change only the model ID. Do not change `model_provider`, reinstall Codex, or sign in again.

CLI can select a model for each launch. Codex App cannot currently display and switch to DeepSeek reliably in its interface, so you need to change the default model in the config and restart the App.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="prepare">Confirm the Key and Model ID</h2>

Open the [API Key page](https://sorrycode.com/keys) and confirm that the key's group contains the model you want. You can keep using an existing compatible key. Create another key only when you need separate usage records, spending limits, or credential rotation.

Use the exact model ID shown for the current group. For example, if the group exposes these models, use these names in the commands below. A model appearing in the group means that the key can route to it; stable Codex use still depends on compatibility with Responses, streaming, and tool calls.

```text
deepseek-v4-flash
deepseek-v4-pro
```

<h2 id="cli">Switch Models in Codex CLI</h2>

Pass the model with `-m` when starting Codex:

```bash
codex -m deepseek-v4-flash
```

Run `/status` inside the session to confirm the active model and provider. The same option works for non-interactive tasks:

```bash
codex exec -m deepseek-v4-flash "Review the current changes"
```

If a model is present in the built-in Codex model catalog, you can also enter `/model` and choose it from the list. `/model` only shows catalog entries; it does not accept an arbitrary model ID. DeepSeek is not currently in the built-in Codex catalog, so use `-m` directly.

If you use the same model often, create an official Codex profile at `~/.codex/deepseek.config.toml`:

```toml
model = "deepseek-v4-flash"
```

Start Codex with that profile:

```bash
codex --profile deepseek
```

The profile only overrides the model. Provider and authentication settings still come from your current global configuration. Do not change the existing provider just to switch models, regardless of its name.

<h2 id="app">Switch Models in Codex App</h2>

As of August 2026, the Codex App model picker may filter out third-party models. Even when DeepSeek is available to the current key, the picker may show only GPT models or label the active model as `Custom`.

To use DeepSeek in a new task, follow the steps below. The screenshots use the Chinese macOS interface. On other systems, open the App settings and continue from the `Configuration` page.

1. Choose `ChatGPT` > `Settings` from the macOS menu bar

   ![Open ChatGPT settings from the macOS menu bar](./codex-app-open-settings.png)

2. Open `Configuration` in the left sidebar

   ![Select Configuration in the settings sidebar](./codex-app-configuration-nav.png)

3. Click `Open config.toml`

   ![Open config.toml from the Configuration page](./codex-app-open-config.png)

4. Find the top-level `model` setting
5. Record the current `model` value and change only that setting. If `model_provider` is also present, leave its existing value unchanged
6. Save the file, quit the App completely, and reopen it. On macOS, use `Command-Q` instead of closing the window
7. Start a new task instead of testing the change in an existing task

The relevant settings should look like this after switching to DeepSeek:

```toml
model = "deepseek-v4-flash"
```

If `model` already exists, edit it in place instead of adding a duplicate. If it is absent, add it at the top level. Do not add, remove, or change `model_provider`. Do not place `model` inside any `[model_providers.*]` section.

To switch back to GPT, restore the `model` value you recorded, quit the App completely, and reopen it. Do not copy another user's GPT model ID because available models can differ by group and version.

Codex App currently uses one global default model at a time. It cannot place DeepSeek and GPT together in the picker for per-task switching. The App reads its model catalog at startup, so closing a window does not reload the config. Existing tasks may also retain their previous model or runtime settings.

If the App shows `Custom`, do not ask the model to identify itself. Check the actual model ID for the request in your SorryCode usage records.

Change only `model` when switching models. Codex sessions carry provider information. If an existing user replaces their original `model_provider` with `sorrycode`, all sessions under the original provider disappear from the current list and appear to have been erased. This does not mean the session data was deleted; restoring the original `model_provider` value should make those sessions visible again. Do not copy a provider value from this guide or another user, and do not change provider sections, authentication files, `CODEX_HOME`, or session directories.

<h2 id="troubleshoot">A Model Does Not Work</h2>

- CLI says the model does not exist: make sure the model ID exactly matches the name provided by the group, then check the key group
- App still uses the previous model: quit the App completely, use `Command-Q` on macOS, then reopen it and start a new task
- App shows `Custom`: this label can appear for custom models in the current version; verify the actual model ID in your SorryCode usage records
- Text starts streaming but tool calls fail: switch to a verified model and send the model ID and error to SorryCode
- All previous sessions disappear after switching: check whether `model_provider` was changed and restore its exact previous value before rerunning any installer
- Behavior changes after switching: start a new task and test again without modifying or migrating old tasks

References: [Codex configuration](https://developers.openai.com/codex/config-reference/), [DeepSeek's Codex integration guide](https://api-docs.deepseek.com/quick_start/agent_integrations/codex/), and [the Codex App custom-model issue](https://github.com/openai/codex/issues/19694).
