# SorryCode Content

Public, reviewed article content for SorryCode remote docs experiments.

This repository is not an internal docs folder and not a CMS. It stores publishable `md + png` articles that SorryCode can fetch, cache, sanitize, and render inside the existing docs experience.

## Structure

```text
index.json
articles/
  tools/
    index.json
    cc-switch/
      zh.md
      en.md
    codex-history/
      zh.md
      en.md
      cover.png
```

## Current Scope

The first migration scope is public `Tools` articles.

Core product docs such as `Runtime`, `Platform`, `Skills`, `Agent Infrastructure`, `Environment`, and `Troubleshoot` still live in the main `sorrycode` repository.

## Rules

- Use `articles/<section>/<slug>/<locale>.md` for public article content.
- Keep one public article per locale file.
- Put public assets next to the article that uses them.
- Keep `index.json` as the root machine-readable content index.
- Optional section indexes such as `articles/tools/index.json` may mirror filtered entries for humans and simple loaders.
- Do not commit tokens, private screenshots, provider credentials, account data, or generation diagnostics.
- Keep production notes, prompts, request/response logs, and candidate images in the media workspace, not here.
- Remote content still must be sanitized and rendered through the main SorryCode docs renderer.
