---
title: WorkBuddy
slug: workbuddy
order: 5
summary: 安装 WorkBuddy 桌面应用，在 Magpie 中启用，再用一个文件任务确认接入。
section: agents
section_title: AGENTS
section_order: 10
---

# WorkBuddy

WorkBuddy 适合在桌面界面里处理文档、表格和本地文件。

## 1. 安装 WorkBuddy

从 [WorkBuddy 官网](https://www.workbuddy.cn/)下载适合系统的版本，完成安装并打开。

## 2. 在 Magpie 中启用

先完成[用 Magpie 配置 SorryCode](/docs/agents/magpie)，在 Agent 面板找到对应的 WorkBuddy 客户端，启用「接入」并选择模型。配置后重新打开 WorkBuddy，在应用的模型选择器中选中刚配置的模型。

WorkBuddy 与国际版 WorkBuddy AI 是不同客户端，要选与你安装版本对应的项目。

## 3. 试一个文件任务

选择一个工作文件夹，发送：

```text
读取这个文件夹中的文档，按文件名各写一句摘要。先只回复，不修改原文件。
```

按需授权这个文件夹即可，不必为了首次测试开放其他目录。接入报错看[常见问题](/docs/troubleshoot/common-errors)。
