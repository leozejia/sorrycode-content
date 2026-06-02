# 公开文章图片资源使用规范

更新时间：2026-05-27

这份文档给直接维护 `sorrycode-content` 的运营和内容同学使用。它是内部治理文档，不进入线上 docs。

## 当前状态

当前线上已经稳定支持文章封面：

- 在 `index.json` 里写 `coverPath`
- 图片放在对应文章目录下
- `sorrycode` 会通过后端资源代理读取并缓存

正文插图使用 Markdown 相对图片语法。`sorrycode` 会把同文章目录下的安全图片改写到站内资源代理，并在浏览器 docs 和 `.md?locale=...` 机器出口中稳定读取。

推荐写法：

```md
![安装成功截图](./install-success.png)
```

图片文件放在同一篇文章目录：

```text
articles/runtime/codex/
  zh.md
  en.md
  install-success.png
```

## 可以放什么

适合放在文章同目录的公开图片：

- 文章封面，例如 `cover.png`
- 产品界面截图
- 安装成功、运行成功、生成结果的示例截图
- 对外可公开的示意图、流程图、结果图
- 已确认可以公开的 skill 产物示例

图片必须满足：

- 不包含 API Key、token、密码、邮箱验证码、密钥片段
- 不包含用户私人信息、真实订单、后台账号、内部供应商、私有路由
- 不包含生产日志、请求响应诊断、成本明细或内部排障记录
- 不依赖外部图床才能展示

不确定能不能公开时，不要提交到 `sorrycode-content`。先放在媒体工作区或本地草稿，确认后再进入公开仓库。

## 文件位置

图片必须和使用它的文章放在同一个目录：

```text
articles/<section>/<slug>/<locale>.md
articles/<section>/<slug>/<image-file>
```

正确：

```text
articles/tools/codex-history/zh.md
articles/tools/codex-history/cover.png
articles/tools/codex-history/session-list.webp
```

错误：

```text
articles/tools/codex-history/images/session-list.webp
articles/tools/shared/session-list.webp
docs/session-list.webp
```

不要跨文章复用图片路径。即使两篇文章使用同一张图，也先复制到各自文章目录，避免一篇文章的资源修改影响另一篇。

## 文件命名

推荐：

- 小写英文
- 短横线分隔
- 语义化
- 单段文件名，不建子目录

示例：

```text
cover.png
install-success.png
first-request-result.webp
deck-preview.jpg
```

不要使用：

```text
截图 1.png
IMG_20260527.PNG
final-final-v3.png
../secret.png
images/step-1.png
```

## 格式和大小

允许格式：

- `.png`
- `.jpg`
- `.jpeg`
- `.webp`
- `.gif`

不允许：

- `.svg`
- `.pdf`
- `.mp4`
- `.html`
- `.zip`
- `.psd`

单个图片必须小于 5 MB。普通截图优先用 `.webp` 或压缩后的 `.png`。

## 封面图

封面图通过 `coverPath` 声明：

```json
{
  "coverPath": "articles/tools/codex-history/cover.png"
}
```

规则：

- `coverPath` 只表示文章封面。
- `coverPath` 不是正文图片清单。
- 一个 article entry 最多一个封面。
- 中文和英文同一篇文章可以共用同一张封面。

如果一张图只用于正文，不要把它写进 `coverPath`。

## 正文插图

正文插图能力上线后，推荐写法：

```md
![Codex session 列表截图](./session-list.webp)
```

也可以省略 `./`：

```md
![Codex session 列表截图](session-list.webp)
```

不要写：

```md
![截图](../shared/session-list.webp)
![截图](images/session-list.webp)
![截图](https://raw.githubusercontent.com/...)
<img src="./session-list.webp">
```

正文里必须保留文字解释。截图只能辅助理解，不能成为命令、参数、错误信息或结论的唯一来源。Agent 读取 `.md?locale=...` 时，应该只看文字和代码也能理解页面。

## 外部图片

默认不要使用外部图床或 GitHub raw 图片。

原因：

- 站内无法统一缓存和校验。
- 外部资源可能失效、变慢或被替换。
- Agent-readable Markdown 需要稳定、可解释的资源地址。

如果确实需要引用外部图片，先判断这是不是公开 docs 应该承载的内容。能下载并确认授权的，优先放进文章目录。

## 提交前检查

至少检查：

- 图片在 `articles/<section>/<slug>/` 下。
- Markdown 引用的是 `./filename.ext` 或 `filename.ext`。
- 文件名没有空格、中文、子目录或 `..`。
- 图片不含敏感信息。
- `index.json` 的 `coverPath` 只指向封面。
- 正文截图旁边有足够文字说明。

JSON 校验：

```bash
jq empty index.json articles/*/index.json
```

检查图片大小：

```bash
find articles -type f \( -name '*.png' -o -name '*.jpg' -o -name '*.jpeg' -o -name '*.webp' -o -name '*.gif' \) -size +5M
```

命中结果必须处理后再提交。
