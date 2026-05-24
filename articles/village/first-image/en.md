---
title: Generate Your First Image
slug: first-image
order: 2
summary: Install the SorryCode Image2 skill first, then generate your first cover, poster, or illustration with gpt-image-2.
section: village
section_title: Village
section_order: 18
group: content-creation
group_title: Content Creation
group_order: 30
---

# Generate Your First Image

<h2 id="goal">Goal</h2>

Use `SorryCode Image2` to generate your first image and save the result in your project.

You do not need to understand HTTP, parameters, or image endpoints first. The default path is to install the skill and let it check your API key, call the image model, and save the prompt, response record, and image result.

<h2 id="prepare">What You Need</h2>

- [Codex](/docs/runtime/codex) or [Claude Code](/docs/runtime/claude-code) installed
- [Skills / SorryCode Image2](/docs/skills/sorrycode-image2) installed
- a SorryCode API key
- one image idea

If you do not have an API key yet, start with [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="install-skill">Install the Image Skill First</h2>

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

If you no longer need this skill later, see the view and remove section in [Skills / What Are Skills](/docs/skills/featured-skills).

<h2 id="set-key">Let Your Computer Remember the Image API Key</h2>

The easiest path is to ask the agent to set it up for you. Copy this into Codex or Claude Code:

```text
Help me set my SorryCode image API key so it works in future sessions. My key is: sk-.... If this is Windows, use a user-level PowerShell setting. If this is macOS, write it to my zsh config. Before changing anything, tell me which file or setting you will update.
```

If the key is missing, `SorryCode Image2` should stop and explain what to do instead of pretending to generate an image.

Technical note: the agent sets `SORRYCODE_API_KEY`. This name is only for the image skill and does not change your Codex model configuration.

<h2 id="steps">Steps</h2>

1. Install `SorryCode Image2`
2. Let your computer remember the image API key
3. Open Codex or Claude Code in your project
4. Copy the prompt below
5. Confirm the result is saved to `outputs/images/first-cover/`

<h2 id="prompt">Copy This</h2>

```text
Use SorryCode Image2 to generate a clean warm Chinese podcast cover about AI coding for beginners. Check the API key first; if it is missing, tell me how to set it. If it succeeds, save the image, prompt, and response/events to outputs/images/first-cover/.
```

<h2 id="done">Completion Check</h2>

You have completed the task if:

- the skill did not get stuck on the API key
- the request succeeded
- `outputs/images/first-cover/` contains the prompt and response or events
- you can open or download the generated result

<h2 id="stuck">If You Get Stuck</h2>

If `SORRYCODE_API_KEY` is missing, go back to the setup step above and let your computer remember the image API key.

If you see `401`, check that the key is complete. It usually starts with `sk-...`.

If you see `503 No available compatible accounts`, the current API key cannot use this image model right now. Check the model name and key; if it still fails, contact SorryCode support.

If the request is slow, wait for a while first. If you see `524`, read [Platform / Image Request](/docs/platform/image-request#common-issues) and follow the recommended image request parameters there.

<h2 id="next">Next Level</h2>

To keep playing, use the image in a product intro, long article, or sharing deck.

To understand the HTTP details, see [Platform / Image Request](/docs/platform/image-request).
