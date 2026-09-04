---
title: 让 AI 记住你的设计风格
slug: remember-design
order: 4
summary: 用 DESIGN.md 保存项目的品牌色、字体和视觉约束，并明确让 Agent 在设计任务中读取它。
section: agent-memory
section_title: 让 AI 记住你的要求
section_order: 15
---

# 让 AI 记住你的设计风格

设计任务经常要重复说明品牌色、字体、版式和禁用风格。把这些稳定要求写进 `DESIGN.md`，不同会话和工具就能读取同一份设计约束。

`DESIGN.md` 不是所有 Agent 都会自动识别的通用协议。需要在项目规则、Skill 说明或当前任务中明确要求 Agent 读取它。

<h2 id="what-is-it">DESIGN.md 是什么</h2>

`DESIGN.md` 是一个写给 Agent 读取的文本文件，可以包括：

- 品牌应该是什么气质
- 用什么颜色、字体、字号
- 按钮、卡片、表单长什么样
- 哪些设计不能使用

它可以补充 Figma 或现有设计系统，但不能代替原始设计稿、组件库和人工验收。

<h2 id="where">放在哪里</h2>

把文件放在相关素材和输出目录所在的工作文件夹中：

```text
我的工作文件夹/
  DESIGN.md
  assets/
  outputs/
```

<h2 id="who-reads-it">谁会读取它</h2>

可以读取它的通常包括：

- 明确支持该文件的设计类 Skills
- Codex、Claude Code 这类能读取项目文件的 Agent
- Open Design 这类设计工作台

能读取文件不代表会主动寻找 `DESIGN.md`。使用前仍要确认当前工具或 Skill 的说明。

<h2 id="what-to-write">应该写什么</h2>

一份更完整的 DESIGN.md 通常包括：

- **项目气质：** 这个项目应该给人什么感觉，避免什么误读
- **品牌原则：** 要传达什么，不要传达什么
- **设计参数：** 颜色、字体、字号、圆角、间距、阴影
- **组件规范：** 按钮、卡片、表单、导航、弹窗的样式
- **布局原则：** 栅格、响应式、页面密度、留白和信息层级
- **交互状态：** hover、focus、loading、empty、error、success
- **推荐和禁止事项：** 明确可用和不可用的视觉做法
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

<h2 id="how-to-use">怎么让 AI 使用</h2>

把 `DESIGN.md` 放进工作文件夹后，在任务中明确要求读取：

```text
请先读取 DESIGN.md，再用 Kami 把这份内容做成一页纸。开始前告诉我你会遵守哪些设计约束。
```

项目长期使用时，可以在 `AGENTS.md`、`CLAUDE.md` 或对应工具的项目规则中引用它。具体规则文件以当前 Agent 的官方说明为准。

图片任务也可以直接说：

```text
请先读取 DESIGN.md，再读取 [GPT Image 2](/docs/runtime/gpt-image-2) 文档，生成一张产品海报。保持项目既有视觉风格，输出到 outputs/images/poster/。
```

<h2 id="relationship">它和 skill 的关系</h2>

Skill 提供任务流程，`DESIGN.md` 保存当前项目的视觉约束。只有 Skill 或任务明确读取了该文件，这些约束才会进入当前上下文。

<h2 id="not-perfect">DESIGN.md 不是万能的</h2>

- Agent 可能漏读、误解或忽略部分规则，重要产物仍需检查
- 复杂设计不要只靠自然语言描述，继续提供原始素材、截图或组件规范
- 规则变化后及时更新文件，删除过期截图和要求

<h2 id="references">参考</h2>

- Google Labs `design.md`：<https://github.com/google-labs-code/design.md>
- Open Design 的 `DESIGN.md` 设计系统库参考：<https://github.com/VoltAgent/awesome-design-md>

<h2 id="next">接下来</h2>

- 选择设计类能力：[Skills / 创作与设计](/docs/skills/creation-design)
- 了解设计工作台：[Tools / Open Design](/docs/tools/open-design)
- 保存开发规则：[让 AI 记住项目规则](/docs/agent-memory/remember-rules)
