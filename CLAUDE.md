# Claude-Code-ZH 项目指令

本仓库是中文优先的 Claude Desktop / Claude Code 配置指南。目标是让 AI 工具能安全地帮助用户完成汉化、第三方模型接入、MCP 迁移和 skills 同步。

开始前先读：

- `README.md`
- `AI_AGENT_GUIDE.md`
- `docs/00-start-here.md`
- 当前任务相关的编号文档

默认中文回复。

修改配置、安装软件、写入 API key、修改 Claude app 文件、复制 skills、迁移高权限 MCP、重启 Claude 或推送 GitHub 前，必须先向用户确认。

不要读取、输出或提交 secrets、tokens、`.env*`、credentials、private keys、真实 Claude 配置、私有 MCP 配置、私有 skills、日志或私有网关地址。

修改后至少运行：

```powershell
.\scripts\Test-ClaudeProjectHygiene.ps1
git diff --check
```
