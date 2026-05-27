---
title: Common Questions
slug: common-errors
order: 1
summary: The shortest fix path by error code and symptom.
section: troubleshoot
section_title: Troubleshoot
section_order: 50
---

# Common Questions

## 401 Unauthorized

Check these first:

- is the API key complete
- is the auth header correct
- did you mix a SorryCode key with an upstream official key

Protocol differences matter too:

- OpenAI-compatible usually uses `Authorization: Bearer ...`
- Anthropic-compatible usually uses `x-api-key: ...`

## 404 Not Found

The most common causes are:

- `/v1` is missing from the Base URL
- the route is wrong
- you mixed an OpenAI-compatible path with an Anthropic-compatible path

## 429 / quota problems

Separate the cause first:

- no balance left
- rate limiting
- too much concurrency in a short window

If you are only validating the path, reduce frequency and concurrency first.

## Timeout / TLS errors

Start with:

- [Environment / Node.js](/docs/environment/nodejs#network)

## PowerShell execution policy errors

Start with:

- [Environment / Windows PowerShell](/docs/environment/windows-powershell)

## Not sure where to look first

Go back to:

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)
