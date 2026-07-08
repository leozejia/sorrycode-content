---
title: 让 AI 记住你的设计风格
slug: remember-design
order: 4
summary: 写一份 DESIGN.md，让 AI 每次生成图片、PPT、网页时都遵守你的品牌色、字体和视觉风格。
section: agent-memory
section_title: 让 AI 记住你的要求
section_order: 15
---

# 让 AI 记住你的设计风格

## 你是不是遇到这些问题

- ❌ 让 AI 生成 10 张图，每张风格都不一样
- ❌ 做 PPT、海报、网页，每次都要重新说"用我们的品牌色"
- ❌ AI 生成的设计看起来像"AI 默认模板"
- ❌ 换一个 agent 或新开会话，之前的设计要求全忘了

**解决方案很简单：写一个叫 DESIGN.md 的文件。**

把它放在你的工作文件夹里，AI 每次生成设计前都会先读它，自动遵守你的设计要求。

## 5 秒速览

```text
问题：AI 不记得我的设计要求
方案：写一个 DESIGN.md 文件
位置：工作文件夹（和你的其他文件放一起）
效果：AI 每次自动读取，保持风格一致
```

<h2 id="comparison">有 DESIGN.md vs 没有 DESIGN.md</h2>

### 没有 DESIGN.md

```text
你：请生成一张产品海报
AI：（生成了渐变背景 + 未来感字体 + 荧光色）
你：不对，我们品牌是克制的，用墨蓝色
AI：（重新生成，风格还是不对）
你：算了，我自己改...
```

### 有 DESIGN.md

```text
你：请先读 DESIGN.md，再生成产品海报
AI：已读取设计规范。将使用墨蓝色主色调、克制排版、留白充足的风格。
你：（一次就对了）
```

<h2 id="what-is-it">DESIGN.md 是什么</h2>

DESIGN.md 是一个文本文件，里面写着你的设计要求：

- 品牌应该是什么气质
- 用什么颜色、字体、字号
- 按钮、卡片、表单长什么样
- 哪些设计坚决不能用

**它不是给人看的设计规范**（那是 Figma 或 Design System）。  
**它是给 AI 看的设计要求**（用自然语言写，AI 能读懂）。

<h2 id="where">放在哪里</h2>

最简单的方式：放在你的工作文件夹里。

```text
我的工作文件夹/
  DESIGN.md          ← 就是这个文件
  assets/            ← 你的素材
  outputs/           ← AI 生成的结果
  其他文件...
```

**不需要"项目"概念。** 就算你的文件散落在桌面、下载文件夹，也可以：

1. 新建一个文件夹
2. 把常用素材扔进去
3. 在里面写一个 DESIGN.md
4. 告诉 AI："进入这个文件夹，读 DESIGN.md，开始做图"

<h2 id="who-reads-it">谁会读取它</h2>

读取者通常是：

- 设计类 skills（SorryCode Image2、Kami、Magazine Web PPT）
- Codex、Claude Code 这类 agent runtime
- Open Design 这类设计工作台
- 能读取文件并生成 UI、图片、PPT 或文档的 agent

它不是某个模型专属，也不是 SorryCode 私有格式。它的价值在于让不同 agent 读取同一份设计要求。

<h2 id="problem">它解决什么问题</h2>

设计任务最容易出现的问题不是"agent 不会做图"，而是风格不稳定：

- 每次都要重新解释品牌色、字体和风格
- agent 记不住哪些设计不能用
- 页面、海报、PPT、图片风格各做各的
- 同一个项目换一个 agent 后，视觉规则丢失
- 输出看起来像默认模板，没有项目自己的气质

DESIGN.md 把这些要求写成可读取的文件，减少口头反复解释。

<h2 id="what-to-write">应该写什么</h2>

一份更完整的 DESIGN.md 通常包括：

