# 工具测试指南

本文用于确认 MCP 客户端已经正确连接 WJR 量化策略 MCP。

## 1. 检查客户端配置

配置示例：

```json
{
  "mcpServers": {
    "wjr-quant-sse": {
      "type": "sse",
      "url": "http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse",
      "headers": {
        "Authorization": "Bearer <你的 AI 网关消费者 Token>"
      }
    }
  }
}
```

确认点：

- 客户端能够识别 `wjr-quant-sse`。
- 能看到 `get_strategy_overview` 和 `get_strategy_report` 两个工具。
- 看不到健康检查、资产目录、技术测试、发布索引等内部工具。

## 2. 测试策略清单

在客户端里问：

```text
有哪些可用策略？
```

预期结果：

- 客户端调用 `get_strategy_overview`。
- 返回策略清单、策略 ID、策略名称、状态、是否有最新信号、是否有历史信号和效果材料。
- 返回内容包含风险提示。

## 3. 测试指定策略介绍

拿上一步返回的 `strategy_id`，继续问：

```text
介绍一下这个策略，它适合什么场景？
```

预期结果：

- 客户端调用 `get_strategy_overview`，并带上 `strategy_id`。
- 返回策略介绍、规则说明、适用边界和风险说明。

## 4. 测试最新信号

继续问：

```text
查看这个策略的最新信号，并解释字段是什么意思。
```

预期结果：

- 客户端调用 `get_strategy_report`。
- `report_type` 应为 `latest_signal`。
- 返回最新信号、仓位或排序字段、图表数据和风险提示。

## 5. 测试历史信号和策略效果

继续问：

```text
查看这个策略的历史信号和历史效果，重点说明风险。
```

预期结果：

- 客户端调用 `get_strategy_report`。
- `report_type` 可以是 `history`、`performance` 或 `full`。
- 返回历史信号时间线、核心效果指标、风险说明和免责声明。

## 6. 最终验收

验收通过标准：

- MCP 服务能连接成功。
- 工具列表能正常加载。
- 公开工具只有两个：`get_strategy_overview`、`get_strategy_report`。
- 返回内容没有要求用户提供内部数据库、模型文件或本地路径。
- 返回内容包含风险提示，不把结果描述成确定性投资建议。
- Token 不出现在截图、日志、Issue 或公开文档中。

## 常见问题

| 现象 | 常见原因 |
| --- | --- |
| 连接失败 | URL 填错、网络不可达、AI 网关未发布、Cloudflare 或 DNS 未生效 |
| 401 或认证失败 | Token 错误、Token 未启用、请求头名称写错 |
| 工具列表为空 | 客户端未刷新、服务端工具清单解析失败、AI 网关未同步工具 |
| 能看到工具但调用失败 | 缺少 `strategy_id`，或客户端生成的 `report_type` 不在允许范围 |
| 返回很慢 | 网络延迟、网关链路拥塞、客户端超时时间太短 |
