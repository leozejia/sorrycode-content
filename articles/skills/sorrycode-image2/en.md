---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: Generate or edit images with gpt-image-2 while saving prompts, responses, diagnostics, and image files for reproducible project workflows.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

If you only need a quick image, ask for it directly in `Codex App`. You do not need to install a Skill first. See [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2) for the full split between natural-language generation, the Images API, and this Skill.

`SorryCode Image2` is for image tasks that need fixed outputs and a reproducible process. It checks the API key, calls the image endpoint, and saves the prompt, response, diagnostics, and image files inside the project.

The only supported model is `gpt-image-2`.

<h2 id="when-to-use">When to Use It</h2>

Install it when you need to:

- edit an existing local image
- choose an exact size and output folder
- save `prompt.txt`, `response.json`, or `events.ndjson`
- repeat the same image workflow inside a project

For a first image or a quick revision, a normal Codex App conversation is simpler.

<h2 id="one-click-install">Install</h2>

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

If you still need a workbench, start here:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

Before uninstalling, run `npx skills list --global` to confirm the name, then use `npx skills remove --global sorrycode-image2`.

<h2 id="api-key">Set the Image API Key</h2>

The Skill reads `SORRYCODE_API_KEY`. If you do not have an API key, go to [Getting Started / Create API Key](/docs/start/create-api-key).

You can give this instruction to Codex or Claude Code:

```text
Help me set my SorryCode image API key so it works in future sessions. My key is: sk-.... On Windows, use a user-level PowerShell setting. On macOS, write it to my zsh configuration. Tell me what you will change before making the change.
```

Windows PowerShell:

```powershell
[Environment]::SetEnvironmentVariable("SORRYCODE_API_KEY", "your sk-...", "User")
```

macOS / Linux:

```bash
echo "export SORRYCODE_API_KEY='your sk-...'" >> ~/.zshrc
source ~/.zshrc
```

This variable is only for SorryCode Image2. It does not change the Codex model configuration.

<h2 id="first-prompt">First Prompt</h2>

Generate an image:

```text
Use SorryCode Image2 to generate a clean warm podcast cover about AI coding for beginners. Use gpt-image-2 and save it to outputs/images/first-cover/.
```

Edit an image:

```text
Use SorryCode Image2 to edit ./input/product.png. Keep the core interface shape, simplify the background, and soften the lighting. Save it to outputs/images/product-hero/.
```

Choose a size:

```text
Use SorryCode Image2 to generate a website hero image at 1536x1024 and save it to outputs/images/website-hero/.
```

Common sizes include `1024x1024`, `1536x1024`, and `1024x1536`. Use `1024x1024` for the first run.

<h2 id="what-it-saves">What It Saves</h2>

The recommended output location is:

```text
outputs/images/your-task-name/
```

The folder normally contains:

- `prompt.txt`
- `request.json`
- `response.json` or `events.ndjson`
- the generated or edited image file

<h2 id="common-issues">Common Issues</h2>

- Missing `SORRYCODE_API_KEY`: create an API key, then reopen the workbench or terminal
- `401`: the API key is wrong or was not set correctly
- `400`: check the input image, prompt, size, and model; the model must be `gpt-image-2`
- `524`: reduce the image size, shorten the prompt, or retry later
- `503 No available compatible accounts`: the current API key cannot use the image model right now; check access or retry later

<h2 id="more-aigc">More AIGC Workflows</h2>

SorryCode Image2 only handles generation and editing with `gpt-image-2`. For additional AIGC models, asset production, or dedicated visual asset workflows, use [SorryAssets](https://sorryassets.com).

<h2 id="next">Next Step</h2>

- Return to the OpenAI image overview: [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2)
- View the source: [linxiverse/sorrycode-image2](https://github.com/linxiverse/sorrycode-image2)
