---
title: Cursor Agent
slug: cursor
order: 1
summary: Configure SorryCode models in the Cursor editor and use Agent for code and file tasks.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: cursor
group_title: Cursor
group_order: 15
---

# Cursor Agent

Cursor is an editor-based agent for code projects. It can read a repository, edit files, run commands, and keep working in the editor.

This page covers Agent mode in the Cursor desktop editor, not the `cursor-agent` command-line tool. The CLI uses Cursor's own account and API credential system, so a SorryCode API key is not a replacement for its login credential.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="install">1. Install Cursor</h2>

Install the version for your system from the [official Cursor download page](https://cursor.com/downloads), then sign in to your Cursor account.

Open a test project. For the first connection, use a directory without important files so you can verify the path safely.

<h2 id="prepare-key">2. Prepare a Key for the Model Group</h2>

Choose a key on the [SorryCode API Key page](https://sorrycode.com/keys). Its group must expose the model you plan to use in Cursor.

List the models available to that key first:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <YOUR SORRYCODE API KEY>"
```

Use `curl.exe` in Windows PowerShell:

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <YOUR SORRYCODE API KEY>"
```

Use the exact `id` returned by this request. Do not mix keys from different groups just because they share an `sk-` prefix.

<h2 id="configure">3. Configure SorryCode in Cursor</h2>

In Cursor, open:

```text
Cursor Settings → Models → API Keys
```

Fill in the OpenAI configuration:

| Field | Value |
| --- | --- |
| OpenAI API Key | Your SorryCode key for the target model group |
| Override OpenAI Base URL | On |
| Base URL | `https://sorrycode.com/v1` |

After saving, add or select the exact model ID returned by `/v1/models`. Do not copy an entire model catalog into Cursor. Add only models you intend to use and have verified with the current key.

Cursor's OpenAI Base URL override is global. It is not a multi-provider list like OpenCode. The active setup normally uses one SorryCode key for one model group. When you switch groups, replace the key and model instead of adding a model from another group to the existing setup.

<h2 id="verify">4. Verify Text, Then Verify Agent Tools</h2>

Select the model you just added in Cursor's Agent panel and send a request that does not modify files:

```text
Reply with exactly CURSOR_SORRYCODE_OK. Do not modify files.
```

After the exact reply arrives, send this from the test project:

```text
Create cursor-sorrycode-check.txt in the project root containing only CURSOR_TOOL_OK and a final newline. Do not modify other files.
```

Confirm the file contents, then remove the test file. This verifies both the model request and the Agent file tool path.

<h2 id="boundaries">5. Know the Boundaries</h2>

- Cursor's BYOK settings mainly cover standard model requests. Tab completion, Background Agent, and other Cursor-specific capabilities may continue to use Cursor-managed services. This page does not promise that they use SorryCode.
- A SorryCode key does not mean the client connects directly to SorryCode. Cursor may still send the request through its own backend to assemble the final prompt before forwarding the model request to the configured Base URL. If that privacy boundary is unacceptable, do not use this path.
- The OpenAI Base URL override may affect Cursor's built-in models. To return to Cursor's default models, turn the override off, choose a built-in model again, and start a fresh session.
- This guide does not require a general environment variable. Do not put the API key in project files, shell history, or chat messages.
- Your Cursor account and subscription remain separate Cursor product boundaries. SorryCode covers only model requests that pass through its gateway and the related usage charges.

<h2 id="common-issues">Common Issues</h2>

- `401`: check that the key is complete, valid, and assigned to the target model group.
- `404` or model not found: query `/v1/models` again and use an exact returned model ID.
- Text works but a file task fails: the current model or Cursor session may not have a working tool-call path. Start a fresh Agent session and repeat the minimal file task above.
- Requests still go to Cursor's built-in service: confirm that `Override OpenAI Base URL` is on and the Base URL is `https://sorrycode.com/v1`.
- A model disappears after switching groups: do not overwrite the old setup blindly. Query `/v1/models` with the new key and update the model list from that result.
- You want to use the `cursor-agent` CLI: that is outside this guide. Its account and credential system is different from Cursor editor's OpenAI BYOK path.

For a manual gateway check, read [First Request](/docs/start/first-request). If you do not have an API key yet, start with [Create API Key](/docs/start/create-api-key).
