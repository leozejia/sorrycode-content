# 运营重构手册

更新时间：2026-05-13

这份文档给直接维护 `sorrycode-content` 的运营同学使用。它是内部治理文档，不进入线上 docs。

## 先读什么

开始重构前，按这个顺序读：

1. `README.md`
   了解仓库结构、公开内容 contract、根 `index.json` 和 section index 的格式。
2. `docs/information-architecture.md`
   了解栏目职责、页面职责、硬切策略和收录原则。
3. 相关专题策略文档
   例如重构 PPT / slides 内容时读 `docs/presentation-skills-strategy.md`。
4. 要改的公开页面
   同时读中文和英文版本，例如 `articles/skills/design-workflow/zh.md` 和 `articles/skills/design-workflow/en.md`。
5. 相关 section index
   例如改 Skills，就读 `articles/skills/index.json`。

## 重构前先判断

不要先改字。先判断这次问题属于哪一类：

| 问题 | 应该怎么处理 |
| --- | --- |
| 名称不准确 | 改标题、摘要、slug 和站内链接 |
| 页面放错栏目 | 移动栏目或分组，并更新 section index |
| 一个页面承担了多个任务 | 拆页，分别给清楚的定位 |
| 多个页面重复解释同一件事 | 留一个主页面，其他页面只链接过去 |
| 某个 skill 被写成整个任务域 | 先做路线图，再写单个 skill |
| 上游能力变化 | 只更新站内长期稳定层，不搬运完整 README |

如果名称、slug、目录路径、栏目、分组或页面定位表达不正确，默认硬切，不保留旧路径，也不做兼容页。

## 硬切清单

改 slug、目录、栏目或页面定位时，必须同时更新：

- `articles/<section>/<slug>/` 目录名
- `zh.md` 和 `en.md` frontmatter
- 根 `index.json`
- 对应 `articles/<section>/index.json`
- 站内所有 `/docs/<section>/<slug>` 链接
- 相关内部策略文档

不要只改 Markdown 正文。线上导航和接口主要看 `index.json` 和 section index。

## 写公开页的基本口径

公开 docs 要 beginner-first、agent-first。

- 先告诉用户什么时候用，而不是先讲概念史。
- 先给最短可执行路径，再给边界和比较。
- 用自然语言触发示例，帮助用户直接复制给 agent。
- 不承诺万能效果，不把工具写成魔法。
- 不暴露内部账号池、供应商、私有路由、凭证、日志或生成诊断。
- 强主观产物要写成“可修改初稿 + 具体反馈 + 逐步迭代”的方法，不写成情绪化立场。

## 写单个 skill 页面

单个 skill 页只讲这个 skill：

- 它是什么
- 适合什么
- 不适合什么
- 怎么安装
- 怎么触发
- 第一话怎么说
- 常见问题
- 上游参考

不要把单个 skill 写成整个任务域。比如 PPT 不是一个 skill，PPT 是交付形态；具体 skill 只是其中一条路线。

## 写路线图页面

当一个任务有多条路线时，先写路线图。

路线图应该回答：

- 用户真正要交付什么
- 默认入口是什么
- 哪些情况应该换路线
- 新手默认路径是什么
- 更专业的工具在哪里继续读

路线图不要复制每个工具页的详细安装步骤。它负责分流，不负责替每个页面展开。

## 提交前校验

至少运行：

```bash
jq empty index.json articles/*/index.json
```

如果改了 slug 或站内链接，再跑一次内容一致性检查：

```bash
python3 - <<'PY'
import json, pathlib, re, sys
root = pathlib.Path('.')
idx = json.loads((root / 'index.json').read_text())
articles = idx['articles']
keys = {(a['section'], a['slug']) for a in articles}
errors = []

for a in articles:
    path = root / a['markdownPath']
    if not path.is_file():
        errors.append(f"missing markdownPath: {a['markdownPath']}")
    expected_route = f"/docs/{a['section']}/{a['slug']}"
    if a['route'] != expected_route:
        errors.append(f"route mismatch: {a['route']} != {expected_route}")
    expected_path = f"articles/{a['section']}/{a['slug']}/{a['locale']}.md"
    if a['markdownPath'] != expected_path:
        errors.append(f"path mismatch: {a['markdownPath']} != {expected_path}")

for section_index in sorted(root.glob('articles/*/index.json')):
    data = json.loads(section_index.read_text())
    section = data['section']
    for slug in data.get('articles', []):
        if (section, slug) not in keys:
            errors.append(f"missing article in section list: {section}/{slug}")
    for group in data.get('navigation', {}).get('groups', []):
        for slug in group.get('items', []):
            if (section, slug) not in keys:
                errors.append(f"missing article in group: {section}/{slug}")

route_re = re.compile(r'\\]\\(/docs/([^/)]+)/([^/#)]+)')
for md in sorted(root.glob('articles/**/*.md')):
    for match in route_re.finditer(md.read_text()):
        key = (match.group(1), match.group(2))
        if key not in keys:
            errors.append(f"broken doc link in {md}: /docs/{key[0]}/{key[1]}")

if errors:
    print('\\n'.join(errors))
    sys.exit(1)

print('content index validation passed')
PY
```

## 上线预期

push 到 `main` 后，公开文章会通过 `sorrycode` 后端代理热更新。生产后端有缓存，通常等几分钟再看线上结果。
