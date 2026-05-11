---
title: OpenClaw
slug: openclaw
order: 3
summary: Connect OpenClaw to SorryCode through its custom API path. Install the CLI first, then write the Base URL, model, and API key in one pass.
section: runtime
section_title: Runtime
section_order: 10
---

# OpenClaw

If you want to use `OpenClaw`, this page gives you the shortest stable path.

This page is an advanced custom connection path, not the beginner default.

If your goal is the best GPT cache, context, and cost behavior, use [Runtime / Codex](/docs/runtime/codex) first. `OpenClaw` can connect to the OpenAI-compatible gateway, but do not assume GPT usage through OpenClaw will be as cost-efficient as Codex.

The current recommendation is simple:

- install the OpenClaw CLI from the official docs
- use OpenClaw onboarding to point the default model path at SorryCode
- run one minimal validation

<h2 id="what-is-openclaw">What OpenClaw Is</h2>

- `OpenClaw` is a terminal agent / runtime built for code work
- it can read projects, edit files, run commands, and use custom model providers
- on SorryCode, the recommended path is the OpenAI-compatible gateway

For a first setup, you only need three values:

- Base URL: `{{API_BASE_URL}}`
- Model: `gpt-5.4`
- API Key: your `sk-...`

References:

- [OpenClaw Installation](https://docs.openclaw.ai/install)
- [OpenClaw Onboarding](https://docs.openclaw.ai/cli/onboard)
- [Configuration Reference](https://docs.openclaw.ai/gateway/configuration-reference)

<h2 id="recommended-path">Recommended Path Today</h2>

For a first setup, use this order:

1. Install `OpenClaw` from the official docs
2. Create an API key in SorryCode
3. Run `openclaw onboard` and write the `Base URL / Model / API Key`
4. Run one minimal validation

If `OpenClaw` is already installed on your machine, skip straight to the connection section below.

<h2 id="install-openclaw">Install OpenClaw</h2>

Use the official installation guide:

- [OpenClaw Installation](https://docs.openclaw.ai/install)

Then confirm the CLI is available:

```bash
openclaw --version
```

If that is still failing, fix the CLI install first. Do not start with provider config.

<h2 id="connect-sorrycode">Connect OpenClaw to SorryCode</h2>

The shortest path is OpenClaw's own onboarding flow with a custom API configuration.

### Write the SorryCode config directly

```bash
openclaw onboard \
  --non-interactive \
  --auth-choice custom-api-key \
  --custom-base-url "{{API_BASE_URL}}" \
  --custom-model-id "gpt-5.4" \
  --custom-api-key "your sk-..." \
  --secret-input-mode plaintext \
  --custom-compatibility openai
```

After that command finishes, OpenClaw will use SorryCode as its default model endpoint.

### If you prefer the interactive flow

Run:

```bash
openclaw onboard --install-daemon
```

Then fill in these values in the wizard:

- Base URL: `{{API_BASE_URL}}`
- Model ID: `gpt-5.4`
- API Key: your `sk-...`

If the wizard asks for a compatibility mode, choose `OpenAI`.

### If you already manage your own provider config

OpenClaw also supports manual config changes. The common paths are:

- `~/.openclaw/openclaw.json`
- `~/.openclaw/agents/<agentId>/agent/models.json`

Do not start there unless you already know you want that control. It is easier to get onboarding working first and tune the provider tree later. Field-level details are in the official [Configuration Reference](https://docs.openclaw.ai/gateway/configuration-reference).

<h2 id="create-api-key">Create API Key</h2>

If you do not have a `sk-...` key yet, do these 3 steps:

1. Sign in at `https://sorrycode.com/login`
2. Open `https://sorrycode.com/keys`
3. Create a new `sk-...` key and store it safely

The full explanation lives on [Platform / Create API Key](/docs/platform/create-api-key).

<h2 id="minimal-verification">Minimal Verification</h2>

The safer path is one minimal request before you throw a large project at the runtime. That verifies:

- the API key
- `{{API_BASE_URL}}`
- the OpenAI-compatible gateway path

Use the OpenAI-compatible example on [Platform / First Request](/docs/platform/first-request).

Once that passes, go back to your project and launch OpenClaw there.

<h2 id="next">Next</h2>

- Want the API key details: [Platform / Create API Key](/docs/platform/create-api-key)
- Want the gateway check first: [Platform / First Request](/docs/platform/first-request)
- Want the shared error page: [Troubleshoot / Common Questions](/docs/troubleshoot/common-errors)
