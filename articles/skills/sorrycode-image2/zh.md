---
title: SorryCode Image2
slug: sorrycode-image2
order: 2
summary: 用 SorryCode Images API 生成或编辑封面、海报、插图和内容素材；支持 gpt-image-2 和已开放的 Gemini 图片模型。
section: skills
section_title: Skills
section_order: 15
group_order: 20
group_title: 创作与设计
group: creation-design
source_url: https://github.com/linxiverse/sorrycode-image2
---

# SorryCode Image2

`SorryCode Image2` 是给图片生成和简单编辑准备的 skill。它把请求图片接口、检查 API Key、保存结果这些步骤包起来，让你不用先学 HTTP 请求。

如果你的目标是生成封面、海报、文章配图、产品视觉草稿、2D 游戏素材，或者基于已有图片做一次风格调整，建议先装这个 skill。

<h2 id="what-is-it">它解决什么问题</h2>

第一次生成或编辑图片，最容易卡在三件事：

- 不知道应该请求生成接口还是编辑接口
- 不知道 API Key 应该放在哪里
- 不知道结果应该保存在哪里，后续怎么继续改

`SorryCode Image2` 的默认工作方式是：先检查 `SORRYCODE_API_KEY`，没有就停下来引导你创建；有 key 后再调用 SorryCode Images API。你说“生成一张图”时，它走 `/v1/images/generations`；你给出本地图片路径并说“编辑这张图”时，它走 `/v1/images/edits`，并把 prompt、响应记录和图片文件保存到项目里。

当前默认推荐先用 `gpt-image-2` 生成常规 1K / 2K 图片。已开放的 Gemini 图片模型也可以通过同一个 skill 使用，但第一次跑通建议先从默认图片模型和 `1024x1024` 开始。

<h2 id="one-click-install">一键安装</h2>

先确认你已经装好了 `Codex` 或 `Claude Code`。

### Codex

```bash
npx skills add linxiverse/sorrycode-image2 -a codex -g -y
```

### Claude Code

```bash
npx skills add linxiverse/sorrycode-image2 -a claude-code -g -y
```

如果你还没装好 runtime，请先回到：

- [Runtime / Codex](/docs/runtime/codex)
- [Runtime / Claude Code](/docs/runtime/claude-code)

如果不想继续使用，先运行 `npx skills list --global` 确认名称，再用 `npx skills remove --global sorrycode-image2` 卸载。

<h2 id="api-key">让电脑记住你的图片 API Key</h2>

`SorryCode Image2` 需要一个 API Key 才能帮你生成或编辑图片。你可以把它理解成“图片功能的钥匙”。

如果你还没有 API Key，先去 [Platform / 创建 API Key](/docs/platform/create-api-key)。

拿到 `sk-...` 以后，可以先把下面这句话复制给 Codex 或 Claude Code，让 agent 帮你判断怎么设置：

```text
请帮我把 SorryCode 图片 API Key 设置成长期可用。我的 key 是：sk-...。如果当前系统是 Windows，请用用户级 PowerShell 设置；如果是 macOS，请写入 zsh 配置。设置前先告诉我你会改哪里。
```

如果你想自己设置，也可以用下面的命令。

### Windows PowerShell，长期有效

```powershell
[Environment]::SetEnvironmentVariable("SORRYCODE_API_KEY", "你的 sk-...", "User")
```

设置后关闭当前 PowerShell，再重新打开 Codex App 或终端。

### macOS / Linux，长期有效

```bash
echo "export SORRYCODE_API_KEY='你的 sk-...'" >> ~/.zshrc
source ~/.zshrc
```

技术说明：这里实际设置的是 `SORRYCODE_API_KEY`。它只给 SorryCode Image2 读取，不会修改 Codex 的模型配置，也不会影响你平时使用 Codex。

<h2 id="first-prompt">第一句可以说什么</h2>

安装完成后，在你的项目里打开 Codex 或 Claude Code，直接说：

```text
请用 SorryCode Image2 帮我生成一张中文播客封面，主题是 AI 编程，新手友好，暖色调，干净排版。先检查 API Key，如果没设置就告诉我怎么设置；成功后把图片和 response 保存到 outputs/images/first-cover/。
```

你也可以换成：

```text
请生成一个 2D 像素风小游戏主角，蓝色外套，背着小背包，透明背景。保存到 outputs/images/game-character/。
```

如果你已经有一张图片，也可以说：

```text
请用 SorryCode Image2 编辑 ./input/product.png，把它改成更适合作为官网 hero 的视觉图：保留核心界面轮廓，背景更干净，光线更柔和。保存到 outputs/images/product-hero/。
```

如果你想指定比例或分辨率，可以直接说：

```text
请用 SorryCode Image2 生成一张官网 hero 横图，尺寸用 1536x1024。
```

`gpt-image-2` 可使用常见尺寸，例如 `1024x1024`、`1536x1024`、`1024x1536`、`2048x2048`、`2048x1152`。第一次跑通建议先用 `1024x1024`；4K 大图暂不作为默认推荐。

<h2 id="what-it-saves">它会保存什么</h2>

默认建议保存到：

```text
outputs/images/你的任务名/
```

里面至少应该有：

- `prompt.txt`
- `response.json` 或 `events.ndjson`
- 图片文件，或可打开的图片链接说明

这样你下次能找回自己用了什么提示词，也方便继续迭代。

<h2 id="common-issues">常见问题</h2>

- 提示没有 `SORRYCODE_API_KEY`
  先去 [Platform / 创建 API Key](/docs/platform/create-api-key)，再按上面的方式让电脑记住这个 key
- 报 `401`
  API Key 不对，或没有按 `Authorization: Bearer ...` 发出去
- 报 `400`
  通常是图片或参数不符合要求：图片太小、格式不支持、图片损坏，或模型、提示词、尺寸写错。按返回的 `message` 调整；编辑图片时，先换一张能正常打开的 PNG / JPEG / WebP 小图。
- 报 `524`
  通常表示图片生成等待太久。先降低尺寸、缩短 prompt，或按 [Platform / 图像请求](/docs/platform/image-request#common-issues) 的推荐参数重试。
- 报 `502`
  不一定代表平台不可用。先按推荐参数重试；如果持续失败，降低分辨率后再试。
- 报 `503 No available compatible accounts`
  当前 API Key 暂时不能使用这个图片模型。先检查模型名和 Key；如果仍然失败，联系 SorryCode 支持。
- 生成很慢
  图片生成通常比文字慢；只要能持续看到流式事件，可以继续等待

<h2 id="next">下一步</h2>

如果你想按任务走，去 [新手村 / 生成第一张图片](/docs/skills/sorrycode-image2)。

如果你想理解 HTTP 请求细节，再看 [Platform / 图像请求](/docs/platform/image-request)。
