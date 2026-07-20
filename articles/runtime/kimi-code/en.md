---
title: Kimi Code
slug: kimi-code
order: 1
summary: Configure Kimi Code with a SorryCode Kimi-group API key and use K3 or another Kimi model available to that key.
section: runtime
section_title: Models & Runtimes
section_order: 10
group: kimi
group_title: Kimi
group_order: 25
---

# Kimi Code

Kimi Code is a terminal coding agent. It can read projects, edit files, run commands, and execute one-off tasks in non-interactive mode.

This page configures the model provider used by Kimi Code. The API key comes from SorryCode and model requests go through SorryCode. The Kimi account and `/login` flow are not used on this path.

Reference: [Kimi Code getting started](https://www.kimi.com/code/docs/en/kimi-code-cli/guides/getting-started.html)

<h2 id="prepare-api-key">Prepare a Kimi-Group API Key</h2>

1. Open `https://sorrycode.com/keys`
2. Create a new API key
3. Select a group that supports Kimi
4. Keep this key separate from keys used for Codex, Claude Code, Grok, or Image2

Query the models available to this key before editing the Kimi Code config:

```bash
curl https://sorrycode.com/v1/models \
  -H "Authorization: Bearer <your Kimi-group API key>"
```

The `model` field used later must match an ID returned by this endpoint. Common IDs currently include `k3`, `kimi-for-coding`, and `kimi-for-coding-highspeed`, but the response for your key is the source of truth.

<h2 id="install">Install Kimi Code</h2>

macOS / Linux:

```bash
curl -fsSL https://code.kimi.com/kimi-code/install.sh | bash
```

Windows PowerShell:

```powershell
irm https://code.kimi.com/kimi-code/install.ps1 | iex
```

Check that the command is available:

```bash
kimi --version
```

<h2 id="configure">Add the SorryCode Provider</h2>

The config file is stored at:

- macOS / Linux: `~/.kimi-code/config.toml`
- Windows: `%USERPROFILE%\.kimi-code\config.toml`

If the file already contains other providers, merge the following block instead of replacing the whole file. Set `api_key` to the Kimi-group key you created:

```toml
default_model = "sorrycode/kimi"

[providers.sorrycode-kimi]
type = "kimi"
base_url = "https://sorrycode.com/v1"
api_key = "<your Kimi-group API key>"

[models."sorrycode/kimi"]
provider = "sorrycode-kimi"
model = "k3"
max_context_size = 1048576
capabilities = ["thinking", "always_thinking", "image_in", "video_in", "tool_use"]
display_name = "K3 via SorryCode"
support_efforts = ["max"]
default_effort = "max"
```

`sorrycode/kimi` is a local alias and can be renamed. `model = "k3"` is the ID sent to SorryCode. If the group does not expose `k3`, replace it with a model returned by `/v1/models` and adjust `max_context_size` and capabilities to match that model.

Kimi Code stores `api_key` as plain text in the local config. Do not commit this file to Git or share screenshots that expose the key. On macOS / Linux, restrict its permissions:

```bash
chmod 600 ~/.kimi-code/config.toml
```

<h2 id="verify">Verify the Configuration</h2>

Check the config and provider first:

```bash
kimi doctor
kimi provider list
```

Then send a minimal request:

```bash
kimi -m "sorrycode/kimi" -p "Reply with exactly: sorrycode-kimi-ok"
```

Once the model responds, the Kimi Code client, SorryCode key, group, and model are connected.

<h2 id="start">Start Using Kimi Code</h2>

Enter a project directory and run:

```bash
cd <your-project-directory>
kimi
```

A safe first prompt is:

```text
Inspect this project's directory structure without changing files. Tell me where the entry point is and which files I should read first.
```

Use `-m` to select a model for one invocation. Inside the interactive UI, use `/model` to switch between configured models.

<h2 id="boundaries">Configuration Boundaries</h2>

- Do not use `/login` for SorryCode. It is for Kimi OAuth and official platform keys.
- Do not rely on a shell-level `KIMI_API_KEY`. Ordinary providers do not read it automatically.
- Do not point `KIMI_CODE_BASE_URL` at SorryCode. That setting belongs to Kimi's OAuth managed service.
- Do not configure Kimi's official `/search` or `/fetch` services under SorryCode. This page configures only the model provider.

<h2 id="common-issues">Common Issues</h2>

- `401`: check that the key is complete and still active
- `404` or model not found: query `/v1/models` again and use the exact model ID
- `missing credentials`: make sure `api_key` is inside `[providers.sorrycode-kimi]`
- no available account or group: select a Kimi-capable group for this API key
- config parse failure: run `kimi doctor` and check for duplicate TOML fields

For shared error guidance, read [Troubleshooting / Common Questions](/docs/troubleshoot/common-errors).
