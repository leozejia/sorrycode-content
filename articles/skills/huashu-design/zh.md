---
title: Huashu Design
slug: huashu-design
order: 5
summary: 第三方设计 skill。适合 App 原型、HTML/PPT、动效、信息图、设计变体和专家评审；个人使用免费，商业使用需授权。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/alchaincyf/huashu-design
---

# Huashu Design

`Huashu Design` 是一个第三方设计 skill。

它适合更复杂的设计交付：App 原型、HTML 幻灯片、可编辑 PPTX、动效、信息图、设计变体和专家评审。

如果 `Kami` 更像成品文档和纸面表达，`藏师傅的 PPT Skill` 更像有设计系统的网页演示，`Huashu Design` 更像把 agent 带进一个设计师工作流：先问清需求，找品牌资产，给方向，再产出并自检。

<h2 id="what-it-does">它能做什么</h2>

常见用途：

- 可点击 App / Web 原型
- HTML deck 和可编辑 PPTX
- 产品发布动效、MP4 / GIF
- 信息图和数据可视化
- 多个设计方向并排比较
- 五维专家评审和修改建议

<h2 id="install">安装</h2>

先确认你已经装好了 `Codex` 或 `Claude Code`。

### Codex

```bash
npx skills add alchaincyf/huashu-design -a codex -g -y
```

### Claude Code

```bash
npx skills add alchaincyf/huashu-design -a claude-code -g -y
```

如果安装器或上游命令有变化，以官方仓库为准：<https://github.com/alchaincyf/huashu-design>

<h2 id="first-prompt">第一句话</h2>

```text
请用 Huashu Design 帮我做一个番茄钟 App 的 iOS 原型，4 个屏幕，可点击。先问我必要问题，再给 3 个设计方向让我选。
```

做动效：

```text
请用 Huashu Design 把这个产品发布逻辑做成 30 秒动效。先给脚本和视觉方向，不要直接生成最终文件。
```

做设计评审：

```text
请用 Huashu Design 对这个页面做五维专家评审，指出保留项、问题和最快能改的地方。
```

<h2 id="license">授权边界</h2>

`Huashu Design` 不是 SorryCode 自有 skill。

根据上游许可证，个人学习、研究、个人内容创作和非营利分享可以免费使用。公司、团队、工作室、机构使用，或用于付费客户交付、商业产品、付费课程和商单创作，需要事先获得作者授权。

如果你要用于商业项目，先看上游许可证并联系作者。

<h2 id="relationship">和其他设计能力的关系</h2>

- `SorryCode Image2`：图片生成和编辑
- `Kami`：一页纸、简历、报告、作品集和纸面风幻灯片
- `藏师傅的 PPT Skill`：有明确视觉风格的网页演示
- `Huashu Design`：更复杂的原型、动效、信息图和设计评审
- `DESIGN.md`：项目设计上下文文件，见 [Agent 基建 / DESIGN.md](/docs/agent-infra/design-md)
