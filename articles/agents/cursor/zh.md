---
title: Cursor 手动配置
slug: cursor
order: 3
summary: Cursor 编辑器与 Magpie 的接入分开处理，保留自定义地址和 API Key 的手动配置线索。
section: agents
section_title: AGENTS
section_order: 10
---

# Cursor 手动配置

本页针对 Cursor 桌面编辑器，不是 Cursor CLI 或 Private Inference。本次检查的 Magpie Agent 面板没有显示 Cursor，不能按其他 Agent 的一键接入步骤操作。

Cursor 的界面和第三方模型支持可能变化。以下是此前编辑器的手动配置路径，**尚未在当前版本与 SorryCode 上重新验证**；如果你的界面没有对应选项，或模型不能使用，请参考 [Cursor 官方 API Key 说明](https://cursor.com/help/models-and-usage/api-keys)，不要认为配置已接通。

## 1. 准备

从 [Cursor 官网](https://cursor.com/downloads)安装并登录。准备一把[所属分组支持目标模型的 SorryCode API Key](/docs/start/create-api-key)。在 Cursor 里打开一个测试项目，不要将 Key 发到聊天或写入项目文件。

## 2. 在编辑器中填写

此前的路径是 `Cursor Settings → Models → API Keys`。如果当前界面提供 OpenAI Base URL 覆盖和自定义模型选项，填写：

| 项目 | 内容 |
| --- | --- |
| OpenAI API Key | 支持目标模型的 SorryCode Key |
| Override OpenAI Base URL | 开启 |
| Base URL | `https://sorrycode.com/v1` |
| 模型 ID | 当前 Key 所属分组返回的准确 ID，不加 Magpie 的本地供应商前缀 |

可按[首条请求](/docs/start/first-request)检查 Key 和可用模型。不同分组的 Key 不要混用；更换分组时，需要重新检查 Key 和模型。以上地址是直连 SorryCode，不是 Magpie 的本地网关。不要同时使用两套配置覆盖同一个入口。

## 3. 验证与边界

保存后选择目标模型，先发送「只回复连接成功，不要修改文件」。收到回复后，再在测试文件夹中单独验证文件操作。聊天成功不代表 Agent 工具调用成功。

Cursor 官方说明自带 Key 只用于聊天模型，Tab 补全仍使用 Cursor 内置模型；请求会经过 Cursor 的服务器。其他专有功能、模型支持和计费以 Cursor 当前说明为准。需要恢复 Cursor 默认配置时，关闭 Base URL 覆盖并重新选择内置模型。

若报 `401`，先检查 Key 和分组；若找不到模型，检查准确 ID。当前版本不提供这些设置或验证失败时，不能仅凭旧教程断定 SorryCode 支持该用法。
