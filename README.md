# SorryCode Content

Public article content and internal content-governance notes for SorryCode docs.

This repository is not a CMS. It stores publishable Markdown articles and public image assets that SorryCode can fetch, cache, sanitize, and render inside the existing docs experience. It may also contain internal editorial notes under `docs/`; SorryCode does not fetch or render those files.

## Structure

```text
index.json
docs/
  information-architecture.md
  operator-restructuring-guide.md
  presentation-skills-strategy.md
articles/
  runtime/
    index.json
    codex-plugins/
      zh.md
      en.md
      cover.png
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

This repository can carry public docs for these sections:

- `start`
- `platform`
- `runtime`
- `skills`
- `village`
- `tools`
- `agent-infra`
- `environment`
- `troubleshoot`

The main `sorrycode` repository still owns routing, backend caching, asset proxying, fallback behavior, sanitization, Markdown rendering, and release experience.

## Public vs Internal

Only these paths are part of the public remote content contract:

- `index.json`
- `articles/<section>/index.json`
- `articles/<section>/<slug>/<locale>.md`
- public assets stored next to an article, such as `cover.png`

`docs/` is for internal content governance: IA decisions, page contracts, inclusion criteria, and maintenance notes. It is not part of the public content index and must not be referenced by `markdownPath`, `assetBaseUrl`, or `coverPath`.

## Internal Reading Order

For major content restructuring, read these first:

1. `docs/operator-restructuring-guide.md`
2. `docs/information-architecture.md`
3. Any relevant topic strategy, such as `docs/presentation-skills-strategy.md`

If a public name, slug, directory path, category, or route is conceptually wrong, restructure it with a hard cut. Do not keep old paths just for compatibility.

## Rules

- Use `articles/<section>/<slug>/<locale>.md` for public article content.
- Keep one public article per locale file.
- Put public assets next to the article that uses them.
- Keep `index.json` as the root machine-readable content index.
- Keep section indexes such as `articles/<section>/index.json` for curated navigation.
- Do not commit tokens, private screenshots, provider credentials, account data, or generation diagnostics.
- Keep production notes, prompts, request/response logs, and candidate images in the media workspace, not here.
- Remote content still must be sanitized and rendered through the main SorryCode docs renderer.

## Root Index Schema

`index.json` has this shape:

```json
{
  "version": 4,
  "kind": "sorrycode-content-index",
  "updatedAt": "2026-05-11",
  "articles": []
}
```

Each article entry must include:

- `type`
- `section`
- `sectionTitle`
- `sectionOrder`
- `slug`
- `locale`
- `title`
- `summary`
- `order`
- `updatedAt`
- `markdownPath`
- `assetBaseUrl`
- `route`

Optional fields:

- `sourceUrl`
- `coverPath`

Paths must stay inside the same article directory:

```text
articles/<section>/<slug>/<locale>.md
articles/<section>/<slug>/<asset-file>
```

Do not point one article entry at another article's Markdown or assets.

## Section Index Schema

Each section may have:

```text
articles/<section>/index.json
```

The section index controls curated navigation. Single-article frontmatter does not decide section IA by itself.
For grouped navigation, `navigation.groups[].items` is the rendered article order inside that group.

```json
{
  "version": 1,
  "section": "runtime",
  "title": {
    "zh": "Runtime",
    "en": "Runtime"
  },
  "updatedAt": "2026-05-11",
  "navigation": {
    "style": "flat",
    "groups": []
  },
  "articles": ["codex", "codex-plugins"]
}
```
