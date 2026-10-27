---
title: 常见问题
slug: common-errors
order: 6
summary: 接入报错、Node.js、PowerShell 和编码问题，遇到时再按需查阅。
section: start
section_title: 开始使用
section_order: 1
---

# 常见问题

默认通过 Magpie 接入时，先确认 Magpie 正在运行，目标 Agent 已启用「接入」，并且配置后已经重新打开 Agent。不要同时运行旧接入器来覆盖配置。

## 模型没有出现，或 Agent 没有识别

- 在 Magpie 的供应商配置里重新点击「获取模型」，确认已保存并选中所需模型。
- 检查 Agent 是否安装完成，Magpie 中的项目是否对应实际客户端。WorkBuddy 与 WorkBuddy AI、Cursor 的不同客户端形态不能混用。
- 更新 Magpie 后重新打开；仍不支持的客户端不要照搬其他工具的配置。

## 401 Unauthorized / API KEY REQUIRED

`API KEY REQUIRED` 表示服务端没有收到支持的认证信息，不等于余额不足。其他 `401` 也可能是 Key 无效或已禁用。

先检查 Magpie 供应商中的 Key 是否完整、有效，是否属于所选分组；再确认请求确实经过 Magpie。尤其留意旧接入脚本、手动配置或环境变量是否把 Agent 指向了其他地址。不要把 Key 贴到聊天里排查。

Magpie 的供应商 Base URL 是 SorryCode 地址；Agent 连接的可以是本机 Magpie 网关地址。两者同时存在是正常的，不要为了统一地址而相互覆盖。

## 403 / 模型不可用

检查 Key 所属分组是否开放目标模型。回 Magpie 获取最新模型列表，从列表选择，不要手抄旧教程的型号。切换分组后也要重新获取模型。

## 404 Not Found

检查 Magpie 供应商的 Base URL，按[配置教程](/docs/agents/magpie)填写，不要重复拼接 `/v1` 或完整请求路径。手动 API 请求则须分别核对协议和路径，不能把所有接口都按同一规则改地址。

## 429 / 配额不足

先检查余额和这把 Key 的额度，再降低请求频率与并发。限频和余额不足不是同一件事。

<h2 id="network">超时 / TLS / 连接中断</h2>

确认 Magpie 正在运行，再检查网络或代理是否能访问供应商地址。不要反复重装工具；付费图片请求中断后，先确认上次是否已完成，不要连续重复提交。

<h2 id="nodejs">找不到 node、npm 或 npx</h2>

Magpie 和桌面 Agent 不要求先装 Node.js。只有某个 Skill 明确需要时，再检查：

```bash
node --version
npm --version
npx --version
```

能显示版本号，通常不必重复安装，具体版本要求以该 Skill 的说明为准。已经能使用 Agent 时，可以把 Skill 文档发给它，先让它检查环境并说明要做的改动。

确实缺少时，从 [Node.js 官网](https://nodejs.org/zh-cn/download)下载当前 LTS 的 macOS 或 Windows 安装包，按默认选项安装，重新打开终端后再检查。不必额外装 Homebrew；已有其他 Node.js 管理方式时，不要叠加安装。下载超时先检查网络和代理，不要反复换版本。

<h2 id="windows-powershell">Windows 命令或脚本报错</h2>

按 `Win` 键搜索「Windows PowerShell」并打开。使用 Windows Terminal 时，确认当前标签页是 PowerShell。只复制教程对应终端的完整命令，不要混用 cmd、Git Bash、WSL 或 macOS / Linux 语法。

<h3 id="execution-policy">脚本被执行策略阻止</h3>

先读清报错并确认脚本来源可信。确实需要运行本地 `.ps1` 时，只对当前窗口临时允许：

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

关闭窗口后设置失效，不需要永久放开系统策略。公司设备按管理员要求处理，不要绕过组织限制。

<h3 id="encoding">中文或 JSON 乱码</h3>

常见原因是 Windows 控制台代码页与 PowerShell 编码不一致。先把 JSON 写成 UTF-8 无 BOM 文件，再用 `curl.exe --data-binary "@file.json"` 发送，不要内联多行 JSON。[首条请求](/docs/start/first-request)有完整的 PowerShell 文件写入示例。

## 仍然失败

记录 Agent 与 Magpie 版本、发生时间、完整错误和 request ID，并隐藏 Key 与个人信息。需要区分网关和客户端问题时，再做[手动 API 验证](/docs/start/first-request)。
