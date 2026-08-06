---
title: 在 Codex 中使用 SorryCode 多模型
slug: codex-multi-model
order: 2
summary: 使用 OpenCodex，把当前 SorryCode Key 分组中的模型加入 Codex App 模型选择器。
section: runtime
section_title: 模型与工作台
section_order: 10
group: openai
group_title: OpenAI
group_order: 10
---

# 在 Codex 中使用 SorryCode 多模型

Codex App 默认不会列出当前 SorryCode 分组中的所有模型。已经按 [Codex](/docs/runtime/codex) 完成接入，但还想在模型选择器里直接使用 DeepSeek 等模型时，使用 OpenCodex。

OpenCodex 在本机运行代理，并把可用模型写入 Codex 共用的模型目录。它不会修改 Codex App 程序本身。

<h2 id="prepare">准备一把 Codex 分组 Key</h2>

在 [API Key 页面](https://sorrycode.com/keys) 单独创建一把给 Codex 使用的 Key，并选择包含目标模型的分组。

模型范围由这把 Key 的分组决定。页面里看到的“全部模型”，指当前分组返回的全部模型，不包括其他分组。

这把 Key 直接填入 OpenCodex，不需要设置环境变量。

<h2 id="install">安装 OpenCodex</h2>

先关闭 Codex App，再在终端运行：

```bash
npm install -g @bitkyc08/opencodex
ocx --version
ocx gui
```

`ocx gui` 会启动本机代理并打开管理页面。OpenCodex 默认监听 `127.0.0.1:10100`。

如果找不到 `npm`，先看 [环境准备 / Node.js](/docs/environment/nodejs)。

<h2 id="provider">添加 SorryCode</h2>

在 OpenCodex 管理页面打开 `Providers`，选择 `Add provider`，再选择自定义端点。使用下面的设置：

| 配置项 | 设置 |
| --- | --- |
| Provider ID | `sorrycode` |
| Adapter | `openai-responses` |
| Base URL | `https://sorrycode.com` |
| API Key | 刚才创建的 Codex 分组 Key |
| Responses Path | `/v1/responses` |
| Live Model Discovery | 开启 |

保存后打开 `Models`。保持 SorryCode 分组为 `All on`，不要设置只允许少数模型的列表。这样 OpenCodex 会从 SorryCode 获取当前 Key 可见的模型，并在 Codex 中显示为 `sorrycode/模型名`。

例如当前分组包含 DeepSeek 时，模型选择器里会看到：

```text
sorrycode/deepseek-v4-flash
sorrycode/deepseek-v4-pro
```

<h2 id="service">让 Codex App 随时可用</h2>

Codex App 的请求会经过本机 OpenCodex。安装后台服务后，它会随登录启动，并在异常退出后自动重启：

```bash
ocx service install
ocx sync --restart-codex
ocx service status
```

Windows 安装后台服务时需要使用管理员权限打开 PowerShell。同步完成后，重新打开 Codex App，在模型选择器中选择 `sorrycode/...` 模型即可。

同一时间只让一个工具管理 Codex 配置和模型目录。此前使用过其他 Provider 管理器时，先停用它，再启用 OpenCodex。

<h2 id="troubleshoot">没有看到模型怎么办</h2>

- OpenCodex 看不到目标模型：检查这把 Key 选择的 SorryCode 分组
- OpenCodex 已经看到，Codex App 还没有：运行 `ocx sync --restart-codex`
- Codex 报本机连接失败：运行 `ocx service status`，再按提示修复服务
- 需要进一步诊断：运行 `ocx doctor`

想暂时恢复原生 Codex 配置，可以运行：

```bash
ocx restore
```

要同时移除后台服务并恢复原生 Codex，运行：

```bash
ocx service uninstall
```

上游参考：[OpenCodex 官方仓库](https://github.com/lidge-jun/opencodex)、[安装文档](https://opencodex.me/getting-started/installation/)、[Codex App 模型选择器](https://opencodex.me/guides/codex-app-models/)。
