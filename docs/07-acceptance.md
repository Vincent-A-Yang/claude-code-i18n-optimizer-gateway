# 07. 验收清单

## 安装

- Claude Desktop 来自官方安装器。
- Claude Code 来自官方文档推荐安装方式。
- `git`、`node`、`npm` 可用。
- 按需依赖已经验证，而不是假设存在。

## 备份

- 修改 Claude 配置前已备份。
- 修改 Claude app 文件前已备份目标文件。
- 备份路径已记录。

## 第三方模型

- `/v1/models` 无 key 返回未授权。
- `/v1/models` 带 key 返回成功。
- `/v1/messages` 非流式成功。
- `/v1/messages` 流式成功。
- Claude 日志显示 gateway healthy。

## MCP

- 每个启用 MCP 都通过 `initialize`。
- 每个启用 MCP 都通过 `tools/list`。
- Claude 重启后没有新增 `Server disconnected`。
- 失败 MCP 未写入正式配置。

## Skills

- Claude skills 是真实目录。
- 没有 junction、shortcut 或 symlink。
- 每个 skill 目录包含 `SKILL.md`。
- 没有重复名称。

## 汉化

- 修改过的 JS 通过 `node --check`。
- Claude 能正常启动。
- 目标页面能打开。
- 日志没有新增 fatal error。

## 发布前

```powershell
.\scripts\Test-ClaudeProjectHygiene.ps1
git diff --check
git status --short
```

确认仓库不包含：

- token、API key、cookie、private key。
- 真实 Claude 配置。
- 私有 MCP 配置。
- 私有 skills。
- 日志、截图、内网 IP、私有网关地址。
