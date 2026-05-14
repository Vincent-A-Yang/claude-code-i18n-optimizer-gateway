# 06. 故障排查

## MCP server disconnected

按顺序检查：

1. MCP 命令在普通终端能否启动。
2. 是否应该通过 `cmd /c xxx.cmd` 启动。
3. stdout 是否输出了非 JSON 日志。
4. GUI app 是否拿不到环境变量。
5. Python / Node 依赖是否装在错误版本。
6. 远程服务、浏览器、Docker 或网关是否可达。
7. token 是否缺失或权限不足。

先用脚本单独验证，不要直接写 Claude 配置：

```powershell
.\scripts\Test-McpServer.ps1 -Command "cmd" -McpArgs @("/c", "your-mcp.cmd")
```

## Unexpected token

通常是 MCP stdout 里出现非 JSON 内容，例如：

```text
Starting server...
```

解决方式：

- 查 MCP 是否有 quiet / silent 参数。
- 写 wrapper，把非 JSON 行转到 stderr。
- 修复前不要写入正式 Claude 配置。

## 第三方模型网关不健康

重点检查：

- base URL 是否 HTTPS。
- `/v1` 是否重复或缺失。
- API key 是否传入 Claude。
- 模型名是否能被网关映射。
- `/v1/models` 是否可用。
- `/v1/messages` 非流式和流式是否都可用。

## 汉化后 Claude 打不开

立即恢复备份。

常见原因：

- 替换了非字符串逻辑。
- 破坏了引号或转义。
- 修改了错误 chunk。
- 没有执行 `node --check`。

## Skills 没识别

检查：

- 是否真实目录。
- 是否包含 `SKILL.md`。
- frontmatter `name` 是否重复。
- 是否复制了 fixture、测试目录或私有项目专用 skill。
