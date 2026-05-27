---
title: 常见问题
slug: common-errors
order: 1
summary: 按错误码和现象给出最短修复路径。
section: troubleshoot
section_title: 排障
section_order: 50
---

# 常见问题

## 401 Unauthorized

优先检查：

- API Key 是否完整
- 认证头是不是写对了
- 你是不是把站内 key 和上游官方 key 混用了

协议差异也要看：

- OpenAI-compatible 常用 `Authorization: Bearer ...`
- Anthropic-compatible 常用 `x-api-key: ...`

## 404 Not Found

最常见原因：

- Base URL 漏了 `/v1`
- 路径拼接错了
- 你把 OpenAI-compatible 路径和 Anthropic-compatible 路径混用了

## 429 / 配额不足

先判断是哪一类：

- 余额不足
- 限频触发
- 短时间并发过高

如果只是验证链路，先降低并发和请求频率再试。

## 超时 / TLS 错误

先看：

- [环境准备 / Node.js](/docs/environment/nodejs#network)

## PowerShell 执行策略报错

先看：

- [环境准备 / Windows PowerShell](/docs/environment/windows-powershell)

## 你不知道该先查哪一页

回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)
