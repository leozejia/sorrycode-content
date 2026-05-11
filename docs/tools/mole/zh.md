---
title: Mole
slug: mole
order: 2
summary: 一个 Mac 本地维护工具。先看清空间被什么占用，再安全预览清理开发缓存、安装包、App 残留和临时文件。
section: tools
section_title: 工具
section_order: 28
source_url: https://github.com/tw93/Mole
---

# Mole

`Mole` 是一个 Mac 本地维护工具。

我们推荐它，不是为了让你一键猛删，而是让你先看清楚本地环境：空间被什么占了，哪些缓存可以清，哪些项目产物已经没用了。

<h2 id="what-is-mole">Mole 是什么</h2>

长期用 Mac 做开发、设计或内容创作，磁盘很容易慢慢被吃掉。

常见情况是：

- Xcode、模拟器、Node、npm、浏览器缓存堆了很多
- 下载目录里有大量安装包
- App 卸载了，但偏好设置、启动项、缓存还在
- 项目里残留了旧构建产物
- 想清理，但不知道哪些能删，哪些不能动

`Mole` 把这些本地维护动作收进一个命令行工具里。它可以分析磁盘、预览清理、清开发缓存、找安装包、卸载 App，也可以看系统状态。

<h2 id="why-recommend">为什么推荐</h2>

AI 编程不是只发生在云端。你的本地环境也会影响体验。

如果磁盘空间紧张、缓存混乱、项目产物堆太多，很多问题会变得很难判断：安装慢、构建慢、依赖异常、模拟器占满空间、电脑风扇狂转。

`Mole` 的价值是帮你把这些问题看清楚，然后再决定要不要清理。

<h2 id="safe-start">先从安全预览开始</h2>

第一次用，不要先运行 `mo clean`。

先按这个顺序：

```bash
mo analyze
mo clean --dry-run
mo purge --dry-run
```

- `mo analyze`：看空间主要被什么占用
- `mo clean --dry-run`：预览系统和开发缓存清理，不真正删除
- `mo purge --dry-run`：预览项目构建产物清理，不真正删除

看懂输出以后，再决定是否执行真正清理。

<h2 id="install">安装</h2>

推荐用 Homebrew：

```bash
brew install mole
```

安装后先看帮助：

```bash
mo --help
```

<h2 id="common-commands">最常用的 4 个命令</h2>

### 看磁盘占用

```bash
mo analyze
```

适合第一次使用。它帮助你先看清楚空间去哪了。

### 预览清理

```bash
mo clean --dry-run
```

适合清理前确认。不要跳过 `--dry-run`。

### 预览项目产物清理

```bash
mo purge --dry-run
```

适合长期做开发的人，用来检查旧项目构建产物。

### 看系统状态

```bash
mo status
```

适合观察 CPU、内存、磁盘、网络等状态。

<h2 id="when-not-to-use">什么时候不要用</h2>

先不要在这些情况下直接清理：

- 你看不懂 `--dry-run` 输出
- 你正在做重要项目，还没提交或备份
- 你不知道某个目录是不是项目必须文件
- 你只是想“试试看能不能多删点”

这时候先停下来，把 `--dry-run` 输出复制给 AI，让它帮你解释哪些可以清、哪些应该保留。

<h2 id="ai-workflow">和 AI 编程有什么关系</h2>

很多 AI 编程问题表面是模型问题，实际是本地环境问题。

比如：

- 安装依赖很慢
- 项目构建异常
- 磁盘空间不足
- 模拟器和缓存占满硬盘
- 旧构建产物影响判断

`Mole` 不会帮你写代码，但它能让你的本地开发环境更清楚、更轻、更可控。

<h2 id="common-issues">常见问题</h2>

- 我可以直接运行 `mo clean` 吗
  第一次不建议。先运行 `mo clean --dry-run`。
- `mo uninstall` 可以直接用吗
  先确认你真的要卸载对应 App，并看清它会移除哪些残留。
- Windows 可以用吗
  Mole 主要面向 macOS。
- 它和 CleanMyMac / AppCleaner 有什么关系
  它覆盖了一部分相似需求，但更偏命令行和开发者场景。
