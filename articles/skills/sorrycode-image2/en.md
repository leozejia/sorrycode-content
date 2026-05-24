---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: Generate or edit covers, posters, illustrations, and content assets with SorryCode Images API; supports gpt-image-2 and enabled Gemini image models.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

`SorryCode Image2` is the skill for image generation and simple edits. It wraps the image request, API key check, and output saving flow, so you do not need to learn HTTP before your first image.

Use it for covers, posters, article images, product visual drafts, 2D game assets, or a first restyle of an existing image.

<h2 id="what-is-it">What It Solves</h2>

First-time image generation or editing usually gets stuck on three things:

- whether to call the generation or edit endpoint
- where to put the API key
- where the result should be saved and how to continue editing it

`SorryCode Image2` checks `SORRYCODE_API_KEY` first. If it is missing, it stops and guides you to create one. If the key exists, it calls SorryCode Images API. When you ask it to generate a new image, it uses `/v1/images/generations`; when you provide a local image path and ask it to edit that image, it uses `/v1/images/edits`. The skill saves the prompt, response records, and image output in your project.

Current default: start with `gpt-image-2` for common 1K / 2K images. Enabled Gemini image models can also be used through the same skill, but for a first run we recommend the default image model and `1024x1024`.

<h2 id="one-click-install">One-Click Install</h2>

First make sure `Codex` or `Claude Code` is installed.

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

If you have not installed a runtime yet, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

If you no longer need it, run `npx skills list --global` to confirm the name, then remove it with `npx skills remove --global sorrycode-image2`.

<h2 id="api-key">Let Your Computer Remember the Image API Key</h2>

`SorryCode Image2` needs an API key before it can generate or edit images. Think of it as the key for image tasks.

If you do not have an API key yet, go to [Platform / Create API Key](/docs/platform/create-api-key).

After you get the `sk-...` value, you can ask Codex or Claude Code to help set it up:

```text
Help me set my SorryCode image API key so it works in future sessions. My key is: sk-.... If this is Windows, use a user-level PowerShell setting. If this is macOS, write it to my zsh config. Before changing anything, tell me which file or setting you will update.
```

If you prefer doing it yourself, use one of these commands.

### Windows PowerShell, persistent

```powershell
[Environment]::SetEnvironmentVariable("SORRYCODE_API_KEY", "your sk-...", "User")
```

After setting it, close PowerShell and reopen Codex App or your terminal.

### macOS / Linux, persistent

```bash
echo "export SORRYCODE_API_KEY='your sk-...'" >> ~/.zshrc
source ~/.zshrc
```

Technical note: this sets `SORRYCODE_API_KEY`. It is only for SorryCode Image2 and does not change your Codex model configuration.

<h2 id="first-prompt">First Prompt</h2>

After installation, open Codex or Claude Code in your project and say:

```text
Use SorryCode Image2 to generate a clean warm Chinese podcast cover about AI coding for beginners. Check the API key first; if it is missing, tell me how to set it. If it succeeds, save the image and response to outputs/images/first-cover/.
```

Another example:

```text
Generate a 2D pixel-art game character wearing a blue jacket and small backpack, transparent background. Save it to outputs/images/game-character/.
```

If you already have an image, you can also say:

```text
Use SorryCode Image2 to edit ./input/product.png into a cleaner website hero visual. Keep the core UI shape, make the background calmer, and use softer lighting. Save it to outputs/images/product-hero/.
```

If you want a specific ratio or resolution, say it directly:

```text
Use SorryCode Image2 to generate a website hero landscape image with size 1536x1024.
```

`gpt-image-2` can use common sizes such as `1024x1024`, `1536x1024`, `1024x1536`, `2048x2048`, and `2048x1152`. For the first successful run, use `1024x1024`; 4K images are not the default recommendation yet.

<h2 id="what-it-saves">What It Saves</h2>

The recommended default folder is:

```text
outputs/images/your-task-name/
```

It should contain at least:

- `prompt.txt`
- `response.json` or `events.ndjson`
- the image file, or a note with the image URL

<h2 id="common-issues">Common Issues</h2>

- Missing `SORRYCODE_API_KEY`
  Create an API key from [Platform / Create API Key](/docs/platform/create-api-key), then let your computer remember it using the steps above
- `401`
  The API key is wrong or not sent as `Authorization: Bearer ...`
- `400`
  This usually means the image or parameters do not meet the requirements: the image is too small, the format is unsupported, the image is broken, or the model, prompt, or size is wrong. Follow the returned `message`; for image editing, first try a PNG / JPEG / WebP image that opens normally.
- `524`
  Usually means image generation waited too long. Reduce the size, shorten the prompt, or retry with the recommended parameters in [Platform / Image Request](/docs/platform/image-request#common-issues).
- `502`
  Does not always mean the platform is unavailable. Retry with recommended parameters; if it keeps failing, lower the resolution.
- `503 No available compatible accounts`
  The current API key cannot use this image model right now. Check the model name and key; if it still fails, contact SorryCode support.
- Slow generation
  Image generation is usually slower than text. If streaming events keep arriving, keep waiting

<h2 id="next">Next Step</h2>

For a guided task, go to [Village / Generate Your First Image](/docs/village/first-image).

For HTTP details, see [Platform / Image Request](/docs/platform/image-request).
