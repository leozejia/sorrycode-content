---
title: Switch SorryCode Models in Codex
slug: cc-switch
order: 1
summary: Use CC Switch to add non-GPT models from a SorryCode group to the Codex App model picker.
section: tools
section_title: Tools
section_order: 28
---

# Switch SorryCode Models in Codex

Codex App shows its bundled GPT models by default. Other models available through the current SorryCode group, such as DeepSeek, do not automatically appear in the model picker. SorryCode recommends CC Switch for managing this model catalog.

This guide uses one path: import SorryCode, fetch the models available to the current key in CC Switch, then restart Codex App.

<h2 id="install">Install CC Switch</h2>

Download CC Switch only from its [official repository](https://github.com/farion1231/cc-switch) or [GitHub Releases](https://github.com/farion1231/cc-switch/releases).

On macOS, you can also use Homebrew:

```bash
brew install --cask cc-switch
```

If CC Switch is already installed, update it first.

<h2 id="import">Import from SorryCode</h2>

1. Open the [SorryCode API Key page](https://sorrycode.com/keys)
2. Find the key you want to use with Codex
3. Click `Import to CCS`
4. Allow the system to open CC Switch and confirm the import

The import link contains the current key. Do not forward it, capture it in screenshots, or share it publicly.

<h2 id="models">Add Models from the Current Group</h2>

Open `CC Switch → Codex → SorryCode → Edit` and use these settings:

| Field | Value |
| --- | --- |
| API endpoint | `https://sorrycode.com` |
| Upstream format | `Responses (native)` |
| Default model | `deepseek-v4-flash` |

Expand the advanced options and click `Fetch Models` in the model mapping section. The current key group determines which models appear. To use DeepSeek, keep these entries:

```text
deepseek-v4-flash
deepseek-v4-pro
```

Save the provider, then enable SorryCode from the Codex provider list.

SorryCode already supports the Responses protocol used by Codex. This setup does not need CC Switch local routing, and CC Switch does not need to remain running in the background.

<h2 id="restart">Restart Codex App</h2>

Codex loads the model catalog at startup. Quit Codex App completely, reopen it, and start a new conversation. The model picker should now include `DeepSeek V4 Flash` and `DeepSeek V4 Pro`.

If they are missing, check that SorryCode is active, the model mapping was saved, and Codex App was fully restarted. If `Fetch Models` does not return DeepSeek, check the SorryCode group assigned to that key.
