# 工具测试指南

本文用于确认 MCP 客户端已经正确连接 WJR量化策略MCP。

## 测试前准备

你需要准备：

- MCP 服务地址：`http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse`
- AI 网关消费者 Token
- 一个支持远程 SSE MCP 的客户端，例如 TRAE、Cursor、Cherry Studio 或 Qwen Code

## TRAE 测试

1. 打开 TRAE 的 MCP 配置。
2. 加入 `examples/trae.json` 中的配置。
3. 把 `<你的AI网关消费者Token>` 替换为真实 Token。
4. 重启 TRAE 或刷新 MCP 服务。
5. 在对话里输入：

```text
查看有哪些可用策略。
```

预期结果：

- 客户端能够识别 `wjr-quant-sse`。
- 能看到 `get_strategy_overview`、`get_latest_signal`、`get_strategy_history_and_performance` 三个工具。
- 提问后能返回策略清单或策略资产说明。

## Cursor 测试

1. 打开 Cursor 的 MCP 配置。
2. 加入 `examples/cursor.json` 中的配置。
3. 替换 Token。
4. 重启 Cursor。
5. 输入：

```text
调用 WJR量化策略MCP，查看有哪些可用策略。
```

预期结果同 TRAE。

## 基础测试问题

建议按下面顺序测试：

```text
查看有哪些可用策略。
```

```text
选择一个策略，查看策略介绍和适用边界。
```

```text
查看这个策略的最新信号，限制返回 10 条。
```

```text
查看这个策略的历史信号和历史效果，并解释主要风险。
```

## 测试通过标准

满足以下条件即可认为客户端接入成功：

- MCP 服务能连接成功。
- 工具列表能正常加载。
- 三个工具都能被客户端识别。
- 返回内容没有要求用户提供内部数据库、模型文件或本地路径。
- 返回内容包含风险提示，不把结果描述成确定性投资建议。

## 常见失败现象

| 现象 | 常见原因 |
| --- | --- |
| 连接失败 | URL 填错、网络无法访问、客户端不支持 SSE |
| 401 或认证失败 | Token 错误、Token 未启用、请求头名称写错 |
| 工具列表为空 | 客户端未刷新、服务端工具清单解析失败 |
| 能连接但调用失败 | 入参缺少 `strategy_id` 或 `limit` 类型不正确 |
| 返回很慢 | 网络延迟、网关链路拥塞、客户端超时时间太短 |

排查细节见 [故障排查](troubleshooting.md)。
