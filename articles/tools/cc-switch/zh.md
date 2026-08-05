---
title: 在 Codex 中切换 SorryCode 模型
slug: cc-switch
order: 1
summary: 用 CC Switch 把 SorryCode 分组中的非 GPT 模型加入 Codex App 模型选择器。
section: tools
section_title: 工具
section_order: 28
---

# 在 Codex 中切换 SorryCode 模型

Codex App 默认只展示内置 GPT 模型。即使当前 SorryCode 分组还提供 DeepSeek 等模型，它们也不会自动出现在模型选择器中。SorryCode 推荐用 CC Switch 管理这份模型目录。

这篇只讲一条路径：导入 SorryCode，在 CC Switch 中获取当前分组模型，然后重启 Codex App。

<h2 id="install">安装 CC Switch</h2>

只从 [CC Switch 官方仓库](https://github.com/farion1231/cc-switch) 或 [GitHub Releases](https://github.com/farion1231/cc-switch/releases) 下载。

macOS 也可以使用 Homebrew：

```bash
brew install --cask cc-switch
```

已有 CC Switch 时，先更新到最新版。

<h2 id="import">从 SorryCode 导入</h2>

1. 打开 [SorryCode API Key 页面](https://sorrycode.com/keys)
2. 找到要给 Codex 使用的 Key
3. 点击 `导入到 CCS`
4. 系统询问是否打开 CC Switch 时，确认打开并完成导入

导入链接包含当前 Key，不要转发、截图或公开分享。

<h2 id="models">加入当前分组的模型</h2>

打开 `CC Switch → Codex → SorryCode → 编辑`，按下面配置：

| 配置项 | 设置 |
| --- | --- |
| API 请求地址 | `https://sorrycode.com` |
| 上游格式 | `Responses（原生）` |
| 默认模型 | `deepseek-v4-flash` |

展开高级选项，在“模型映射”区域点击 `获取模型列表`。当前 Key 所属分组决定这里能看到哪些模型。需要使用 DeepSeek 时，保留：

```text
deepseek-v4-flash
deepseek-v4-pro
```

保存后，在 Codex 供应商列表中启用 SorryCode。

SorryCode 已支持 Codex 使用的 Responses 协议，这条路径不需要开启 CC Switch 路由接管，也不要求 CC Switch 长期在后台运行。

<h2 id="restart">重启 Codex App</h2>

模型目录在 Codex 启动时加载。完全退出 Codex App，再重新打开并新建会话。模型选择器中应出现 `DeepSeek V4 Flash` 和 `DeepSeek V4 Pro`。

如果没有出现，回到 CC Switch 检查三项：SorryCode 是否正在使用、模型映射是否已经保存、Codex App 是否完全退出后重启。`获取模型列表` 看不到 DeepSeek 时，应检查这把 Key 选择的 SorryCode 分组。
