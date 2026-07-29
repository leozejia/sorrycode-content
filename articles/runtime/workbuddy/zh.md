---
title: WorkBuddy 快速开始
slug: workbuddy
order: 1
summary: 安装 WorkBuddy，接入 SorryCode，选择安全的工作空间，并完成第一个本地文件任务。
section: runtime
section_title: 模型与工作台
section_order: 10
group: tencent
group_title: Tencent
group_order: 27
---

# WorkBuddy 快速开始

WorkBuddy 是一个桌面 AI 工作台。你可以把文件、资料和任务交给它，让它规划步骤、调用工具，并把结果保存成实际文件。

如果你想让 WorkBuddy 的模型请求走 SorryCode，最短路径是：

1. 安装并登录 WorkBuddy
2. 在 WorkBuddy 里添加一个 SorryCode 自定义模型
3. 为第一次任务选择一个独立的测试文件夹
4. 保持默认权限，先完成一个低风险文件任务

这页负责把整条路线跑通。具体模型字段见 [WorkBuddy 接入 SorryCode](/docs/runtime/workbuddy-sorrycode)，文件权限见 [WorkBuddy 的权限与工作空间](/docs/runtime/workbuddy-permissions)。

<h2 id="install">安装 WorkBuddy</h2>

从 WorkBuddy 官网下载与你电脑匹配的桌面版：

<https://www.workbuddy.cn/>

当前桌面版支持 macOS 和 Windows。安装后打开 WorkBuddy，按界面提示完成登录。

如果点击登录没有反应，先确认电脑已经设置默认浏览器，再完全退出 WorkBuddy 后重新打开。不要从非官方站点下载安装包。

<h2 id="connect-sorrycode">接入 SorryCode</h2>

WorkBuddy 自带模型，也支持 OpenAI 兼容的自定义 API。SorryCode 使用后一条路径。

打开：

```text
左下角账户菜单 → 设置 → 模型 → 添加模型 → 自定义 / Custom
```

接着按 [WorkBuddy 接入 SorryCode](/docs/runtime/workbuddy-sorrycode) 填写接口地址、API Key 和模型名称。保存后，新增模型会出现在聊天界面的“自定义模型”分组中。

<h2 id="workspace">准备第一个工作空间</h2>

不要用桌面根目录、下载目录、整个用户目录或重要项目作为第一次测试的工作空间。

新建一个空文件夹，例如：

```text
WorkBuddy-Test
```

回到“新建任务”，点击输入框下方的“选择工作空间”，选择这个文件夹。工作空间决定 WorkBuddy 这次任务主要读取和保存哪些文件。

权限保持“默认权限”。遇到超出工作空间或高风险操作时，WorkBuddy 会停下来请求确认。

<h2 id="first-task">完成第一个任务</h2>

先从一个容易检查的 Markdown 文件开始：

```text
请在当前工作空间创建 hello-workbuddy.md，写入今天的日期、三条使用 WorkBuddy 的注意事项，以及一句“SorryCode 连接测试完成”。完成后告诉我文件保存在哪里。不要修改其他文件。
```

任务结束后检查三件事：

- WorkBuddy 给出了正常回复
- `hello-workbuddy.md` 出现在刚才选择的文件夹中
- 文件内容符合要求，且没有改动其他文件

这一步同时验证了模型连接、工具调用和工作空间写入。只会聊天但没有创建文件时，去看 [WorkBuddy 接入 SorryCode / 常见问题](/docs/runtime/workbuddy-sorrycode#common-issues)。

<h2 id="next">下一步做什么</h2>

第一次任务成功后，可以逐步增加复杂度：

- 把一份会议记录整理成 Markdown 或 Word 初稿
- 读取一小份表格并输出字段说明
- 为几份测试文件生成重命名预览，确认后再执行
- 根据公开资料生成报告提纲，再逐段补充来源

每次先用副本或测试目录。涉及批量重命名、覆盖、删除、运行脚本或访问外部服务时，先要求 WorkBuddy 展示计划和影响范围。

<h2 id="boundaries">使用边界</h2>

- WorkBuddy 是工作台，模型质量和可用能力取决于你选择的模型
- 自定义模型费用由对应的 SorryCode API Key 产生，不消耗 WorkBuddy 自带模型额度
- 电脑关机或 WorkBuddy 未运行时，本地任务不会继续执行
- 默认权限能降低误操作风险，但不能替代文件备份
- 不要把 API Key 粘贴到任务对话、截图、文档或项目文件里

上游参考：[WorkBuddy 官网](https://www.workbuddy.cn/) 和 [WorkBuddy 官方文档](https://www.workbuddy.cn/docs/workbuddy/FirstTask)。
