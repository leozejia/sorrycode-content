---
title: Grok
slug: grok-cli
order: 4
summary: Install Grok and connect it to SorryCode with a custom model config.
section: runtime
section_title: Runtime
section_order: 10
---

# Grok

If you want to use xAI's `grok` command as a local agent while sending requests through SorryCode, this is the shortest path.

You can copy the one-click Grok installer from `Connect Tool` in the SorryCode console. If your page has not refreshed to the new entry yet, use the manual setup below.

<h2 id="prepare-api-key">Prepare Your API Key</h2>

1. Log in to the SorryCode console
2. Open `API Keys`
3. Create a new `sk-...` key if you do not have one
4. Make sure the key can use a Grok group

Quick link: `https://sorrycode.com/keys`.

If you have not created an API key before, start with [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="install">Install Grok</h2>

macOS / Linux / WSL:

```bash
curl -fsSL https://x.ai/cli/install.sh | bash
```

Windows PowerShell:

```powershell
irm https://x.ai/cli/install.ps1 | iex
```

After install, reopen your terminal and make sure the `grok` command is available.

<h2 id="connect-sorrycode">Connect To SorryCode</h2>

macOS / Linux / WSL:

```bash
mkdir -p ~/.grok
cat > ~/.grok/config.toml <<'EOF'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "https://api.sorrycode.com/v1"
name = "SorryCode Grok"
env_key = "SORRYCODE_API_KEY"

[models]
default = "sorrycode-grok"
EOF

export SORRYCODE_API_KEY="sk-your-sorrycode-key"
grok
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.grok" | Out-Null

$config = @'
[model.sorrycode-grok]
model = "grok-4.5"
base_url = "https://api.sorrycode.com/v1"
name = "SorryCode Grok"
env_key = "SORRYCODE_API_KEY"

[models]
default = "sorrycode-grok"
'@

[System.IO.File]::WriteAllText(
  "$env:USERPROFILE\.grok\config.toml",
  $config,
  [System.Text.UTF8Encoding]::new($false)
)

$env:SORRYCODE_API_KEY = "sk-your-sorrycode-key"
grok
```

Replace `sk-your-sorrycode-key` with your own SorryCode API key.

<h2 id="start">Start Grok</h2>

If `sorrycode-grok` is your default model, run:

```bash
grok
```

If you keep multiple Grok configs, specify this one explicitly:

```bash
grok -m sorrycode-grok
```

<h2 id="notes">Notes</h2>

- Set `base_url` to `https://api.sorrycode.com/v1`, not the official xAI API URL.
- Set `SORRYCODE_API_KEY` to your SorryCode `sk-...` key, not xAI account credentials.
- Keep `model` as `grok-4.5`.
- Do not use the xAI browser login path for SorryCode. SorryCode uses API keys and custom model config.
