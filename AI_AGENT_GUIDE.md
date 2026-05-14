# AI Agent 执行协议

本文件面向 Codex、Claude Code、OpenCode、Copilot 和其他 AI 工具。用户把本仓库链接交给你时，你的目标不是复述文档，而是按本协议协助用户完成 Claude Desktop / Claude Code 的中文化、优化、MCP / skills 迁移和第三方模型接入。

## 执行目标

完成一次可验证、可回滚、不泄密的 Claude 配置流程：

- 识别当前环境和 Claude 安装状态。
- 备份将要修改的配置和 app 文件。
- 按用户目标配置第三方模型网关、MCP、skills 和汉化。
- 每一步高风险操作先询问用户。
- 修改后运行最小有效验证。
- 最终报告清楚说明做了什么、验证了什么、哪些没做。

## 先读这些文件

1. `README.md`
2. `docs/00-start-here.md`
3. `docs/02-preparation.md`
4. 当前任务相关的编号文档

如果你是 Claude Code、Codex 或 Copilot，还要遵守仓库根目录的 `AGENTS.md`、`CLAUDE.md` 或 `.github/copilot-instructions.md`。

## 禁止行为

- 不读取、输出或提交 `.env*`、token、cookie、private key、credential、secrets。
- 不上传用户真实 `~/.claude.json`、`claude_desktop_config.json`、`.mcp.json`、Claude 日志、MCP 配置或 skills 内容。
- 不把失败的 MCP 写进正式 Claude 配置。
- 不用 Windows shortcut、junction 或 symlink 冒充 Claude skills。
- 不在没有备份时修改 Claude app 文件。
- 不做变量名级、函数名级、协议字段级汉化。
- 不把 Codex / OpenCode / 其他工具的私有权限模型原样复制到 Claude。

## 必须先问用户的动作

以下动作必须先暂停并确认：

- 安装、卸载或升级 Claude Desktop / Claude Code / Node / GitHub CLI / Docker。
- 写入或覆盖 `~/.claude.json`、`~/.claude/settings.json`、`claude_desktop_config.json`、`.mcp.json`。
- 配置第三方模型网关、API key、base URL、模型别名或自定义 headers。
- 修改 Claude app 安装目录中的 JS、asar、chunk 或资源文件。
- 迁移能执行命令、读写文件、控制浏览器、访问 GitHub、访问云服务或签名身份的 MCP。
- 批量复制、删除或覆盖 skills。
- 重启 Claude、停止服务、启动 Docker、修改网络入口。
- 创建、重命名或推送 GitHub 仓库。

## 标准执行阶段

1. 环境盘点：
   检查 Windows、PowerShell、Git、Node、Claude Desktop、Claude Code、可选 GitHub CLI、可选 Docker。只读检查，不修改。

2. 目标确认：
   问清用户要做哪些模块：汉化、第三方模型、MCP、skills、故障排查、发布仓库。不要默认全做。

3. 备份：
   修改配置前运行或等价执行 `scripts/Backup-ClaudeConfig.ps1`。修改 Claude app 文件前单独备份目标文件。

4. 第三方模型：
   验证 HTTPS base URL、`/v1/models`、`/v1/messages`、流式响应和 Claude 日志。不要把 API key 写入仓库。

5. MCP：
   对每个候选 MCP 分类。先用 `scripts/Test-McpServer.ps1` 跑 `initialize` 和 `tools/list`。失败则记录原因，不写正式配置。

6. Skills：
   只复制真实目录。复制前 dry-run，复制后检查 junction、缺失 `SKILL.md` 和重复名称。

7. 汉化：
   先用 `scripts/Patch-ClaudeI18n.ps1 -DryRun` 查看命中，再经用户确认后应用。应用后对修改过的 JS 执行 `node --check`。

8. 重启与日志：
   重启 Claude 前确认。重启后检查 Claude 主日志和 MCP 日志，确认没有新增 fatal error、`Server disconnected`、`Unexpected token`、`ModuleNotFound`。

9. 发布前卫生：
   如果要提交或发布仓库，运行 `scripts/Test-ClaudeProjectHygiene.ps1`、`git diff --check` 和敏感词搜索。

10. 最终报告：
   说明修改面、备份位置、验证命令、通过/失败的 MCP、未完成项和用户需要手动处理的事项。

## 关键询问模板

第三方模型：

```text
请确认第三方模型网关设置：HTTPS base URL 是什么？Claude 侧模型名是什么？API key 由哪个环境变量或本机私有配置提供？是否确认允许我写入 Claude 配置？
```

MCP：

```text
这个 MCP 会获得哪些权限？是否允许我先单独 smoke test，并在通过后写入 Claude 配置？失败的 MCP 我会只记录原因，不写入正式配置。
```

Skills：

```text
是否允许我把指定 skills 复制为真实目录到 Claude skills 目录？我会先 dry-run，确认没有快捷方式、junction、缺失 SKILL.md 或重复项。
```

汉化：

```text
是否允许我修改 Claude app 的 JS 文件？我会先备份，dry-run 命中字符串，应用后执行 node --check，并在失败时恢复备份。
```

## 成功标准

- 所有已写入的配置可解析。
- 所有已启用 MCP 至少通过 `tools/list`。
- Claude 重启后关键日志健康。
- 用户私有信息没有被提交、输出或外泄。
- 用户能根据报告复现或回滚关键步骤。
