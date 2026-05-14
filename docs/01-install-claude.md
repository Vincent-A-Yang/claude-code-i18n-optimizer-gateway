# 01. 安装 Claude Desktop / Claude Code

## Claude Desktop

官方入口：

- 下载页：[https://claude.com/download](https://claude.com/download)
- 安装说明：[Install Claude Desktop](https://support.claude.com/en/articles/10065433-install-claude-desktop)

建议流程：

1. 使用官方安装器安装 Claude Desktop。
2. 启动 Claude Desktop，确认能打开设置页。
3. 如果需要开发者设置、MCP、extensions 或 Claude Code tab，先确认当前版本 UI 中是否存在对应入口。
4. 不要用来源不明的重打包安装器覆盖官方版本。

如果 Claude 提示需要“现代安装程序”，优先重新安装官方 Claude Desktop，不要继续修补旧安装目录。

## Claude Code

官方入口：

- Overview：[https://code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview)
- Settings：[https://code.claude.com/docs/en/settings](https://code.claude.com/docs/en/settings)
- MCP：[https://code.claude.com/docs/en/mcp](https://code.claude.com/docs/en/mcp)

官方文档当前给出的 Windows PowerShell 安装命令是：

```powershell
irm https://claude.ai/install.ps1 | iex
```

也可以使用 WinGet：

```powershell
winget install Anthropic.ClaudeCode
```

执行安装命令前，AI agent 必须先向用户确认。

安装后检查：

```powershell
claude --version
```

如果命令不存在：

- 重新打开终端刷新 PATH。
- 回到官方文档确认当前安装方式。
- 检查是否装在当前用户可访问路径。

## 基础依赖检查

```powershell
git --version
node --version
npm --version
powershell -NoProfile -Command "$PSVersionTable.PSVersion"
```

按需检查：

```powershell
gh --version
gh auth status
docker --version
python --version
```

GitHub CLI 只在需要 GitHub 自动化时安装。Docker 只在需要自建网关或本地服务时安装。
