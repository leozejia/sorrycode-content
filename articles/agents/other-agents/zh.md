---
title: 其他 Agents
slug: other-agents
order: 6
summary: 已经习惯其他 Agent？从官方安装，在 Magpie 中启用对应客户端即可。
section: agents
section_title: AGENTS
section_order: 10
---

# 其他 Agents

如果还没选工具，先用 [Codex](/docs/agents/codex)。已经习惯下面的工具，就继续用，不必为接入 SorryCode 换工作台。

## 下载与选择

| Agent | 官方入口 | 使用时注意 |
| --- | --- | --- |
| OpenCode | [下载](https://opencode.ai/download) | 有桌面端和终端版，按你安装的版本使用 |
| Pi Agent | [官网](https://pi.dev/) | 轻量终端工具，安装方式以官网为准 |
| Kimi Code | [安装说明](https://www.kimi.com/code/docs/kimi-code-cli/guides/getting-started.html) | 终端工具，模型从 Magpie 当前列表选择 |
| Grok Build | [官方安装脚本](https://x.ai/cli/install.sh) | 接入文字模型不代表内置图片、视频工具也经过 SorryCode |
| Cursor | [下载](https://cursor.com/downloads) | CLI、普通编辑器和 Private Inference 是不同形态，不能混用配置 |

## 通过 Magpie 接入

1. 从官方入口安装目标工具。
2. 按[用 Magpie 配置 SorryCode](/docs/agents/magpie)添加供应商和模型，在 Agent 面板启用对应客户端。只按 Magpie 实际显示和支持的项目操作；不要把 Cursor Private Inference 的配置用于普通 Cursor 编辑器。
3. 重新打开工具，选择工作目录，发送「列出这个文件夹的主要文件，不要修改内容」。

如果 Magpie 没有识别到客户端，先确认安装是否完成、客户端形态是否匹配，再更新 Magpie。不要同时运行旧接入脚本或手改配置来覆盖它。其他错误见[常见问题](/docs/start/common-errors)。
