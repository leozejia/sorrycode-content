---
title: Manual Cursor Setup
slug: cursor
order: 3
summary: Treat Cursor editor separately from Magpie and retain the manual custom URL and API key setup for reference.
section: agents
section_title: AGENTS
section_order: 10
---

# Manual Cursor Setup

This page covers the Cursor desktop editor, not Cursor CLI or Private Inference. Cursor did not appear in the Magpie Agent panel inspected for this update, so do not assume the one-click steps for other agents apply.

Cursor's interface and third-party model support can change. The following is the previous editor setup path and **has not been revalidated with the current Cursor version and SorryCode**. If the options are missing or a model does not work, consult [Cursor's API key documentation](https://cursor.com/help/models-and-usage/api-keys); do not assume the connection succeeded.

## 1. Prepare

Install and sign in from the [Cursor website](https://cursor.com/downloads). Prepare a [SorryCode API key whose group supports your model](/docs/start/create-api-key). Open a test project in Cursor; do not send your key in chat or write it into project files.

## 2. Configure the Editor

The previous path was `Cursor Settings → Models → API Keys`. If the current interface offers an OpenAI Base URL override and custom models, enter:

| Field | Value |
| --- | --- |
| OpenAI API Key | A SorryCode key for the target model's group |
| Override OpenAI Base URL | Enable |
| Base URL | `https://sorrycode.com/v1` |
| Model ID | The exact ID returned for the current key's group, without Magpie's local provider prefix |

Use [Your First Request](/docs/start/first-request) to check the key and available models. Do not mix keys from different groups; recheck the key and model when switching groups. This URL connects to SorryCode directly, not to Magpie's local gateway. Do not let two configuration methods overwrite the same client entry.

## 3. Verify and Understand the Limits

Save, select the target model, and first ask: "Reply with connection successful. Do not modify files." After a reply, test file operations separately in the test folder. Successful chat does not prove agent tool calls work.

Cursor says custom keys only work with chat models, while Tab completion uses Cursor's built-in models; requests go through Cursor's servers. Check Cursor's current documentation for other proprietary features, model support, and billing. To restore the default configuration, disable the Base URL override and select a built-in model again.

For `401`, check the key and group first; for a missing model, check its exact ID. If the current version lacks these settings or the test fails, an old guide alone does not establish that this setup works with SorryCode.
