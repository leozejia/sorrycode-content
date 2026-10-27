---
title: Common Questions
slug: common-errors
order: 1
summary: Check the Magpie connection first, then narrow down authentication, model access, and network errors.
section: troubleshoot
section_title: Troubleshoot
section_order: 50
---

# Common Questions

With the default Magpie setup, first confirm that Magpie is running, **Connect** is enabled for the target agent, and you reopened the agent after setup. Do not run an old connector over this configuration.

## Missing models or an unrecognized agent

- Click **Fetch Models** again in the Magpie provider settings, save, and select the models you need.
- Confirm that the agent is installed and the Magpie entry matches the actual client. WorkBuddy and WorkBuddy AI, and the different Cursor client types, are not interchangeable.
- Update and reopen Magpie. Do not copy another tool's configuration into an unsupported client.

## 401 Unauthorized / API KEY REQUIRED

`API KEY REQUIRED` means the server did not receive supported authentication information. It does not mean the balance is empty. Other `401` errors can also indicate an invalid or disabled key.

Check that the provider's key in Magpie is complete, active, and belongs to the selected group. Then confirm that the request actually goes through Magpie. Old connectors, manual settings, or environment variables may point the agent elsewhere. Do not paste your key into chat for troubleshooting.

The provider Base URL in Magpie points to SorryCode. The agent may connect to a local Magpie gateway URL instead. These addresses can coexist; do not overwrite one with the other to make them match.

## 403 / unavailable model

Check whether the key's group exposes the requested model. Fetch the current model list in Magpie and choose from it instead of copying model names from an old guide. Fetch models again after changing groups.

## 404 Not Found

Check the provider Base URL against the [Magpie guide](/docs/agents/magpie). Do not append `/v1` twice or include a full request path. For manual API calls, check each protocol and path separately rather than applying one URL rule to every endpoint.

## 429 / quota problems

Check the account balance and key spending limit, then reduce request frequency and concurrency. Rate limiting and insufficient balance are different causes.

## Timeout / TLS / interrupted connection

Confirm that Magpie is running, then check whether your network or proxy can reach the provider URL. Reinstalling repeatedly is not a network fix. For an interrupted paid image request, check whether it already completed before submitting another.

## Still failing

Record the agent and Magpie versions, time, full error, and request ID. Hide the key and personal information. Use a [manual API check](/docs/start/first-request) only when you need to separate gateway and client failures. For Windows command or encoding issues, see [Windows PowerShell](/docs/environment/windows-powershell).
