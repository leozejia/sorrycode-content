# SorryCode Content

Public, reviewed Markdown content for SorryCode remote docs experiments.

This repository mirrors the public docs information architecture instead of the media-production article layout. It is not a CMS. It stores publishable `md + png` content that SorryCode can fetch, cache, sanitize, and render inside the existing docs system.

## Structure

```text
index.json
docs/
  tools/
    cc-switch/
      zh.md
      en.md
    codex-history/
      zh.md
      cover.png
```

## Current Scope

The first migration scope is `Tools`.

Core product docs such as `Runtime`, `Platform`, `Skills`, `Agent Infrastructure`, `Environment`, and `Troubleshoot` still live in the main `sorrycode` repository.

## Rules

- Mirror SorryCode docs routes as `docs/<section>/<slug>/<locale>.md`.
- Keep one public document per locale file.
- Put public assets next to the document that uses them.
- Do not commit tokens, private screenshots, provider credentials, account data, or generation diagnostics.
- Keep production notes, prompts, request/response logs, and candidate images in the media workspace, not here.
- Remote content still must be sanitized and rendered through the main SorryCode docs renderer.
