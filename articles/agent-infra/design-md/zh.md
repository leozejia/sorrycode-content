---
title: DESIGN.md 是什么
slug: design-md
order: 5
summary: DESIGN.md 是设计 agent 的上下文文件。它把产品目标、品牌原则、设计 tokens、组件、布局和禁用规则写成可复用标准。
section: agent-infra
section_title: Agent 基建
section_order: 32
---

# DESIGN.md 是什么

`DESIGN.md` 是写给设计 agent 的上下文文件。

它和 `AGENTS.md / CLAUDE.md` 属于同一类心智：把长期上下文写进文件，让 agent 在后续任务里读取并遵守。区别是，`AGENTS.md / CLAUDE.md` 更偏项目规则和工作方式，`DESIGN.md` 更偏产品长什么样、界面怎么组织、视觉和交互不能跑偏。

Google Labs 已经发布 `design.md` alpha 规范和 CLI，所以它可以视为正在形成的 AI 设计协作新约定。当前不能把它说成完全定稿的行业标准，但已经值得作为事实依据纳入站内文档。

<h2 id="who-reads-it">谁会读取它</h2>

读取者通常是：

- 设计类 skills
- Codex、Claude Code 这类 agent runtime
- Open Design 这类设计工作台
- 能读取项目文件并生成 UI、图片、PPT 或文档的 agent

它不是某个模型专属，也不是 SorryCode 私有格式。它的价值在于让不同 agent 读取同一份设计上下文。

<h2 id="problem">它解决什么问题</h2>

设计任务最容易出现的问题不是“agent 不会写代码”，而是上下文不稳定：

- 每次都要重新解释品牌色、字体和风格
- agent 记不住哪些设计不能用
- 页面、海报、PPT、图片风格各做各的
- 同一个项目换一个 agent 后，视觉规则丢失
- 输出看起来像默认模板，没有项目自己的气质

`DESIGN.md` 把这些要求写成可读取的项目文件，减少口头反复解释。

<h2 id="where">放在哪里</h2>

最常见位置是项目根目录：

```text
your-project/
  DESIGN.md
  AGENTS.md
  README.md
  assets/
  outputs/
```

如果项目很大，也可以在子目录放更具体的 `DESIGN.md`，比如 `apps/web/DESIGN.md`。但公开文档默认先推荐根目录，一个项目一份，最容易理解和维护。

<h2 id="what-to-write">应该写什么</h2>

一份更完整的 `DESIGN.md` 通常包括：

- 产品目标：这个产品服务谁，核心体验是什么
- 品牌原则：要传达什么气质，避免什么误读
- 设计 tokens：颜色、字体、字号、圆角、间距、阴影、动效
- 组件规范：按钮、卡片、表单、导航、弹窗、状态样式
- 布局原则：栅格、响应式、页面密度、留白和信息层级
- 交互状态：hover、focus、loading、empty、error、success
- 可访问性：对比度、键盘导航、语义结构
- Do / Don’t：明确推荐和禁止的视觉做法
- 素材位置：Logo、产品截图、品牌图、图标放在哪里

<h2 id="avoid">不应该写什么</h2>

不要把这些东西写进去：

- API Key、账号密码或供应商密钥
- 临时任务，比如“今天先做首页”
- 无法验证的空话，比如“要非常高级”
- 大段和设计无关的业务闲聊
- 已经过期的品牌规则和旧截图

如果一句话不能帮助 agent 做出更稳定的视觉判断，就不要写进去。

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

<h2 id="how-to-use">怎么让 agent 使用</h2>

把 `DESIGN.md` 放进项目目录后，可以直接说：

```text
请先读取 DESIGN.md，再用 Kami 把这份内容做成一页纸。开始前告诉我你会遵守哪些设计约束。
```

或者：

```text
请先读取 DESIGN.md，再用 SorryCode Image2 生成一张产品海报。保持项目既有视觉风格，输出到 outputs/images/poster/。
```

<h2 id="relationship">它和 skill 的关系</h2>

Skill 负责告诉 agent 某类任务怎么做，比如如何生成图片、如何排版文档、如何做网页 PPT。

`DESIGN.md` 负责告诉 agent 这个项目应该长什么样。

两者一起用时更稳：skill 给流程，`DESIGN.md` 给风格边界。

<h2 id="references">参考</h2>

- Google Labs `design.md`：<https://github.com/google-labs-code/design.md>
- Open Design 的 `DESIGN.md` 设计系统库参考：<https://github.com/VoltAgent/awesome-design-md>
