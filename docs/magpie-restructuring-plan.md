# AGENTS 入口规范

更新时间：2026-10-27

本决议替代原 Magpie 重构草案中的厂商分组、模型版本专页、CLI 场景命令与重定向方案。长期栏目规则以 `information-architecture.md` 为准。

## 默认路线

创建匹配分组的 API Key -> Magpie 图形界面添加自定义供应商并获取模型 -> 安装并启用 Agent -> 第一个文件任务。不知道选什么时默认 Codex。

## 栏目

`articles/agents/` 与 `/docs/agents/*`，中英文展示名均为 `AGENTS`，导航平铺：

- `magpie`：唯一共享配置教程，保留四张截图。
- `agent-setup`：合并 Codex、Claude Code、DSH、WorkBuddy 和其他 Agent 的共同流程，保留各自安装、启动、工作区、模型选择与权限步骤。
- `cursor`：保留桌面编辑器手动配置及独立限制。历史步骤尚未在当前版本复测，不承诺可用，不混同 CLI 或 Private Inference。

不新增 models 栏目或型号清单。不再维护 Fable、Agent 扩展机制和四篇媒体 API 独立教程，Claude Desktop Gateway 路线也退出默认推荐。不指定具体 Skill 承接图片或办公任务；Skills 只在核心概念保留一篇，所需工具、凭证和权限不由 Magpie 接入代替。

## 维护与验证

- 已验证的特殊手动路径可保留；不可把历史配置当作当前已验证事实。Magpie 共用配置不在各客户端重复。
- 新工具只有出现独立、稳定的上手需求才新增文章，否则先进入其他 Agents。
- 改栏目、slug 或删文章时，正文、双语索引、站内链接和可复制给 Agent 的提示一起改；不保留旧路由或重定向。
- 验证双语元数据、三篇平铺顺序、站内链接、图片与 Markdown 入口。客户端实际调用未测试时，不宣称已通过真机验证。
- 内容 push 到 `main` 后由生产每五分钟同步本地只读快照，不重建应用。上线后核对内容 index、目标文章、图片和机器入口；异常按主项目公开内容恢复流程处理。
