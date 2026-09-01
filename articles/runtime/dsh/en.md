---
title: DSH
slug: dsh
order: 1
summary: Start the DeepSeek Harness Web UI, connect SorryCode models through Responses or Anthropic Messages, and send the first request.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: deepseek
group_title: DeepSeek
group_order: 22
---

# DSH

DSH, short for DeepSeek Harness, is an open-source agent harness from DeepSeek. Its Web UI lets you choose a workspace, manage models, and ask an agent to read files, run commands, and complete tasks.

DSH is not limited to DeepSeek models. It supports custom providers, so you can use Responses models through SorryCode as well as Claude models such as `claude-opus-5` and `claude-opus-4-6`.

DSH is still in developer preview. Its interface and configuration can change incompatibly. This guide follows the public Web UI and does not ask users to maintain internal configuration files.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="prepare">Prepare Node.js and an API Key</h2>

Check for Node.js and npm first:

```bash
node --version
npm --version
```

If either command is missing, read [Node.js](/docs/environment/nodejs) first.

Open the [API Key page](https://sorrycode.com/keys) and choose a key whose group contains the target model. Use a Grok-group key for `grok-4.6`, or a Claude-group key for `claude-opus-5` and `claude-opus-4-6`. One key group can expose multiple models; prepare another group key only when the target model belongs to a different group.

<h2 id="start">Start the DSH Web UI</h2>

Run the official command inside the project directory you want DSH to use:

```bash
npx @deepseek-ai/dsh web
```

The command prints the Web UI address. The default is:

```text
http://127.0.0.1:3080
```

Open that address in a browser. A fresh DSH instance has no selected workspace until you add one in the interface.

<h2 id="configure">Add the SorryCode Provider</h2>

Open `Settings` > `Models` in the DSH Web UI, then choose `Add Custom Provider`. Use these values for a Responses model:

| Field | Value |
| --- | --- |
| Provider ID | `sorrycode-grok` |
| Display name | `SorryCode Grok` |
| Base URL | `https://sorrycode.com/v1` |
| API protocol | `openai-responses` |
| API key | The SorryCode key for the target group |

Use a separate provider for Claude models:

| Field | Value |
| --- | --- |
| Provider ID | `sorrycode-claude` |
| Display name | `SorryCode Claude` |
| Base URL | `https://sorrycode.com` |
| API protocol | `anthropic-messages` |
| API key | The SorryCode key whose group contains the target Claude model |

Use a lowercase Provider ID. DSH records it in model defaults and saved sessions, so do not rename it casually after saving. Give every independent key a unique Provider ID and a display name that identifies its group. Models returned for the same key group and protocol can share one provider; add another provider for a different key group or protocol instead of overwriting an existing key.

Click `Get Available Models`. DSH queries the model catalog with the Base URL and key shown in the form. Select the target model from the result, then save the provider. If model discovery fails after you have confirmed the key and Base URL, you can enter the exact model ID manually.

Model discovery mainly confirms which model IDs the current key can use. It does not prove that image input, context capacity, or thinking levels are configured. Complete the text-only connection check below first. For images or custom thinking levels, follow the current [DSH model configuration guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md) and verify each capability with a minimal request instead of inferring it from the model name.

DSH stores the key in its credential file and only returns a redacted descriptor to the settings page. Public setup does not require an environment variable. Do not put the key in a regular settings field or a chat message.

<h2 id="workspace">Choose the Model and Workspace</h2>

After saving the provider:

1. Select the SorryCode provider and model you just added
2. Click `Choose workspace`
3. Add and select the project directory where you started DSH
4. Start a new session

The composer remains unavailable until a workspace is selected.

<h2 id="verify">Verify the Connection</h2>

Send a minimal request that does not modify files:

```text
Reply with exactly DSH_SORRYCODE_OK. Do not modify files.
```

A model response confirms the `DSH + SorryCode key + selected protocol + target model` connection. Prompt interpretation, tool selection, and output style remain model and DSH behavior rather than a SorryCode integration promise.

<h2 id="other-models">Use Another Model</h2>

Other models from the same key group and protocol can share the existing provider. Create a new Provider ID with the matching key for a different group or protocol, do not overwrite an existing provider, and always use an exact model ID returned by `Get Available Models`. Chat Completions should also use a separate provider.

<h2 id="common-issues">Common Issues</h2>

- `npx` is not found: install Node.js, then reopen the terminal
- the Web UI does not open: keep the DSH terminal running and use the exact address it printed
- `401`: check that the key is complete, valid, and assigned to the target model group
- model discovery returns `401 / 403`: check the Base URL and key before adding unknown models manually
- the target model is absent: refresh the model list and confirm that the current key group includes it
- a previous model disappears after switching groups: do not overwrite an existing provider with another group's key; add a new Provider ID
- an image is rejected before sending: model discovery confirmed only the ID; configure image capability with the current model guide and start a new session
- the composer is unavailable: select both a workspace and a model
- fields change after an update: DSH is still in developer preview, so follow the current official interface

References: the [DeepSeek Harness repository](https://github.com/deepseek-ai/deepseek-harness), [Web UI guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md), and [model configuration guide](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/providers.md).
