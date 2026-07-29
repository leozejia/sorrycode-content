---
title: WorkBuddy Quick Start
slug: workbuddy
order: 1
summary: Install WorkBuddy, connect it to SorryCode, choose a safe workspace, and complete your first local file task.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy Quick Start

WorkBuddy is a desktop AI workbench. You can give it files, source material, and a task; it can plan the work, call tools, and save the result as an actual file.

To run WorkBuddy model requests through SorryCode, use this path:

1. Install and sign in to WorkBuddy
2. Add a SorryCode custom model in WorkBuddy
3. Choose a separate test folder for the first task
4. Keep Default Permission enabled and complete one low-risk file task

This page covers the end-to-end path. See [Connect WorkBuddy to SorryCode](/docs/runtime/workbuddy-sorrycode) for model fields and [WorkBuddy Permissions and Workspaces](/docs/runtime/workbuddy-permissions) for file access boundaries.

<h2 id="install">Install WorkBuddy</h2>

Download the desktop app for your computer from the official WorkBuddy website:

<https://www.workbuddy.cn/>

The current desktop app supports macOS and Windows. Open WorkBuddy after installation and follow the sign-in flow.

If the sign-in button does nothing, make sure your computer has a default browser, then quit WorkBuddy completely and reopen it. Do not download installers from unofficial websites.

<h2 id="connect-sorrycode">Connect SorryCode</h2>

WorkBuddy includes built-in models and also supports custom OpenAI-compatible APIs. SorryCode uses the custom API path.

Open:

```text
Account menu in the lower-left → Settings → Models → Add Model → Custom
```

Then follow [Connect WorkBuddy to SorryCode](/docs/runtime/workbuddy-sorrycode) to enter the endpoint, API key, and model name. After saving, the model appears under the `Custom Models` group in the chat model picker.

<h2 id="workspace">Prepare the First Workspace</h2>

Do not use the Desktop root, Downloads folder, your entire home directory, or an important project as the first test workspace.

Create an empty folder such as:

```text
WorkBuddy-Test
```

Return to `New Task`, click `Select Workspace` below the input box, and choose this folder. The workspace defines the files WorkBuddy will primarily read and write for this task.

Keep `Default Permission` enabled. WorkBuddy will ask before actions that leave the workspace or cross a higher-risk boundary.

<h2 id="first-task">Complete the First Task</h2>

Start with a Markdown file that is easy to inspect:

```text
Create hello-workbuddy.md in the current workspace. Include today's date, three practical notes about using WorkBuddy, and the sentence "SorryCode connection test complete." Do not modify any other files. Tell me the saved path when finished.
```

Check three things when it finishes:

- WorkBuddy returned a normal response
- `hello-workbuddy.md` exists in the selected folder
- the content is correct and no other files changed

This checks the model connection, tool calling, and workspace write access together. If WorkBuddy can chat but does not create the file, see [Connect WorkBuddy to SorryCode / Common Issues](/docs/runtime/workbuddy-sorrycode#common-issues).

<h2 id="next">What to Try Next</h2>

Increase complexity gradually after the first task succeeds:

- turn meeting notes into a Markdown or Word draft
- read a small spreadsheet and document its fields
- generate a rename preview for several test files, then execute only after review
- create a sourced report outline before drafting each section

Use copies or test folders first. For bulk rename, overwrite, delete, script, or external-service tasks, ask WorkBuddy to show the plan and affected files before execution.

<h2 id="boundaries">Boundaries</h2>

- WorkBuddy is the workbench; quality and available capabilities depend on the selected model
- custom model usage is billed through the selected SorryCode API key, not WorkBuddy's built-in model allowance
- local tasks do not continue when the computer is off or WorkBuddy is not running
- Default Permission reduces accidental changes but does not replace backups
- never paste an API key into a task, screenshot, document, or project file

Upstream references: [WorkBuddy website](https://www.workbuddy.cn/) and [WorkBuddy first-task guide](https://www.workbuddy.cn/docs/workbuddy/FirstTask).
