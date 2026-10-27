---
title: DeepSeek Harness
slug: dsh
order: 4
summary: 下载 DSH 桌面应用，通过 Magpie 接入，然后打开文件夹完成第一个任务。
section: agents
section_title: AGENTS
section_order: 10
---

# DeepSeek Harness

DeepSeek Harness，简称 DSH，有桌面应用。不需要先安装 Node.js，也不用通过命令启动 Web UI。

## 1. 安装桌面应用

打开 [DeepSeek Harness 官网](https://www.deepseek.com/harness/)，选择适合系统的桌面版并安装。首次打开后，完成必要的系统权限确认。

## 2. 在 Magpie 中启用

先完成[用 Magpie 配置 SorryCode](/docs/agents/magpie)，在 Agent 面板找到 DeepSeek Harness，启用「接入」并选择模型。配置后重新打开 DSH。

## 3. 打开文件夹，试一个任务

在 DSH 中选择工作文件夹，发送：

```text
读取这个文件夹，按文件类型整理一份清单。只回复清单，不要移动或修改文件。
```

能看到实际文件内容的回复，就可以继续自己的任务。DSH 仍在快速迭代，界面以当前版本为准；接入报错看[常见问题](/docs/troubleshoot/common-errors)。
