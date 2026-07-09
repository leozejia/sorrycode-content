---
title: 生成图片
slug: image-request
order: 6
summary: SorryCode 提供两种图片生成方式：直接在 Codex App 对话中生图，或安装 SorryCode Image2 Skill 完成可复现的生成和编辑任务。
section: platform
section_title: Platform
section_order: 8
---

# 生成图片

SorryCode 目前提供两种图片生成方式。第一次使用时，直接在 `Codex App` 对话中提出图片需求即可，不需要先学习接口、模型参数或命令行。

<h2 id="codex-app">方式一：直接在 Codex App 中生图</h2>

这是默认方式，适合快速生成封面、海报、插图、头像和视觉草稿。

完成 [Runtime / Codex](/docs/runtime/codex) 接入后，在 Codex App 中直接说：

```text
帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。
```

也可以继续提出修改：

```text
把标题区域留得更宽一些，减少装饰元素，改成横版。
```

对大多数用户来说，这条路径已经够用。

<h2 id="image2-skill">方式二：使用 SorryCode Image2 Skill</h2>

当任务需要下面这些能力时，再安装 `SorryCode Image2`：

- 编辑已有的本地图片
- 指定输出目录和尺寸
- 保存 prompt、响应和流式诊断
- 在项目中重复执行同一套图片工作流

`SorryCode Image2` 当前只使用 `gpt-image-2`。安装和使用方法见：

- [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)

<h2 id="which-one">应该选哪一种</h2>

| 需求 | 选择 |
| --- | --- |
| 第一次生图、快速出一张图 | 直接在 Codex App 对话中说 |
| 继续用自然语言修改刚生成的图片 | 直接在 Codex App 中继续对话 |
| 编辑本地图片 | SorryCode Image2 |
| 固定尺寸、目录或保存诊断文件 | SorryCode Image2 |
| 在项目工作流中重复执行 | SorryCode Image2 |

需要更多 AIGC 模型、素材生产或专门的视觉资产工作流时，请使用 [SorryAssets](https://sorryassets.com)。

<h2 id="next">下一步</h2>

- 还没接入 Codex：[Runtime / Codex](/docs/runtime/codex)
- 需要进阶图片工作流：[Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- 还没有 API Key：[Platform / 创建 API Key](/docs/platform/create-api-key)
