---
title: WorkBuddy Permissions and Workspaces
slug: workbuddy-permissions
order: 3
summary: Understand Default Permission, Full Access, and workspace boundaries before letting WorkBuddy modify local files.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy Permissions and Workspaces

WorkBuddy is more than a chat app. It can read and write local files and may call scripts or external programs. Choosing the right workspace and keeping Default Permission enabled matters more than writing a long prompt.

<h2 id="workspace">What a Workspace Is</h2>

A workspace is the folder WorkBuddy primarily reads and writes for the current task. Click `Select Workspace` below the input box on the `New Task` screen.

Use a separate folder for each task type:

```text
WorkBuddy-Tasks/
  meeting-notes/
  spreadsheet-cleanup/
  report-draft/
```

Place only copies of the files needed for this task in that folder. For a first task, do not select your whole Desktop, Downloads folder, home directory, production project, or the only copy of important material.

<h2 id="default-permission">Default Permission</h2>

`Default Permission` is the recommended mode for everyday work. WorkBuddy operates inside its safety sandbox and asks before actions that leave the normal boundary or carry higher risk.

Pay particular attention to requests involving:

- writing outside the workspace
- deleting, overwriting, or bulk-moving files
- running scripts, commands, or external programs
- network access or sensitive configuration
- credentials, keys, or system directories

Before approving, inspect the action, target path, and affected scope. If anything is unclear, cancel and ask WorkBuddy to show the file list, rename preview, script, or rollback method first.

<h2 id="full-access">When Full Access Is Appropriate</h2>

`Allow Full Access` reduces or skips step-by-step confirmation for risky operations. It does not make the model smarter; it gives the model more direct control.

Use it briefly only when all of these are true:

- the task runs in an isolated, disposable test folder
- every input has a copy or version-control history
- you understand the scripts and commands involved
- a wrong execution cannot affect production data, personal files, or system configuration

Switch back to Default Permission when the task is complete.

Do not enable Full Access in folders containing customer data, financial files, unique originals, production projects, your home directory, or credentials.

<h2 id="safe-prompt">Preview Before Execution</h2>

For bulk work, begin with:

```text
Do not modify files yet. Inspect the current workspace and list the planned steps, affected files, before-and-after changes, and rollback method. Wait for my confirmation before execution.
```

For bulk rename:

```text
Create a table of old and proposed filenames first. Do not rename anything yet. List duplicates, unrecognized files, and format anomalies separately instead of guessing.
```

For document generation:

```text
Write the result to a new file and do not overwrite the source. Report the output path and anything you did not process.
```

<h2 id="backup">Backups and Rollback</h2>

Default Permission is not a backup system. Before important work, do at least one of these:

- copy input files into a test folder
- use Git or cloud-drive version history
- ask WorkBuddy to create a new output instead of overwriting the source
- save a before-and-after map before bulk changes

WorkBuddy backup behavior can vary by operating system and release. Do not use it as the only rollback mechanism.

<h2 id="credentials">Keep Credentials Out of Workspaces</h2>

Store the API key in WorkBuddy model settings. Do not put it in a task prompt, Markdown file, spreadsheet, screenshot, or project file.

If a workspace contains `.env` files, certificates, SSH keys, payment data, or customer information, remove them or use sanitized copies. Before installing a third-party Skill, inspect its source, scripts, and requested data access.

<h2 id="recommended-default">Recommended Defaults</h2>

| Scenario | Permission | Workspace |
| --- | --- | --- |
| First use | Default Permission | new empty test folder |
| Documents, spreadsheets, and source organization | Default Permission | copies needed for this task only |
| Bulk rename or move | Default Permission | preview first and save a mapping |
| Repeated trusted script | Default Permission; temporary Full Access only in isolation | disposable test folder |
| Production material or unique originals | Default Permission | avoid direct modification in WorkBuddy |

Upstream reference: [WorkBuddy Default Permission and Safety Sandbox](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Permission-Modes).
