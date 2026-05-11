# SorryCode Content

Public, reviewed Markdown content for SorryCode remote docs experiments.

This repository is not a CMS. It stores publishable `md + png` content that SorryCode can fetch, cache, sanitize, and render inside the existing docs system.

## Structure

```text
index.json
articles/
  codex-history/
    zh.md
    cover.png
```

## Rules

- Only publish reviewed public content.
- Do not commit tokens, private screenshots, provider credentials, account data, or generation diagnostics.
- Keep production notes, prompts, request/response logs, and candidate images in the media workspace, not here.
- Core product docs still live in the main `sorrycode` repository.
