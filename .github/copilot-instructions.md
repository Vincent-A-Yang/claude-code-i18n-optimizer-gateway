# Copilot / AI Agent Instructions

This repository is Chinese-first. Reply in Chinese unless the user asks otherwise.

Before acting, read:

- `README.md`
- `AI_AGENT_GUIDE.md`
- `docs/00-start-here.md`
- The relevant numbered document under `docs/`

Do not commit real Claude/Codex configs, private skills, MCP tokens, logs, gateway hostnames, `.env*`, credentials, or private keys.

Ask the user before installing software, modifying Claude app files, writing API keys, changing Claude config, migrating high-risk MCP servers, copying skill trees, restarting Claude, or pushing to GitHub.

After edits, run:

```powershell
.\scripts\Test-ClaudeProjectHygiene.ps1
git diff --check
```
