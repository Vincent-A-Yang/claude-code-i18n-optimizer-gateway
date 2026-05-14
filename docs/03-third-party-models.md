# 03. 第三方模型网关

## 目标

让 Claude Desktop / Claude Code 通过 Anthropic API 兼容网关使用第三方模型，同时保留 Claude 侧稳定配置和可诊断日志。

## 需要确认的信息

- HTTPS base URL。
- Claude 侧模型名。
- API key 来源。
- 网关是否需要 `/v1`。
- 网关是否支持 Anthropic messages API。
- 是否支持流式响应。

API key 应通过环境变量或本机私有配置提供，不写进仓库。

## Base URL 原则

优先使用 HTTPS 域名入口。

不建议在 Claude 里写裸 IP HTTPS 地址，因为证书 hostname 校验通常会失败。是否带 `/v1` 取决于 Claude 当前配置面和网关实现，必须实际验证，避免出现 `/v1/v1/models`。

## 验证请求

无 key 时应返回未授权：

```powershell
curl.exe https://gateway.example.com/v1/models
```

带 key 时应返回模型列表：

```powershell
curl.exe https://gateway.example.com/v1/models `
  -H "x-api-key: $env:ANTHROPIC_API_KEY"
```

非流式 messages：

```powershell
curl.exe https://gateway.example.com/v1/messages `
  -H "content-type: application/json" `
  -H "x-api-key: $env:ANTHROPIC_API_KEY" `
  -H "anthropic-version: 2023-06-01" `
  -d '{"model":"claude-sonnet-4-5","max_tokens":32,"messages":[{"role":"user","content":"ping"}]}'
```

流式请求也要单独验证，因为 Claude UI 和 Claude Code 可能走不同路径。

## Claude 日志健康信号

期望看到类似：

```text
ConfigHealth recomputed { state: 'healthy', provider: 'gateway' }
```

不应出现：

- `baseUrl must use https`
- `/v1/v1/models`
- `not an Anthropic model`
- TLS hostname 校验错误
- API key 缺失

## 写入配置前

AI agent 必须先询问用户确认：

```text
请确认第三方模型网关设置：HTTPS base URL 是什么？Claude 侧模型名是什么？API key 由哪个环境变量或本机私有配置提供？是否确认允许我写入 Claude 配置？
```
