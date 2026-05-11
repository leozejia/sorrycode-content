---
title: Hermes Agent
slug: hermes-agent
order: 4
summary: Connect Hermes Agent to SorryCode through the custom endpoint path. Use the official install flow on macOS or Linux, and follow the upstream WSL2 route on Windows.
section: runtime
section_title: Runtime
section_order: 10
---

# Hermes Agent

If you want to use `Hermes Agent` with SorryCode, this page gives you the shortest stable path.

One support detail is already confirmed here: the SorryCode gateway path has been validated with `Hermes Agent`.

Keep the platform story simple:

- `macOS / Linux` is the shortest path
- `Windows` should follow the upstream `WSL2` route

More importantly, this page is an advanced custom connection path, not the beginner default. If your goal is the best GPT cache, context, and cost behavior, use [Runtime / Codex](/docs/runtime/codex) first. `Hermes Agent` can connect to the OpenAI-compatible gateway, but do not assume GPT usage through Hermes will be as cost-efficient as Codex.

<h2 id="what-is-hermes-agent">What Hermes Agent Is</h2>

- `Hermes Agent` is Nous Research's terminal agent / runtime
- it supports provider runtimes and custom endpoints
- on SorryCode, the recommended path is the OpenAI-compatible gateway through `Custom endpoint`

For a first setup, you still only need three values:

- Base URL: `{{API_BASE_URL}}`
- Model: `gpt-5.4`
- API Key: your `sk-...`

References:

- [Hermes Agent Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation)
- [Provider Runtime](https://hermes-agent.nousresearch.com/docs/developer-guide/provider-runtime/)
- [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration/)

<h2 id="recommended-path">Recommended Path Today</h2>

For a first setup, use this order:

1. Install `Hermes Agent` from the official docs, with `WSL2` on Windows
2. Create an API key in SorryCode
3. Run `hermes model` and choose `Custom endpoint`
4. Fill in `Base URL / Model / API Key`, then run one minimal validation

If `Hermes Agent` is already installed, skip straight to the connection section below.

<h2 id="install-hermes-agent">Install Hermes Agent</h2>

### macOS / Linux

Use the official installation guide:

- [Hermes Agent Installation](https://hermes-agent.nousresearch.com/docs/getting-started/installation)

Then confirm the CLI is available:

```bash
hermes --version
```

### Windows

Follow the upstream `WSL2` path.

That is the safer recommendation here. The runtime itself is more Linux-shaped upstream, and `WSL2` is the shorter path to a setup that behaves like the official docs.

<h2 id="connect-sorrycode">Connect Hermes Agent to SorryCode</h2>

The shortest path is:

```bash
hermes model
```

In the wizard, choose `Custom endpoint`, then fill in:

- Base URL: `{{API_BASE_URL}}`
- Model: `gpt-5.4`
- API Key: your `sk-...`
- Context length: leave it blank and let Hermes detect it

For a first setup, this is safer than editing config files by hand.

### If you prefer to write config directly

Use the official custom provider model and write:

```yaml
model:
  provider: custom
  default: gpt-5.4
  base_url: {{API_BASE_URL}}
  api_key: your sk-...
```

If you want multiple custom endpoints later, extend it with the official `custom_providers` syntax. Do not start there unless you need it.

<h2 id="create-api-key">Create API Key</h2>

If you do not have a `sk-...` key yet, do these 3 steps:

1. Sign in at `https://sorrycode.com/login`
2. Open `https://sorrycode.com/keys`
3. Create a new `sk-...` key and store it safely

The full explanation lives on [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="minimal-verification">Minimal Verification</h2>

The safer path is still one minimal request first. That verifies:

- the API key
- `{{API_BASE_URL}}`
- the OpenAI-compatible gateway path

Use the OpenAI-compatible example on [Platform / First Request](/docs/platform/first-request).

Once that passes, go back to your project and launch `Hermes Agent`.

<h2 id="next">Next</h2>

- Want the API key details: [Platform / Create API Key](/docs/platform/create-api-key)
- Want the gateway check first: [Platform / First Request](/docs/platform/first-request)
- Want the shared error page: [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
