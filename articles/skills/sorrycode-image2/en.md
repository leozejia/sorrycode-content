---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: Reuse the current SorryCode Codex key to generate or edit images with gpt-image-2-all or gpt-image-2 and save reproducible project files.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

Built-in image generation in Codex depends on the tools exposed by the current session. With a custom SorryCode provider, installing this Skill is the reliable path. See [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2) for the difference between this Skill, the Images API, and built-in Codex generation.

`SorryCode Image2` is for image tasks that need fixed outputs and a reproducible process. The agent finds the current SorryCode Codex key, calls the image endpoint, and saves the prompt, response, diagnostics, and image files inside the project.

For standard sizes, the Skill tries `gpt-image-2-all` first and then `gpt-image-2` when the first result is an explicit failure and retrying is safe. 2K and 4K sizes use `gpt-image-2`.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to complete the configuration and verification steps it can safely perform, then list anything that still needs your confirmation. If the agent can read web pages, you can send this page URL instead. Do not paste your API key into the conversation.

<h2 id="when-to-use">When to Use It</h2>

Install it when you need to:

- edit an existing local image
- choose an exact size and output folder
- save `prompt.txt`, `response.json`, or `events.ndjson`
- repeat the same image workflow inside a project

You can also generate directly in Codex when the current session explicitly exposes a built-in image tool.

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

<h2 id="api-key">Reuse the Codex Key</h2>

Complete [Models & Runtimes / Codex](/docs/runtime/codex) setup first. The Skill confirms the active SorryCode provider in the current Codex configuration and reads the key it already uses. You do not need a separate image key or a Skill-specific environment variable.

When you use the Skill from Claude Code, complete the SorryCode Codex setup on the same machine first. The agent reads that Codex configuration instead of creating another credential setup.

If the agent cannot find the key, return to `https://sorrycode.com/keys`, select the key you use for Codex, choose `Connect Tool`, and run the Codex connection command again. Do not paste the key into an agent conversation, save it in project files, or include it in screenshots.

Image requests always use the direct `https://api.sorrycode.com/v1` ingress.

<h2 id="first-prompt">First Prompt</h2>

Generate an image:

```text
Use SorryCode Image2 to generate a clean warm podcast cover about AI coding for beginners and save it to outputs/images/first-cover/.
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

- Key not found: run `Connect Tool > Codex` again from the API Key page, then rerun the Skill
- `401`: the current Codex key is no longer valid; reconnect Codex
- `403`: image generation is not enabled for the current Codex key's group
- `400`: check the input image, prompt, size, and model
- Request interrupted or timed out: do not immediately send another paid request; check the diagnostics and the previous request state first
- `503 No available compatible accounts`: the current Codex group has no compatible image account available right now

<h2 id="more-aigc">More AIGC Workflows</h2>

SorryCode Image2 handles generation and editing with `gpt-image-2-all` and `gpt-image-2`. For additional AIGC models, asset production, or dedicated visual asset workflows, use [SorryAssets](https://sorryassets.com).

<h2 id="next">Next Step</h2>

- Return to the OpenAI image overview: [Models & Runtimes / GPT Image 2](/docs/runtime/gpt-image-2)
- View the source: [linxiverse/sorrycode-image2](https://github.com/linxiverse/sorrycode-image2)
