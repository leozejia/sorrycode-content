# 公开文章图片资源使用规范

更新时间：2026-08-06

这份文档定义 `sorrycode-content` 中公开图片的存放、引用和安全要求。文章封面与正文插图都通过 `sorrycode` 的资源代理读取和缓存。

## 基本规则

图片和使用它的文章放在同一个目录：

```text
articles/<section>/<slug>/
  zh.md
  en.md
  cover.png
  install-success.webp
```

不要使用共享图片目录或跨文章相对路径。两篇文章需要同一张图时，各自保存一份，避免一篇文章的资源变动影响另一篇。

适合公开的图片包括文章封面、产品截图、成功结果、示意图和已确认可以公开的 skill 产物。图片不得包含：

- API Key、token、密码、验证码或密钥片段
- 用户私人信息、真实订单或后台账号
- 内部供应商、私有路由、生产日志或排障记录

不确定是否可以公开时，先留在媒体工作区或本地草稿。

## 文件名、格式和大小

文件名使用小写英文、短横线和明确含义，不建图片子目录。可以使用 `.png`、`.jpg`、`.jpeg`、`.webp` 和 `.gif`，不能使用 `.svg`、`.pdf`、`.mp4`、`.html`、`.zip` 或 `.psd`。

单个图片必须小于 5 MB。普通截图优先使用 `.webp` 或压缩后的 `.png`。

推荐：

```text
cover.png
install-success.webp
first-request-result.webp
```

不要使用带空格、中文、临时版本号、子目录或 `..` 的文件名。

## 封面图

封面通过根 `index.json` 的 `coverPath` 声明：

```json
{
  "coverPath": "articles/tools/codex-history/cover.png"
}
```

一个 article entry 最多声明一张封面。中英文可以共用封面。只在正文出现的图片不写入 `coverPath`。

## 正文插图

正文使用 Markdown 相对图片语法：

```md
![安装成功截图](./install-success.webp)
```

也可以省略 `./`。不要引用父目录、图片子目录、外部图床，也不要使用 HTML `<img>`。

正文必须保留完整说明。截图不能成为命令、参数、错误信息或结论的唯一来源，Agent 只读 `.md?locale=...` 的文字和代码时也应能理解页面。

## 外部图片

默认不使用外部图床或 GitHub raw 图片。外部资源无法统一缓存和校验，也可能失效或被替换。确实需要引用时，先确认公开必要性和授权；可以安全保存的，放入文章目录。

## 提交前检查

- 图片位于对应 `articles/<section>/<slug>/` 目录
- Markdown 使用文件名或 `./filename.ext`
- 文件名、格式和大小符合本页要求
- 图片不含敏感信息
- `coverPath` 只指向封面
- 正文不依赖截图传达必要信息

运行 JSON 校验：

```bash
jq empty index.json articles/*/index.json
```

检查超过 5 MB 的图片：

```bash
find articles -type f \( -name '*.png' -o -name '*.jpg' -o -name '*.jpeg' -o -name '*.webp' -o -name '*.gif' \) -size +5M
```

命中结果必须处理后再提交。
