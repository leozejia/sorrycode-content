---
title: Generate Images
slug: image-request
order: 6
summary: SorryCode offers two image paths: generate directly in a Codex App conversation, or install the SorryCode Image2 Skill for reproducible generation and editing tasks.
section: platform
section_title: Platform
section_order: 8
---

# Generate Images

SorryCode currently offers two ways to generate images. For a first run, ask for the image directly in `Codex App`. You do not need to learn API endpoints, model parameters, or shell commands first.

<h2 id="codex-app">Option 1: Generate Directly in Codex App</h2>

This is the default path for covers, posters, illustrations, avatars, and visual drafts.

After completing [Runtime / Codex](/docs/runtime/codex), say this in Codex App:

```text
Generate a clean warm podcast cover about AI coding for beginners. Keep the layout simple and leave enough room for a title.
```

You can continue with a revision:

```text
Make the title area wider, remove some decoration, and change it to a landscape layout.
```

This path is enough for most users.

<h2 id="image2-skill">Option 2: Use the SorryCode Image2 Skill</h2>

Install `SorryCode Image2` when you need to:

- edit an existing local image
- choose an output folder or exact size
- save the prompt, response, and streaming diagnostics
- repeat the same image workflow inside a project

`SorryCode Image2` currently uses only `gpt-image-2`. See:

- [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)

<h2 id="which-one">Which One Should You Use?</h2>

| Need | Use |
| --- | --- |
| First image or quick draft | Ask directly in Codex App |
| Continue revising the generated image | Continue the Codex App conversation |
| Edit a local image | SorryCode Image2 |
| Fixed size, folder, or saved diagnostics | SorryCode Image2 |
| Repeatable project workflow | SorryCode Image2 |

For additional AIGC models, asset production, or dedicated visual asset workflows, use [SorryAssets](https://sorryassets.com).

<h2 id="next">Next Step</h2>

- Need Codex first: [Runtime / Codex](/docs/runtime/codex)
- Need an advanced image workflow: [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- Need an API key: [Platform / Create API Key](/docs/platform/create-api-key)
