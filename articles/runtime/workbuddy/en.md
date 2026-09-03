---
title: WorkBuddy
slug: workbuddy
order: 1
summary: Install WorkBuddy, add a SorryCode custom model, and complete a first local file task.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy

WorkBuddy is a desktop agent that can read source material, call tools, and write local files. This page keeps only the steps needed to connect SorryCode and complete a first file task.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. Do not paste your API key into the conversation.

<h2 id="install">Install</h2>

Download the macOS or Windows app from the [WorkBuddy website](https://www.workbuddy.cn/), then install it and follow the sign-in flow.

<h2 id="configure">Add a SorryCode custom model</h2>

On the [SorryCode API Key page](https://sorrycode.com/keys), choose a key whose group exposes the model you need. WorkBuddy uses the OpenAI-compatible `/v1/chat/completions` endpoint. The model name must be the exact `id` returned by `/v1/models` for that key.

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <your SorryCode API key>"
```

Open this path in WorkBuddy:

```text
Account menu in the lower-left → Settings → Models → Add Model → Custom
```

Fill in these fields:

| Field | Value |
| --- | --- |
| Provider | `Custom` |
| Endpoint | `https://sorrycode.com/v1/chat/completions` |
| API Key | a SorryCode key whose group exposes the target model |
| Model Name | the exact model ID returned by `/v1/models` |
| Tool Calling | enable for file tasks, when the model supports tool calls |
| Image Input | enable only when the model and group explicitly support images |
| Thinking Mode | enable only when the model supports reasoning |
| Custom Protocol | disabled |

For several models in one group, repeat only the model name. For example, a Gemini-group key can add `gemini-3.7-flash` and `gemini-3.8-flash`, while a Claude-group key can add `claude-opus-5` and `claude-opus-4-6`. Use only IDs returned for the current key. Gemini thinking uses `high`; enable Claude thinking only after the current WorkBuddy version and group have been verified.

<h2 id="verify">Complete the first file task</h2>

Create an empty folder such as `WorkBuddy-Test`, select it as the workspace in `New Task`, keep `Default Permission` enabled, and select the custom model. Enter:

```text
Create hello-workbuddy.md in the current workspace. Include today's date and the sentence "SorryCode connection test complete." Do not modify any other files. Tell me the saved path when finished.
```

The setup is working when WorkBuddy replies normally and `hello-workbuddy.md` appears in the test folder. For the first test, use an empty folder instead of the Desktop, Downloads folder, home directory, or a production project. Inspect requests to delete, overwrite, or run scripts before approving them.

<h2 id="boundaries">Boundaries</h2>

WorkBuddy custom models use Chat Completions. Image and video generation models cannot be WorkBuddy's primary model. Image Input, Thinking Mode, and file tools require support from the model, group, and client version. Store the API key only in model settings, not in prompts, project files, or screenshots.

Expert and Expert Team still use the current model and its existing permissions; they do not bypass file restrictions. Complete the regular file task first, then see [How Agent Capabilities Are Extended](/docs/runtime/agent-capabilities) and the [Expert Center](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Expert-Center).

<h2 id="common-issues">Common issues</h2>

| Symptom | Check first |
| --- | --- |
| `401` or invalid key | the key is complete and enabled, and its group supports the model |
| `404` or model not found | the endpoint includes `/v1/chat/completions` and the model is an exact `/v1/models` ID |
| Chat works but no file is created | Tool Calling is enabled and the model supports OpenAI-compatible tool calls |
| `429` or insufficient balance | SorryCode balance, key limit, and request rate |

For shared errors, see [Common Errors](/docs/troubleshoot/common-errors).

Official references: [first task](https://www.workbuddy.cn/docs/workbuddy/FirstTask), [model configuration](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Model), and [permission modes](https://www.codebuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes).
