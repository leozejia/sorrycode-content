---
title: VS Code
slug: vscode
order: 3
summary: 一个可选的可视化项目工作台。用它打开项目、查看文件和改动，并按需安装 Codex / Claude Code 插件。
section: tools
section_title: 工具
section_order: 28
source_url: https://code.visualstudio.com/
---

# VS Code

`VS Code` 是一个免费的项目编辑器。

你可以先把它理解成：项目文件管理器 + 代码编辑器 + 改动查看器。它不是 `Codex`，也不是 `Claude Code`，而是一个可以承载这些插件的可视化工作台。

如果你还没跑通 `Codex` 或 `Claude Code`，不用先学 VS Code。SorryCode 的默认路径是：先一键安装，再用官方桌面 App 进入项目。

<h2 id="when-to-use">什么时候适合用</h2>

适合这些情况：

- 你不习惯一直看终端
- 你想用侧边栏看项目里有哪些文件
- 你想更清楚地看到 AI 改了哪些内容
- 你想在同一个窗口里编辑文件、看差异、运行插件
- 你已经能启动 `Codex` 或 `Claude Code`，现在想要更可视化的工作台

不适合把它当成第一步硬前置。对纯小白来说，先把 runtime 跑起来更重要。

<h2 id="install-vscode">安装 VS Code</h2>

1. 打开 VS Code 官网：<https://code.visualstudio.com/>
2. 点击 `Download`，按你的系统下载安装
3. 打开 VS Code
4. 点击 `File / Open Folder...`
5. 选择你想操作的项目文件夹

官方安装说明：<https://code.visualstudio.com/docs/setup/setup-overview>

<h2 id="install-extensions">安装插件</h2>

VS Code 的插件都从左侧 `Extensions` 面板安装。

最简单的路径：

1. 打开 VS Code
2. 点击左侧方块图标 `Extensions`
3. 在搜索框输入插件名称
4. 点进插件详情页
5. 确认是官方或可信来源
6. 点击 `Install`

官方插件安装说明：<https://code.visualstudio.com/docs/getstarted/extensions>

<h2 id="codex-extension">Codex 插件</h2>

如果你想在 VS Code 里使用 Codex，可以看 OpenAI 的官方 IDE Extension 文档：

- Codex IDE Extension：<https://developers.openai.com/codex/ide>

建议顺序：

1. 先完成 [Runtime / Codex](/docs/runtime/codex) 的一键安装
2. 下载并打开 `Codex App`，确认能选择项目
3. 再安装 VS Code
4. 按 OpenAI 官方说明安装 Codex IDE 插件
5. 如果插件要求登录或授权，按插件自己的提示完成

不要默认假设 VS Code 插件一定会自动读取所有 SorryCode 配置。遇到登录、授权或配置提示时，以官方插件提示为准。

<h2 id="claude-code-extension">Claude Code 插件</h2>

如果你想在 VS Code 里使用 Claude Code，可以看 Claude Code 的官方 VS Code 文档：

- Claude Code VS Code：<https://code.claude.com/docs/en/vs-code>

建议顺序：

1. 先完成 [Runtime / Claude Code](/docs/runtime/claude-code) 的一键安装
2. 下载 `Claude Desktop`，或确认 `claude` 能在终端里启动
3. 再安装 VS Code
4. 按官方说明安装 Claude Code 插件
5. 如果插件要求登录、授权或配置，按插件自己的提示完成

<h2 id="mental-model">三句话理解关系</h2>

- `Codex / Claude Code`：真正执行任务的 agent runtime
- `Skills`：给 agent 看的操作说明书
- `VS Code`：看文件、看改动、装插件的可视化工作台

所以 VS Code 不是替代 `Codex` 或 `Claude Code`，而是让你更容易看见项目和改动。

<h2 id="first-use">第一次怎么用</h2>

第一次建议这样开始：

1. 用 VS Code 打开项目文件夹
2. 先看左侧文件树，确认是不是你要操作的项目
3. 打开 `README`、`package.json` 或入口文件
4. 再打开对应插件，或者继续用 `Codex App / Claude Desktop`
5. 让 agent 先解释项目，不要马上大改

可以复制这句话：

```text
先别改文件。请先读一下当前项目，告诉我这个项目是做什么的、入口在哪里、我应该先看哪些文件。
```

<h2 id="common-issues">常见问题</h2>

- VS Code 是必须安装的吗
  不是。它是可选的可视化工作台。
- 它和 Codex App 有什么区别
  `Codex App` 是 Codex 自己的桌面应用；`VS Code` 是通用编辑器，可以装不同插件，也适合看文件和改动。
- 插件装完就一定能用 SorryCode 吗
  不一定。先按 SorryCode runtime 页完成一键安装；如果插件弹出登录或配置提示，以插件官方说明为准。
- 我应该先学 VS Code 还是先学 Codex
  先把 `Codex` 或 `Claude Code` 跑通。VS Code 是后续让过程更可视化的选择。

<h2 id="next">下一步</h2>

- 要跑 Codex：去 [Runtime / Codex](/docs/runtime/codex)
- 要跑 Claude Code：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 要理解 Skills：去 [Skills / Skills 是什么](/docs/skills/featured-skills)
