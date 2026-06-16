---
title: Windows PowerShell
slug: windows-powershell
order: 2
summary: Windows 用户运行 SorryCode 一键安装时的终端入口：怎么打开、粘贴命令、避免混用 shell 和编码问题。
section: environment
section_title: 环境准备
section_order: 40
---

# Windows PowerShell

如果你是 Windows 用户，运行 SorryCode 一键安装时，默认打开 `PowerShell` 或 `Windows Terminal`。

你不需要先学会命令行。只要知道：在 SorryCode 控制台复制整条安装命令，打开终端，粘贴，按回车。

<h2 id="open">怎么打开</h2>

1. 按键盘上的 `Win` 键
2. 输入 `PowerShell` 或 `Terminal`
3. 打开 `Windows PowerShell` 或 `Windows Terminal`
4. 粘贴 SorryCode 控制台或文档里的 `Windows` 一键安装命令
5. 按一次回车

如果你不知道选哪个，优先打开 `Windows Terminal`。如果电脑里没有，就打开 `Windows PowerShell`。

<h2 id="install">一键安装怎么粘贴</h2>

优先在 `API 密钥` 页面点击 `接入工具`，选择 `Codex` 或 `Claude Code`，再选择 `Windows`，把弹窗里的命令整条复制。

如果你暂时打不开控制台弹窗，也可以在 `Runtime / Codex` 或 `Runtime / Claude Code` 页面里，找到 `Windows` 下面的通用命令，整条复制。

不要只复制一半，也不要自己拆成多行。

- 安装 Codex：去 [Runtime / Codex](/docs/runtime/codex)
- 安装 Claude Code：去 [Runtime / Claude Code](/docs/runtime/claude-code)

<h2 id="dont-mix-shells">不要混用不同 shell</h2>

Windows 上常见入口有好几个：

| 名称 | 能不能直接照抄 SorryCode Windows 命令 |
| --- | --- |
| `PowerShell` | 可以 |
| `Windows Terminal` | 可以，里面通常也是 PowerShell |
| `cmd` | 不建议手动改命令；文档里的命令已经用 `cmd /c` 包好了 |
| `Git Bash` | 不要照抄 PowerShell 命令 |
| `WSL` | 不要照抄 Windows 命令；它更像 Linux |

小白默认只记住一句话：

```text
Windows 文档里的命令，就在 PowerShell / Windows Terminal 里运行。
```

<h2 id="execution-policy">执行策略</h2>

如果你看到 `ExecutionPolicy` 或“脚本无法运行”相关提示，不要自己先永久修改系统策略。

SorryCode 的 Windows 一键安装会只对当前安装过程使用临时 `Bypass`，不会永久放开你的电脑策略。

如果你只是复制 Runtime 页面里的 Windows 一键安装命令，通常不用手动执行下面这些命令。

只有在你自己手动运行本地 `.ps1` 文件，或者客服明确让你处理执行策略时，再看这里。

### 临时允许当前窗口

这条只影响当前 PowerShell 窗口。关闭窗口后就失效，优先用它：

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### 当前用户长期允许本地脚本

这条会影响当前 Windows 用户。只有你明确知道自己在做什么，或者有人指导你处理时再用：

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

如果仍然失败，先把完整报错发给社群或客服，不要随便复制网上的其它长期放开策略命令。

<h2 id="encoding">编码和 JSON</h2>

Windows 终端有时会因为 `console code page / PowerShell encoding mismatch` 导致中文、JSON 或文件内容乱码。

所以公开文档里的 Windows 示例会尽量这样写：

- 不把复杂 JSON 直接塞进一行命令
- 先写入 `request.json`
- 用 UTF-8 无 BOM 保存
- 再让 `curl` 读取这个文件

如果你是小白，不需要理解这些术语。只要照抄文档里的 PowerShell 示例，不要把 macOS / Linux 的命令拿到 Windows 里改。

<h2 id="next">下一步</h2>

- 要装 Codex：去 [Runtime / Codex](/docs/runtime/codex)
- 要装 Claude Code：去 [Runtime / Claude Code](/docs/runtime/claude-code)
- 要准备 Node.js：去 [环境准备 / Node.js](/docs/environment/nodejs)
