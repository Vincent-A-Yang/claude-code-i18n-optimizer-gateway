# 04. MCP 与 Skills

## MCP 迁移原则

不要把其他工具里的 MCP 配置原样复制到 Claude。

迁移前先分类：

- 本地 stdio MCP。
- 本地 wrapper + 远程依赖。
- 云服务 MCP。
- 浏览器自动化 MCP。
- 文件系统 / 命令执行 MCP。
- 身份、签名、账号类高风险 MCP。

高风险 MCP 需要用户明确确认权限范围。

## MCP 最低验证标准

配置写入 Claude 前，先跑协议级 smoke test：

```powershell
.\scripts\Test-McpServer.ps1 -Command "cmd" -McpArgs @("/c", "context7-mcp.cmd", "--transport", "stdio")
```

通过标准：

- 进程能启动。
- `initialize` 有响应。
- `tools/list` 有响应。
- 没有提前退出。
- stdout 没有非 JSON 噪声导致解析失败。

失败 MCP 不写入正式 Claude 配置，只记录原因。

## Windows 启动建议

Node / npm 安装的 MCP 常见入口是 `.cmd`。Claude Desktop 作为 GUI app 启动时，优先使用：

```json
{
  "command": "cmd",
  "args": ["/c", "example-mcp.cmd", "--transport", "stdio"]
}
```

如果 MCP 会在 stdout 输出启动横幅，需使用 quiet 参数或 wrapper，把非 JSON 输出转到 stderr。

## Skills 同步原则

Claude skills 应是实目录：

- 不用 `.lnk`。
- 不用 junction。
- 不用 symlink。
- 每个 skill 目录必须有 `SKILL.md`。
- frontmatter `name` 应唯一。
- 不复制测试 fixture 或私有项目专用 skill。

先 dry-run：

```powershell
.\scripts\Sync-ClaudeSkills.ps1 -Source "$HOME\.codex\skills" -Destination "$HOME\.claude\skills" -DryRun
```

确认后再复制。复制前必须询问用户。

## 不要提交

- 真实 MCP token。
- 真实 MCP config。
- 私有 skills 内容。
- 真实远程服务地址。
- 含 prompt、账号或路径的日志。
