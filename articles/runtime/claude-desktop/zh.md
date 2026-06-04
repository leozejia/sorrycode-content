---
title: Claude Desktop
slug: claude-desktop
order: 3
summary: 在 Claude Desktop 里启用第三方推理网关，把模型请求接到 SorryCode。
section: runtime
section_title: Runtime
section_order: 10
---

# Claude Desktop

如果你想用 `Claude Desktop` 的图形界面，又希望模型请求走 SorryCode，这页就是最短路径。

你不需要先学终端，也不需要手动改配置文件。准备好 SorryCode API Key，在 Claude Desktop 里打开第三方推理配置，填入 Gateway 地址和 Key，重启后能正常进入 `Cowork 3P · Gateway`，就说明已经接通。

这页讲的是 Claude Desktop 的第三方推理网关配置。如果你只是想在终端里用 `claude` 读项目、改代码、执行命令，先看 [Runtime / Claude Code](/docs/runtime/claude-code)。

<h2 id="prepare">开始前准备</h2>

你需要三样东西：

1. 已安装 `Claude Desktop`
2. SorryCode API Key
3. SorryCode Gateway 地址：`https://sorrycode.com`

Claude Desktop 官方下载入口：

<https://claude.com/download>

API Key 在 SorryCode 控制台创建：

<https://sorrycode.com/keys>

创建后你会得到一个 `sk-...` 开头的 Key。后面填配置时会用到。

如果你还不知道怎么创建 API Key，先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="macos">macOS 配置步骤</h2>

### 第一步：打开 Claude Desktop

先打开 `Claude Desktop`。

如果你是第一次打开，停留在登录页面就可以。这里先不要登录 Anthropic 账号，因为我们要配置的是第三方推理网关。

### 第二步：启用 Developer Mode

保持 Claude Desktop 处于打开状态，看屏幕最上方的 macOS 菜单栏。

先点击 `Help`。如果你还没启用开发者模式，会在这里看到 `Troubleshooting`。

![Claude Desktop Help 菜单](./help-menu.png)

依次点击：

```text
Help → Troubleshooting → Enable Developer Mode
```

确认后，Claude Desktop 会重启，或者提示你重新打开。

如果你没有看到 `Developer` 菜单，通常是因为 Developer Mode 还没有启用成功。完全退出 Claude Desktop，再重新打开一次。

### 第三步：打开第三方推理配置

重启后，顶部菜单栏会出现 `Developer`。

点击：

```text
Developer → Configure Third-Party Inference...
```

![Claude Desktop Developer 菜单](./developer-menu.png)

这会打开第三方推理配置窗口。

### 第四步：填写 SorryCode 配置

在配置窗口里，先确认连接类型是 `Gateway`。

然后填写：

| 配置项 | 填什么 |
| --- | --- |
| `Credential kind` | `Static API key` |
| `Gateway base URL` | `https://sorrycode.com` |
| `Gateway API key` | 你的 SorryCode API Key，也就是 `sk-...` |
| `Gateway auth scheme` | `bearer` |

![Claude Desktop Gateway 配置窗口](./gateway-configuration.png)

注意：

- `Gateway base URL` 不要多加空格
- 这里填 `https://sorrycode.com`，不要加 `/v1`、`/v1/messages` 或其他路径
- `Gateway API key` 填你在 SorryCode 创建的 `sk-...`
- API Key 输入框显示成圆点是正常的，不需要让它明文显示
- 不确定是否填对时，可以先点 `Test connection`

填完之后点击右下角的 `Apply Changes`。

它的意思是：把这份配置应用到你当前这台电脑上。

### 第五步：重启并进入 Gateway 模式

应用配置后，按 Claude Desktop 的提示重启应用。

重启后，如果看到 `Continue with gateway`，点击它进入。

进入后，左下角状态区域会显示类似：

```text
Cowork 3P · Gateway
```

这说明 Claude Desktop 当前已经在 Gateway 模式下工作。

![Claude Desktop Gateway 模式运行状态](./gateway-success.png)

<h2 id="windows">Windows 配置步骤</h2>

Windows 的填写内容和 macOS 一样，区别主要是菜单入口。

打开 Claude Desktop 后，停留在登录页面。

在左上角找到菜单按钮，或者用键盘按 `Tab` 切换焦点，直到左上角菜单被选中，再按 `Enter` 打开。

然后依次进入：

```text
Help → Troubleshooting → Enable Developer Mode
Developer → Configure Third-Party Inference...
```

后面的填写方式和 macOS 一样：

| 配置项 | 填什么 |
| --- | --- |
| `Credential kind` | `Static API key` |
| `Gateway base URL` | `https://sorrycode.com` |
| `Gateway API key` | 你的 SorryCode API Key，也就是 `sk-...` |
| `Gateway auth scheme` | `bearer` |

填完后点击 `Apply Changes`，再按提示重启 Claude Desktop。

<h2 id="verify">怎么确认已经成功</h2>

配置完成后，先不要马上让它改项目。

你可以先问一句很简单的话：

```text
你现在可以正常回答吗？
```

如果能正常回复，说明基础连接已经通了。

如果你想确认它是不是能进入工作模式，可以再问：

```text
请先不要改任何文件，只告诉我现在这个界面能做什么。
```

第一次使用时，建议先做低风险测试。不要一上来就让它删除文件、重构项目，或者执行复杂命令。

<h2 id="common-issues">常见问题</h2>

### 没有 Developer 菜单

先确认你已经执行过：

```text
Help → Troubleshooting → Enable Developer Mode
```

然后完全退出 Claude Desktop，再重新打开。

只关闭窗口不一定等于完全退出。macOS 可以在菜单栏里选择 `Quit Claude`，Windows 可以从任务栏或任务管理器确认应用已经关闭。

### 找不到 Configure Third-Party Inference

先确认 Developer Mode 已经启用，并且 Claude Desktop 已经重启。

如果还是没有，说明当前 Claude Desktop 版本可能不支持这个入口。先更新到最新版，再重新打开。

### 没有 Continue with gateway

通常是配置还没有应用成功。

检查三件事：

1. 是否点击了 `Apply Changes`
2. 是否按提示重启了 Claude Desktop
3. 配置窗口里 Gateway 地址和 API Key 是否还在

如果仍然没有出现，重新打开配置窗口，再保存一次。

### API Key 报错

重新去 SorryCode 控制台复制一次 API Key。

注意不要复制到空格，也不要把说明文字一起复制进去。正确的 Key 通常是 `sk-...` 开头。

### 连接失败

优先检查：

1. `Gateway base URL` 是否填对
2. API Key 是否有效
3. SorryCode 账号是否有可用余额或权限
4. 当前网络是否能访问 SorryCode

如果你不确定是哪一层出问题，可以先看 [排障 / 常见问题](/docs/platform/create-api-key)。

### Code 页面不能按预期工作

Claude Desktop 里不同页面的能力边界可能不完全一样。你先用这页教程跑通 Gateway 模式。

如果你的目标是让模型读本地项目、改代码、执行命令，直接看 [Runtime / Claude Code](/docs/runtime/claude-code)。

<h2 id="next">下一步</h2>

如果你已经能进入 Claude Desktop，可以先从一个很小的任务开始：

```text
请帮我整理一个新手学习 AI 工具的待办清单，不要太长，分成今天、这周、以后再说三类。
```

如果你是想让它处理本地项目，可以先问：

```text
先不要改文件，先告诉我这个项目大概是做什么的，以及我应该先看哪些文件。
```

先让它观察，再让它行动。
