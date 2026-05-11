---
title: 生成第一张图片
slug: first-image
order: 2
summary: 先安装 SorryCode Image2 skill，再用 gpt-image-2 生成第一张封面、海报或插图。
section: village
section_title: 新手村
section_order: 18
group: content-creation
group_title: 内容创作
group_order: 30
---

# 生成第一张图片

<h2 id="goal">任务目标</h2>

用 `SorryCode Image2` 生成第一张图片，并把结果保存到项目里。

这关不要求你先理解 HTTP、参数和图片接口。默认路径是先装 skill，让它帮你检查 API Key、请求图片模型，并把 prompt、响应记录和图片结果保存下来。

<h2 id="prepare">准备物品</h2>

- 已安装 [Codex](/docs/runtime/codex) 或 [Claude Code](/docs/runtime/claude-code)
- 已安装 [Skills / SorryCode Image2](/docs/skills/sorrycode-image2)
- 一个 SorryCode API Key
- 一个图片想法

如果你还没有 API Key，先看 [Platform / 创建 API Key](/docs/platform/create-api-key)。

<h2 id="install-skill">先安装图片 skill</h2>

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

<h2 id="set-key">让电脑记住图片 API Key</h2>

最省心的方式是让 agent 帮你设置。把下面这句话复制给 Codex 或 Claude Code：

```text
请帮我把 SorryCode 图片 API Key 设置成长期可用。我的 key 是：sk-...。如果当前系统是 Windows，请用用户级 PowerShell 设置；如果是 macOS，请写入 zsh 配置。设置前先告诉我你会改哪里。
```

如果你没有设置 key，`SorryCode Image2` 应该先停下来提醒你，而不是继续生成。

技术说明：agent 会帮你设置 `SORRYCODE_API_KEY`。这个名字只给图片 skill 使用，不会影响 Codex 的模型配置。

<h2 id="steps">通关步骤</h2>

1. 安装 `SorryCode Image2`
2. 让电脑记住图片 API Key
3. 在项目里打开 Codex 或 Claude Code
4. 复制下面这句话
5. 确认它把结果保存到 `outputs/images/first-cover/`

<h2 id="prompt">复制这句话</h2>

```text
请用 SorryCode Image2 帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。先检查 API Key，如果没设置就告诉我怎么设置；成功后把图片、prompt 和 response/events 保存到 outputs/images/first-cover/。
```

<h2 id="done">通关标志</h2>

你通关了，如果：

- skill 没有卡在 API Key
- 请求成功返回
- `outputs/images/first-cover/` 里能找到 prompt 和 response 或 events
- 你能打开或下载生成结果

<h2 id="stuck">卡关怎么办</h2>

如果提示没有 `SORRYCODE_API_KEY`，先回到上面的步骤，让电脑记住图片 API Key。

如果报 `401`，检查你设置的 key 是否完整，开头通常是 `sk-...`。

如果报 `503 No available compatible accounts`，说明当前 API Key 暂时不能使用这个图片模型。先检查模型名和 Key；如果仍然失败，联系 SorryCode 支持。

如果请求很慢，可以先等一会儿。遇到 `524` 时，去看 [Platform / 图像请求](/docs/platform/image-request#common-issues)，按图片请求页里的推荐参数排查。

<h2 id="next">下一关</h2>

想继续玩，可以把这张图用到产品介绍、长文章或分享 PPT 里。

想理解底层 HTTP 请求，再看 [Platform / 图像请求](/docs/platform/image-request)。
