---
title: WorkBuddy
slug: workbuddy
order: 1
summary: Install WorkBuddy, connect a SorryCode custom chat model such as Gemini 3.7 Flash, Gemini 3.8 Flash, or Claude Opus, and complete a first local file task with Default Permission.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy

WorkBuddy is a desktop agent that can read source material, call tools, and write results to local files. The steps below connect it to SorryCode and verify the model and file-writing path in an empty folder.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="install">Install WorkBuddy</h2>

Download the macOS or Windows app from the [WorkBuddy website](https://www.workbuddy.cn/), then install it and follow the sign-in flow. Do not download installers from unofficial websites.

<h2 id="prepare-key">Prepare an API Key</h2>

WorkBuddy uses the OpenAI-compatible `/v1/chat/completions` endpoint. On the [SorryCode API Key page](https://sorrycode.com/keys), choose a key whose group exposes both the model you need and this endpoint. Use a Gemini-group key for the Gemini examples below. You can reuse an existing compatible key; creating a separate key for WorkBuddy is optional for usage tracking, spending limits, or credential rotation.

WorkBuddy needs an exact model ID. Use an `id` returned by `/v1/models` for the current key instead of guessing from a display name.

```bash
curl https://sorrycode.com/v1/models -H "Authorization: Bearer <WORKBUDDY_API_KEY>"
```

In Windows PowerShell, use `curl.exe`:

```powershell
curl.exe https://sorrycode.com/v1/models -H "Authorization: Bearer <WORKBUDDY_API_KEY>"
```

<h2 id="connect">Add a SorryCode Custom Model</h2>

Open this path in WorkBuddy:

```text
Account menu in the lower-left → Settings → Models → Add Model → Custom
```

Use these values:

| Field | Value |
| --- | --- |
| Provider | `Custom` |
| Endpoint | `https://sorrycode.com/v1/chat/completions` |
| API Key | a SorryCode key whose group exposes the target model and OpenAI-compatible endpoint |
| Model Name | an exact model ID returned by `/v1/models` |
| Tool Calling | enabled |
| Image Input | enable only when the model and group support images |
| Thinking Mode | enable only when the model supports a reasoning mode |
| Custom Protocol | disabled |
| Input / Output | keep the provider defaults |

The endpoint must include the complete `/v1/chat/completions` path. After saving, the model appears in the `Custom Models` group.

<h2 id="claude-opus">Use Claude Opus</h2>

WorkBuddy can use `claude-opus-5` and `claude-opus-4-6` through the same custom-model flow. First confirm that both IDs appear in `/v1/models` for the Claude-group key, then add the two models separately:

- use `https://sorrycode.com/v1/chat/completions` for both endpoints
- use the same Claude-group key for both entries
- enter `claude-opus-5` and `claude-opus-4-6` as separate model names
- enable Tool Calling and disable Custom Protocol

Save each model separately. Both will then appear under `Custom Models`. This guide covers only the settings required for text and tool calls. Image Input and Thinking Mode need separate verification against the current WorkBuddy version and model-group capabilities.

<h2 id="gemini-flash">Use Gemini Flash</h2>

For `gemini-3.7-flash` and `gemini-3.8-flash`, use the Gemini-group key and add the two custom models separately with these values:

- endpoint: `https://sorrycode.com/v1/chat/completions`
- API key: the Gemini-group SorryCode key
- model names: `gemini-3.7-flash` and `gemini-3.8-flash`
- Tool Calling: enable only when the current model and group support it
- Custom Protocol: disabled

Save the two models separately. Both use `https://sorrycode.com/v1/chat/completions` and the same Gemini-group key, then appear under `Custom Models`.

<h2 id="add-more-models">Add More Models</h2>

WorkBuddy does not automatically import every model returned for the current key. To use several models from the same group, get their exact IDs from `/v1/models`, then repeat `Add Model` for each one. The endpoint and API key can stay the same; only the model ID needs to change. After saving, the models appear together under `Custom Models`.

This does not mean WorkBuddy can use every model on SorryCode. Custom models currently need an OpenAI-compatible Chat Completions interface. Image-generation, video-generation, and other non-chat models cannot be used as the WorkBuddy primary model. Agent tasks such as file operations also require tool-call support, while Image Input and Thinking Mode should only be enabled when the model supports them.

<h2 id="verify">Complete the First File Task</h2>

Create an empty folder such as `WorkBuddy-Test`, select it as the workspace in `New Task`, and keep `Default Permission` enabled. Select the custom model and enter:

```text
Create hello-workbuddy.md in the current workspace. Include today's date and the sentence "SorryCode connection test complete." Do not modify any other files. Tell me the saved path when finished.
```

The setup is working when WorkBuddy returns a normal response and `hello-workbuddy.md` appears in the test folder. This verifies the model connection, tool call, and workspace write path.

<h2 id="experts">Expert and Expert Team</h2>

A WorkBuddy Expert combines a role, method, and tools for a defined class of problems. Expert Team is for complex work that needs several specialist roles: a lead divides the task and integrates the results.

An Expert is not a new model and does not bypass file permissions. It still uses the current model and works through configured Skills, MCP servers, or tools. Complete the regular file task above first. Choose an Expert when you need a stable specialist role, and use Expert Team when the task genuinely requires collaboration.

See [How Agent Capabilities Are Extended](/docs/runtime/agent-capabilities) for how these mechanisms relate. Refer to the [Expert Center](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center) for WorkBuddy-specific setup.

<h2 id="permissions">File Permissions</h2>

- Use an empty test folder first, not the Desktop, Downloads folder, home directory, or a production project
- Keep Default Permission enabled and inspect requests to delete, overwrite, bulk-move, or run scripts
- Work on copies of important files and write new outputs instead of overwriting the only original
- Store the API key only in model settings, not in prompts, project files, or screenshots
- Do not enable Full Access in folders containing customer data, financial files, or credentials

<h2 id="common-issues">Common Issues</h2>

| Symptom | What to check |
| --- | --- |
| `401` or invalid key | the key is complete, still enabled, and its group supports the current model |
| `404` or model not found | the endpoint includes `/v1/chat/completions` and the model is an exact `/v1/models` ID |
| Chat works but no file is created | Tool Calling is enabled and the model supports OpenAI-compatible tool calls |
| Images are not understood | the model, group, and Image Input setting all support images |
| `429` or insufficient balance | SorryCode balance, key limit, and request rate |

For shared errors, see [Common Errors](/docs/troubleshoot/common-errors). Upstream references: [first task](https://www.workbuddy.cn/docs/workbuddy/FirstTask), [model configuration](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model), and [permission modes](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes).
