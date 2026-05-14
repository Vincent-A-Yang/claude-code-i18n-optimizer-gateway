# 00. 从这里开始

本项目把 Claude Desktop / Claude Code 的常见改造拆成四个模块：

- 汉化 Claude Desktop。
- 接入第三方模型网关。
- 迁移 MCP。
- 同步 skills。

你可以只做其中一个，也可以按顺序做全套。不要在没有明确目标时一次性修改所有配置。

## 推荐顺序

1. 确认 Claude Desktop / Claude Code 安装状态。
2. 备份 Claude 配置。
3. 接入或验证第三方模型网关。
4. 逐个迁移 MCP。
5. 同步 skills。
6. 汉化 Claude Desktop。
7. 重启 Claude 并检查日志。
8. 按验收清单确认结果。

## 交给 AI 工具执行时

让 AI 先读：

- `README.md`
- `AI_AGENT_GUIDE.md`
- `AGENTS.md`
- `CLAUDE.md`
- 当前任务对应的 `docs/0x-*.md`

AI 必须在高风险操作前询问你。高风险操作包括安装软件、写配置、写 API key、修改 Claude app 文件、复制 skills、迁移高权限 MCP、重启 Claude 和推送 GitHub。

## 不要提交到公开仓库

- 真实 API key、token、cookie、private key。
- 真实 Claude 配置。
- 真实 MCP 配置。
- 私有 skills。
- Claude / Codex / 浏览器日志。
- 内网 IP、Tailscale 域名、私有网关地址。
