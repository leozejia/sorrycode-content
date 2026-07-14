---
title: CC-Switch
slug: cc-switch
order: 1
summary: 进阶配置切换工具。适合需要图形化管理 endpoint、API Key 和多 runtime 配置的人。
section: tools
section_title: 工具
section_order: 28
---

# CC-Switch

如果你已经跑通过一键安装，但后续需要频繁切换 endpoint、API Key 或不同 runtime 配置，可以再看 CC-Switch。

它不是 runtime 本身，而是帮你管理本地 endpoint、API Key 和配置切换的工具。

参考：[CC-Switch 项目地址](https://github.com/farion1231/cc-switch)

## 适合谁

这条路径更适合下面几种人：

- 你想图形化管理配置
- 你会切换多个站点
- 你不想记环境变量写在哪里
- 你想先把链路跑通，再慢慢理解 runtime 细节

## 你能得到什么

通过 CC-Switch，你通常可以把这些事情集中处理：

- endpoint 配置
- API Key 配置
- 多站点切换
- 不同 runtime 的本地配置管理

## 怎么接入 SorryCode

1. 登录 SorryCode
2. 去 [开始使用 / 创建 API Key](/docs/start/create-api-key)
3. 在 key 列表页点击「导入到 CCS」
4. 或手动新建配置
5. 填入你当前 runtime 所需的地址和密钥

如果你走 OpenAI-compatible 路径，通常会用到：

- Base URL：`{{API_BASE_URL}}`
- API Key：你的 `sk-...`

如果你走 Claude Code 路径，通常会改由 Claude 相关配置模板导入。

## 什么时候它比手动配置更合适

优先选 CC-Switch 的场景：

- 你不想自己维护 `export / setx`
- 你要频繁切换不同站点
- 你不想把接入细节和 runtime 启动过程绑死在一起

## 和一键安装是什么关系

小白默认先走一键安装。

CC-Switch 不是必经前置，而是进阶配置切换工具：当你已经知道自己要切换哪些 endpoint、API Key 或 runtime 配置时，再用它集中管理。

## 下一步

- 要看 Codex：去 [Runtime / Codex](/docs/runtime/codex)
- 要看 Claude Code：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 要补共享前置：去 [环境准备 / Node.js](/docs/environment/nodejs)
