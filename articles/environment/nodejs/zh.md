---
title: Node.js
slug: nodejs
order: 1
summary: macOS / Windows 的共享环境排障页。主要服务手动安装和一键安装失败后的环境定位。
section: environment
section_title: 环境准备
section_order: 40
---

# Node.js

对大多数 CLI 来说，Node.js 不是可选项，而是基础层。macOS 上还会遇到 `Command Line Tools / Homebrew / Git` 这一层。

但这页不是新手默认入口。

如果你只是想尽快把 `Codex` 或 `Claude Code` 跑起来，先回到对应的 runtime 页走一键安装。只有想手动控环境，或者安装时卡在 `Apple 弹窗 / Homebrew / Git / node / npm` 这一层，再认真看这页。

<h2 id="why-nodejs">为什么需要 Node.js</h2>

- 很多 CLI 本质上就是 Node.js 程序
- `node` 或 `npm` 不存在时，runtime 往往根本装不上
- 这一层出问题时，报错很容易被误判成网关或 API Key 故障

这页主要解决这些场景：

- `node` 命令不存在
- `npm` 命令不存在
- macOS 弹出 Apple 官方安装窗口
- macOS 要你输入电脑密码
- 安装 CLI 时直接报环境错误
- Windows 上不知道该用哪个终端，或者被脚本策略拦住；这种情况先看 [Windows PowerShell](/docs/environment/windows-powershell)

<h2 id="macos">macOS</h2>

macOS 一键安装会尽量帮你准备三层东西：

1. `Apple Command Line Tools`
2. `Homebrew / Git`
3. `Node.js 22 LTS / npm`

你不需要先理解它们。只要照着 runtime 页的一键安装命令走即可。

### Apple Command Line Tools

如果终端提示需要 `Apple Command Line Tools`，可能会弹出 Apple 官方安装窗口。

你要做的是：

1. 点“安装”
2. 等它安装完成
3. 不要关闭正在运行 SorryCode 安装命令的终端

如果你取消了弹窗，或者安装很久没有完成，重新运行同一条 SorryCode 一键安装命令即可。

### Homebrew / Git

`Homebrew` 是 macOS 上常用的工具安装器，`Git` 用来从 GitHub 安装社区 Skills。

一键安装会尝试自动准备它们。如果 Homebrew 提示按回车，就按回车；如果终端要求输入密码，输入你的电脑登录密码。输入时屏幕不会显示字符，这是 macOS 终端的正常行为。

如果你所在网络无法访问 GitHub，社区 Skills 可能还是装不上。这部分 SorryCode 不代管，需要你自己切换网络或代理。

### Node.js 22 LTS

SorryCode 一键安装会优先把 `Node.js 22 LTS` 装到你的用户目录，不要求你手动理解 Node。

如果安装已经完成，但你关闭终端重新打开后，输入 `node -v`、`npm -v` 或 `codex` 仍然提示“找不到命令”，通常是 macOS 没有读到命令路径。

按 `Command` + `空格`，输入 `Terminal`，按回车，然后复制下面整段命令粘贴进去，再按回车：

```bash
grep -q 'HOME/.local/sorrycode-node/bin' ~/.zprofile 2>/dev/null || cat >> ~/.zprofile <<'EOF'
# >>> SorryCode managed PATH >>>
export PATH="$HOME/.local/sorrycode-node/bin:$HOME/.npm-global/bin:/opt/homebrew/bin:/usr/local/bin:$HOME/.local/bin:$PATH"
# <<< SorryCode managed PATH <<<
EOF
grep -q 'HOME/.local/sorrycode-node/bin' ~/.zshrc 2>/dev/null || cat >> ~/.zshrc <<'EOF'
# >>> SorryCode managed PATH >>>
export PATH="$HOME/.local/sorrycode-node/bin:$HOME/.npm-global/bin:/opt/homebrew/bin:/usr/local/bin:$HOME/.local/bin:$PATH"
# <<< SorryCode managed PATH <<<
EOF
source ~/.zprofile
```

然后关闭终端，重新打开，再运行：

```bash
node -v
npm -v
codex --version
```

只有一键安装失败，才建议你手动安装：

推荐优先级：

1. Node.js 官方安装包
2. `Homebrew`

### 官方安装包

新手建议走官方安装包：

- 打开 [Node.js 官网](https://nodejs.org/en/download)
- 下载 `LTS` 版本
- 双击安装包，一路下一步完成安装
- 安装完成后，关闭并重新打开终端
- 再运行一次 `node -v` 和 `npm -v`

参考：[Node.js 官方下载页](https://nodejs.org/en/download)

### Homebrew

如果你已经知道 Homebrew 是什么，也可以用：

```bash
brew install node
```

这条手动命令会安装 Homebrew 当前默认的 Node 版本，不等同于 SorryCode 一键安装里的 `Node.js 22 LTS` 用户目录方案。

<h2 id="windows">Windows</h2>

推荐优先级：

1. Node.js 官方安装包
2. `winget`

### 官方安装包

- 打开 [Node.js 官网](https://nodejs.org/en/download)
- 下载 `LTS` 版本
- 双击安装包完成安装

### winget

```powershell
winget install OpenJS.NodeJS.LTS
```

<h2 id="powershell">PowerShell</h2>

对一键安装来说，你通常不用自己处理 `PowerShell` 执行策略。

SorryCode 的 Windows 安装链路会只对当前安装进程使用 `ExecutionPolicy Bypass`，不会永久改你的机器策略。

只有在你自己手动执行本地 `.ps1` 脚本，而且确实被策略拦住时，再考虑下面这些方式：

- 优先用当前进程的 `Bypass`
- 实在需要长期放开，再评估当前用户级别的策略

如果你只是要安装 runtime，不要先把这一步当成默认前置动作。

<h2 id="verify-install">验证安装</h2>

打开终端执行：

```bash
node -v
npm -v
```

两个命令都能输出版本号，就说明这一层已经准备好。

第一次接入建议选：

- Node.js `22 LTS`

第一次接入时，不建议一上来就追最新实验版本。

<h2 id="network">网络问题</h2>

只有在依赖下载明显很慢时，再考虑切换 npm 镜像。

切到国内镜像：

```bash
npm config set registry https://registry.npmmirror.com
```

恢复官方源：

```bash
npm config set registry https://registry.npmjs.org
```

如果你已经把这一层准备好，下一步回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)
- [工具 / CC-Switch](/docs/tools/cc-switch)
