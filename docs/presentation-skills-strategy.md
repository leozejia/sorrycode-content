# 演示 / PPT 交付路线

更新时间：2026-05-13

这份文档定义 SorryCode 如何维护 PPT、slides 和演示表达相关内容。它是 `sorrycode-content` 的内部治理文档，不进入线上 docs。

## 核心判断

PPT 不是一个单一工具分类，而是一种交付形态。用户说“做 PPT”时，真实需求可能是：

- 修改已有 `.pptx`
- 快速生成一套网页演示
- 把文章、报告或作品集排成演示材料
- 做高保真视觉方案、信息图或动效感页面
- 做可维护、可评论、可导出的代码式 deck

因此公开文档不能把某一个 skill 写成“PPT 的唯一方案”。应该维护一张“演示 / PPT 交付路线”，再把具体 skill 放进对应路线。

PPT 也是需要迭代的设计类交付。站内不要承诺“一句话得到 100 分 PPT”。公开表达应强调：skill 帮用户从空白页进入可修改初稿，用户通过更具体的反馈，让 agent 逐步靠近这次场景需要的结果。

公开 PPT 页面应该主动链接到 `Skills / 设计类 Skills 怎么用`，让用户先理解：

- 质量问题、场景问题和个人偏好要分开反馈。
- 风格分歧不是一定要修的 bug。
- 高频出现的偏好应该沉淀成 `DESIGN.md`、references 或自己的 skill。

## 当前路线图

| 需求 | 默认入口 | 页面位置 |
| --- | --- | --- |
| 修改已有 PowerPoint、套公司模板、最终交付 `.pptx` | `PPTX` | `Skills / 办公文档` |
| 快速生成有明确视觉风格的网页演示 | `藏师傅的 PPT Skill` | `Skills / 创作与设计` |
| 把文字、报告、简历、作品集整理成纸面风材料或 slides | `Kami` | `Skills / 创作与设计` |
| 做可维护、可评论、可导出 HTML/PDF 的代码式 deck | `Open Slide` | `Tools` |
| 做演示视频、发布动效或社媒 MP4 | `HyperFrames` | `Tools` |

这张表是长期入口。未来出现新的优秀 PPT skill，只加入路线图，不重写整个新手村。

## `藏师傅的 PPT Skill` 怎么定位

上游是 `op7418/guizang-ppt-skill`。站内公开标题使用 `藏师傅的 PPT Skill`，保留作者个人 IP，也避免把它压扁成单一的“杂志风网页 PPT”。

页面要讲清：

- 这是当前收录的一个优秀 PPT 制作 skill，不是 SorryCode 唯一 PPT 方案。
- 它适合用 agent 生成有明确设计系统的单文件 HTML 横向翻页 PPT。
- 当前上游已经覆盖电子杂志风、瑞士国际主义、配图流程、平台封面和质量检查。
- 具体版式数量、主题数量、校验脚本和最新能力以官方仓库为准。

站内不要追着上游 README 逐项同步。站内只维护长期稳定层：

- 适合什么任务
- 不适合什么任务
- 怎么安装
- 怎么触发
- 和 PPTX、Kami、Open Slide 怎么选
- 最近验证口径

当前路由仍是 `/docs/skills/magazine-web-ppt`，但这是现状，不是长期兼容承诺。如果这个 slug 后续被判断为不准确，按 IA 硬切策略执行：删除旧 slug，更新站内链接，不保留别名或兼容页。

## `Kami` 为什么也出现在 PPT 路线里

`Kami` 也能做 slides，但主任务不同。

`Kami` 的核心是排版成品。它适合把文字、访谈、报告、简历、白皮书、作品集整理成稳定、克制、可交付的材料。它做 slides 时，更像纸面文档的演示版。

所以它应该出现在“演示 / PPT 交付路线”里，但单页仍按自己的核心能力写，不改名成 PPT skill。

## 新手村和 Skills 的分工

`新手村 / 做一套分享 PPT` 只给第一次做演示的默认路径。它可以默认使用 `藏师傅的 PPT Skill`，但不要展开完整比较。

`Skills / 创作与设计` 承担路线图。它解释不同 PPT 交付形态该选哪个入口。

单个 skill 页只讲自己的能力，不复制整张路线图，只保留一小段“和其他 PPT 能力怎么选”。

## 公开页面维护规则

改公开页面时优先更新这些文件：

- `articles/skills/creation-design/zh.md`
- `articles/skills/creation-design/en.md`
- `articles/skills/magazine-web-ppt/zh.md`
- `articles/skills/magazine-web-ppt/en.md`
- `articles/village/share-ppt/zh.md`
- `articles/village/share-ppt/en.md`
- `articles/skills/pptx/*`
- `articles/tools/open-slide/*`
- 根 `index.json`
- `articles/skills/index.json`

如果名称、slug、目录、栏目或页面定位被判断为不准确，执行硬切：旧 slug 从根 `index.json`、section index 和站内正文中一次性移除。
