# 02. 准备工作

## 先确认目标

执行前先选择要做的模块：

- 只汉化 Claude Desktop。
- 只配置第三方模型网关。
- 只修 MCP disconnected。
- 只迁移 skills。
- 做全套配置。

不同目标需要的权限和依赖不同。不要因为仓库里有脚本，就默认全部执行。

## 基础必需项

- Windows 10 / 11。
- PowerShell 5.1 或 PowerShell 7。
- Git。
- Node.js 18+。
- 官方 Claude Desktop 或 Claude Code。
- 一个备份目录。

## 按需准备项

- Python 3.10+：Python MCP 或本地工具需要时使用。
- GitHub CLI：创建仓库、推送或接入 GitHub MCP 时使用。
- Docker：自建 NewAPI、LiteLLM、one-api、反代、数据库或本地服务时使用。
- Tailscale / Caddy / Nginx / IIS：需要给本地网关提供 HTTPS 域名时使用。
- API key：第三方模型、GitHub、搜索服务、云 MCP 各自需要自己的凭据。

## Docker 是否必需？

不必需。

汉化 Claude、复制 skills、测试本地 stdio MCP 都不需要 Docker。只有你要自己部署模型网关、NewAPI、数据库、反代或某些 MCP 服务时，Docker 才是可选方案。

## 配置前备份

优先使用：

```powershell
.\scripts\Backup-ClaudeConfig.ps1 -BackupRoot .\backups
```

如果 AI 工具不用脚本，也必须等价备份这些可能存在的文件：

- `%USERPROFILE%\.claude.json`
- `%USERPROFILE%\.claude\settings.json`
- `%USERPROFILE%\.claude\CLAUDE.md`
- `%APPDATA%\Claude\claude_desktop_config.json`
- `%LOCALAPPDATA%\Claude-3p\claude_desktop_config.json`

修改 Claude app 文件前，还要单独备份目标 JS / asar / chunk 文件。