- **项目气质：** 这个项目应该给人什么感觉，避免什么误读
- **品牌原则：** 要传达什么，不要传达什么
- **设计 tokens：** 颜色、字体、字号、圆角、间距、阴影
- **组件规范：** 按钮、卡片、表单、导航、弹窗的样式
- **布局原则：** 栅格、响应式、页面密度、留白和信息层级
- **交互状态：** hover、focus、loading、empty、error、success
- **Do / Don't：** 明确推荐和禁止的视觉做法
- **素材位置：** Logo、产品截图、品牌图、图标放在哪里

<h2 id="avoid">不应该写什么</h2>

不要把这些东西写进去：

- API Key、账号密码或供应商密钥
- 临时任务，比如"今天先做首页"
- 无法验证的空话，比如"要非常高级"
- 大段和设计无关的业务闲聊
- 已经过期的品牌规则和旧截图

如果一句话不能帮助 AI 做出更稳定的视觉判断，就不要写进去。

<h2 id="starter">最小模板</h2>

可以先从这份很短的模板开始：

```md
# DESIGN.md

## 项目气质

这个项目应该看起来克制、清楚、可信，不做夸张科技感。

## 颜色

- 主色：墨蓝色
- 辅助色：米白色、浅灰色
- 避免：高饱和荧光色

## 字体和排版

- 中文优先保证可读性
- 标题要清楚，不要过度装饰
- 留白要足，不要把信息塞满

## 图片和素材

- 输入素材放在 `assets/`
- 输出文件放在 `outputs/`

## 禁止事项

- 不要默认 AI 风格
- 不要使用模糊的小字
- 不要把中文标题做成乱码或不可编辑图片
```

<h2 id="advanced">进阶结构</h2>

长期项目可以扩成这个结构：

```md
# DESIGN.md

## Product Context

## Brand Principles

## Design Tokens

### Colors

### Typography

### Spacing

### Radius and Shadow

## Components

### Buttons

### Cards

### Forms

### Navigation

## Layout

## Interaction States

## Accessibility

## Assets

## Do

## Don't
```

<h2 id="how-to-use">怎么让 AI 使用</h2>

把 DESIGN.md 放进工作文件夹后，可以直接说：

```text
请先读取 DESIGN.md，再用 Kami 把这份内容做成一页纸。开始前告诉我你会遵守哪些设计约束。
```

或者：

```text
请先读取 DESIGN.md，再用 SorryCode Image2 生成一张产品海报。保持项目既有视觉风格，输出到 outputs/images/poster/。
```

<h2 id="relationship">它和 skill 的关系</h2>

Skill 负责告诉 AI 某类任务怎么做，比如如何生成图片、如何排版文档、如何做网页 PPT。

DESIGN.md 负责告诉 AI 这个项目应该长什么样。

两者一起用时分工很清楚：skill 给流程，DESIGN.md 给风格边界。

<h2 id="not-perfect">DESIGN.md 不是万能的</h2>

需要理解：

- AI 不是设计师，**它会误读、会理解偏差、会优先级错乱**
- DESIGN.md 只是"每次读一遍"，不是"永久记住"
- 如果你的要求很复杂，AI 可能只记住一部分

所以：

- ✅ 把核心视觉规则写清楚
- ✅ 用 Do / Don't 明确边界
- ✅ 重要任务前，明确提醒 AI："先读 DESIGN.md"
- ❌ 不要指望 AI 完美还原 Figma 设计稿
- ❌ 不要把临时想法写进 DESIGN.md

<h2 id="references">参考</h2>

- Google Labs `design.md`：<https://github.com/google-labs-code/design.md>
- Open Design 的 `DESIGN.md` 设计系统库参考：<https://github.com/VoltAgent/awesome-design-md>

<h2 id="next">接下来</h2>

**如果你想用 DESIGN.md 生成图片、PPT、网页：**

- 先看 [Skills / 精选 Skills](/docs/skills/featured-skills) 找合适的 skill
- 或者看 [Tools / Open Design](/docs/tools/open-design) 了解完整设计工作台

**如果你想让 AI 记住项目的开发规则：**

- 看 [让 AI 记住项目规则](/docs/agent-memory/remember-rules)
