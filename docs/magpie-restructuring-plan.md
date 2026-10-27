# AGENTS 入口规范

更新时间：2026-10-27

本决议替代原 Magpie 重构草案中的厂商分组、模型版本专页、CLI 场景命令与重定向方案。长期栏目规则以 `information-architecture.md` 为准。

## 默认路线

创建匹配分组的 API Key -> Magpie 图形界面添加自定义供应商并获取模型 -> 安装并启用 Agent -> 第一个文件任务。不知道选什么时默认 Codex。

## 栏目

`articles/agents/` 与 `/docs/agents/*`，中英文展示名均为 `AGENTS`，导航平铺：

- `magpie`：唯一共享配置教程，保留已确认的四张截图。
- `codex`、`claude-code`、`dsh`、`workbuddy`：安装、在 Magpie 启用、首次任务。
- `other-agents`：OpenCode、Pi、Kimi Code、Grok Build、Cursor 的官方入口与必要边界。

不新增 models 栏目或型号清单。不再维护 Fable、Agent 扩展机制和四篇媒体 API 独立教程，Claude Desktop Gateway 路线也退出默认推荐。图片任务由现有 SorryCode Image2 Skill 承接，Skill 所需凭证不由 Magpie 接入代替。

## 维护与验证

- 各 Agent 页不保留第二套接入脚本、手改配置或密钥环境变量教程。
- 新工具只有出现独立、稳定的上手需求才新增文章，否则先进入其他 Agents。
- 改栏目、slug 或删文章时，正文、双语索引、站内链接和可复制给 Agent 的提示一起改；不保留旧路由或重定向。
- 验证双语元数据、六篇平铺顺序、站内链接、图片与 Markdown 入口。客户端实际调用未测试时，不宣称已通过真机验证。
- 内容 push 到 `main` 后由生产每五分钟同步本地只读快照，不重建应用。上线后核对内容 index、目标文章、图片和机器入口；异常按主项目公开内容恢复流程处理。
