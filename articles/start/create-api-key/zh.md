---
title: 创建 API Key
slug: create-api-key
order: 3
summary: 在控制台创建匹配模型分组的 API Key，然后交给 Magpie 配置。
section: start
section_title: 开始使用
section_order: 1
---

# 创建 API Key

API Key 是调用模型的密钥，用来确认使用记录和费用归属。创建后把它填入 Magpie，不要发到聊天里。

## 1. 打开 API 密钥页面

登录 [SorryCode 控制台](https://sorrycode.com)，确认余额可用，在左侧进入「API 密钥」，也可以直接打开 [API 密钥列表](https://sorrycode.com/keys)。

![控制台里的 API 密钥入口](./api-key-menu.png)

## 2. 创建密钥，选择分组

点击创建密钥，填写名称，选择要使用的模型分组。名称方便自己辨认即可，例如「日常工作」。

分组决定这把 Key 可用的模型和计费倍率。先选一个需要的分组；要在 Magpie 中添加多个分组，再分别准备对应的 Key。

额度限制为 `0` 表示不单独限制，按需设置预算。速率限制和有效期不确定时可先保持默认。

![创建密钥时设置名称和分组](./create-key-dialog.png)

## 3. 复制到 Magpie

创建后复制完整密钥，按[用 Magpie 配置 SorryCode](/docs/agents/magpie)，粘贴到对应自定义供应商的 API Key 字段。

![创建完成后复制 API Key](./key-created-copy.png)

一份账号余额可以有多把 Key。同一兼容分组的 Key 可以供多个 Agent 使用，不必每装一个工具就新建一把。只有需要分开统计、限额或轮换时，才按用途拆分。

想换分组，可以回到列表切换；随后在 Magpie 中核对对应配置并重新获取模型，不要把不同分组的 Key 混填。

![在 API 密钥列表切换分组](./key-group-switch.png)

密钥不要放进提示词、公开截图或代码仓库。泄露后立即在控制台禁用或删除，并创建新 Key。
