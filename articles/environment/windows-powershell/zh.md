---
title: Windows PowerShell
slug: windows-powershell
order: 2
summary: 需要运行 Windows 命令时，如何打开 PowerShell、复制命令并避免编码问题。
section: environment
section_title: 环境准备
section_order: 40
---

# Windows PowerShell

默认通过 Magpie 图形界面配置，不需要先打开终端。只有安装终端工具、Skill 或手动排障时，才需要这页。

<h2 id="open">怎么打开</h2>

按 `Win` 键，搜索并打开「Windows PowerShell」。使用 Windows Terminal 时，确认当前标签页运行的是 PowerShell。

<h2 id="install">怎么复制命令</h2>

只复制教程中标为 Windows PowerShell 的命令，完整粘贴后按回车。安装 Claude Code 时使用[官方安装说明](/docs/agents/claude-code)中的 Windows 路径，不再运行旧 SorryCode 接入脚本覆盖 Magpie。

<h2 id="dont-mix-shells">不要混用终端语法</h2>

PowerShell、cmd、Git Bash、WSL 是不同环境。Windows Terminal 只是终端窗口，不保证每个标签页都是 PowerShell。macOS / Linux 的命令不要直接粘贴到 PowerShell。

<h2 id="execution-policy">脚本被执行策略阻止</h2>

先确认脚本来源可信并读清报错。确实需要运行本地 `.ps1` 时，只对当前窗口临时允许：

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

关闭窗口后该设置失效，不需要永久修改系统策略。公司设备受策略管理时，按管理员要求处理，不要绕过组织限制。

<h2 id="encoding">中文和 JSON 乱码</h2>

常见原因是 Windows 控制台代码页与 PowerShell 编码不一致。发送 JSON 时，先写成 UTF-8 无 BOM 文件，再让 `curl.exe` 读取，不要把多行 JSON 塞进一条命令。

[首条请求](/docs/start/first-request)已有完整 PowerShell 文件写入示例，按原样使用，不混入 cmd 或 Bash 语法。报错求助时先隐藏 Key 和个人信息。

<h2 id="next">下一步</h2>

回到 [Claude Code](/docs/agents/claude-code) 或正在安装的 [Skill](/docs/skills/featured-skills)；还没配置模型时，先看 [Magpie](/docs/agents/magpie)。
