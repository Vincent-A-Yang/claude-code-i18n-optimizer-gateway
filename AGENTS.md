# AGENTS.md

本仓库是 `Claude-Code-ZH`：Claude Desktop / Claude Code 中文化、MCP 迁移、skills 同步和第三方模型接入指南。

进入仓库后先读：

1. `README.md`
2. `AI_AGENT_GUIDE.md`
3. `docs/00-start-here.md`
4. 当前任务对应的编号文档

默认中文回复。

## 执行边界

可以做只读检查、dry-run、脚本语法检查、JSON 解析、SVG 解析、仓库卫生检查。

执行以下动作前必须询问用户：

- 安装或卸载软件。
- 写入 Claude 配置。
- 写入 API key、base URL、模型别名或自定义 headers。
- 修改 Claude app 文件。
- 复制或删除 skills。
- 迁移高风险 MCP。
- 重启 Claude 或服务。
- 推送 GitHub。

不要读取、输出或提交 secrets、tokens、`.env*`、credentials、private keys、真实 Claude 配置、私有 MCP 配置、私有 skills、日志或私有网关地址。

## 修改后验证

```powershell
Get-ChildItem .\scripts -Filter *.ps1 | ForEach-Object {
  $tokens=$null; $errs=$null
  $null=[System.Management.Automation.Language.Parser]::ParseFile($_.FullName,[ref]$tokens,[ref]$errs)
  if($errs){ throw "$($_.Name): $($errs[0].Message)" }
}
.\scripts\Test-ClaudeProjectHygiene.ps1
git diff --check
```
