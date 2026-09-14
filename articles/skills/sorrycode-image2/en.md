---
title: SorryCode Image2
slug: sorrycode-image2
order: 5
summary: A reusable Agent Skill for generating or editing GPT Image 2 and GPT Image 2.5 images through SorryCode, with saved outputs and completion checks.
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: Creation and Design
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

`SorryCode Image2` is an image Skill for Codex and Claude Code. It gives the agent a reusable path for image requests, key setup, saved outputs, and completion checks.

Use it when you want to:

- generate covers, posters, illustrations, or product visuals
- edit an existing PNG, JPEG, or WebP image
- choose a model, size, quality, or output directory explicitly
- have the agent verify that the saved image can actually be read

If you only want to call the Images API yourself, read [GPT Image 2](/docs/runtime/gpt-image-2) or [GPT Image 2.5](/docs/runtime/gpt-image-2-5). Install this Skill when you want the agent to execute the request and save the result for you.

> **Let Your Agent Configure It**
>
> Click `Copy Markdown` in the upper-right and send the content to the agent you are using. Ask it to install the Skill, configure the key, and run one minimal image verification based on this page, then list anything that still needs your confirmation. Do not paste an API key into the conversation.

<h2 id="install">Install</h2>

Install [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code) first, then run:

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -a claude-code -g -y
```

Native plugin installation is also supported:

```text
codex plugin marketplace add linxiverse/sorrycode-image2
codex plugin add sorrycode-image2@sorrycode-image2
```

After installation, ask the agent to reload or inspect the currently available Skills. Do not copy the repository README into project instruction files.

<h2 id="key">Configure the Image2 Key</h2>

Create or select a key on the [API Key page](https://sorrycode.com/keys). Its group must be able to access the image model you plan to use. GPT Image 2 and GPT Image 2.5 use the OpenAI / Codex group, so do not substitute a Grok-group key.

Ask the agent to locate the installed `sorrycode-image2` Skill and run its bundled configurator:

```bash
node /path/to/sorrycode-image2/scripts/configure-key.mjs
```

The configurator hides input and writes the key to `.env` beside the installed Skill. The variable name is:

```text
SORRYCODE_IMAGE2_API_KEY
```

This `.env` belongs only to the Skill. It is user-readable and user-writable, and it is not written to Git, project files, or diagnostics. If a reinstall replaces the whole Skill directory, run the configurator again. You can also provide the same variable in the process environment; it takes precedence over the Skill-local `.env`.

Do not put the key in prompts, screenshots, project files, or shell history. Direct API calls do not need this Skill-specific variable; use the Bearer Token shown in the model guide instead.

<h2 id="use">Use It After Installation</h2>

Name the Skill and describe the image and output path:

```text
Use SorryCode Image2 to generate a warm Chinese podcast cover about AI coding for beginners. Leave a clear area for the title and save it to outputs/images/podcast-cover/.
```

Edit an existing image:

```text
Use SorryCode Image2 to edit ./input.png. Change the background to light blue, preserve the subject and existing text, and save the result to outputs/images/edited-cover/.
```

If you need a specific model, size, or quality, say so directly:

```text
Use SorryCode Image2 with the explicit gpt-image-2 model. Generate a blue circle on a clean white 1024x1024 background and save it to outputs/images/blue-circle/.
```

The Skill defaults are:

| Task | Default model or behavior |
| --- | --- |
| New image generation | `gpt-image-2.5-flare`, `quality: auto` |
| Image editing | `gpt-image-2.5-sunburst`, `quality: auto` |
| Explicit `gpt-image-2` | Streaming enabled by default, with the final image saved |

These are defaults and examples, not a local model allowlist. An explicit `--model` value is passed to the API unchanged. The API decides whether the model exists, whether the key has access, and which parameters it supports.

<h2 id="result">Output and Saving</h2>

When no path is supplied, the result is saved under:

```text
outputs/images/<short-slug>/
```

The Skill saves a request summary, necessary diagnostics, and the final image. Partial images in a stream are previews; the final image is saved after completion. Before reporting success, the agent should confirm that the target file exists, has the expected format, and can be opened.

If a request is interrupted, times out, or fails while downloading the result, do not immediately submit it again. The previous paid request may still be processing, so check its state first.

<h2 id="boundaries">Boundaries</h2>

- This Skill generates and edits images through the SorryCode Images API. It does not handle Grok images or videos.
- Edit inputs can be PNG, JPEG, or WebP.
- It sends one paid request at a time and does not switch keys, models, or applications automatically.
- For video, read [Grok Video Generation](/docs/runtime/grok-video).
- For manual request formats and the full Images API guidance, read [GPT Image 2](/docs/runtime/gpt-image-2) and [GPT Image 2.5](/docs/runtime/gpt-image-2-5).

<h2 id="troubleshoot">Common Issues</h2>

- No key found: run the bundled `configure-key.mjs`; do not paste the key into chat.
- `401`: check the key and confirm that the request uses a Bearer Token.
- `403`: the current key group does not include the requested image capability. Choose a matching group on the API Key page.
- `400`: check the model ID, prompt, size, quality, and input image format.
- Timeout or interrupted connection: do not retry automatically; check the previous request state first.

<h2 id="references">References</h2>

- [GPT Image 2](/docs/runtime/gpt-image-2): Images API, streaming, and edit requests for `gpt-image-2`
- [GPT Image 2.5](/docs/runtime/gpt-image-2-5): model selection and parameters for Flare and Sunburst
- [SorryCode Image2 repository](https://github.com/linxiverse/sorrycode-image2): the install package and latest scripts
