# WJR 量化策略 MCP

WJR 量化策略 MCP 是一个面向普通用户的公网 MCP 服务，用来查看已经发布的量化策略资产。

你可以用它查看：

- 当前有哪些可用策略
- 某个策略是做什么的
- 某个策略最新发布了什么信号
- 某个策略的历史信号、历史效果和主要风险

它适用于 TRAE、Cursor、Cherry Studio、Qwen Code，以及其他支持远程 SSE MCP Server 的客户端。

## 快速接入

服务地址：

```text
http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse
```

认证方式：

```text
Authorization: Bearer <你的 AI 网关消费者 Token>
```

TRAE / Cursor 配置：

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

不要把真实 Token 提交到 GitHub、截图、日志或公开 Issue 中。如果 Token 泄露，请立即在 AI 网关中禁用或重置。

## 可用工具

| 工具名 | 用途 |
| --- | --- |
| `get_strategy_overview` | 查看可用策略清单，或查看指定策略的介绍、规则说明和适用边界 |
| `get_strategy_report` | 查看指定策略的报告，可选择最新信号、历史信号、策略效果、风险说明或完整报告 |

## 推荐提问

```text
查看有哪些可用策略。
```

```text
查看某个策略的完整报告，并用普通人能懂的话解释。
```

```text
查看某个策略的最新信号，并说明这些字段是什么意思。
```

```text
查看某个策略的历史信号和历史效果，并说明主要风险。
```

## 详细文档

- [TRAE 配置示例](examples/trae.json)
- [Cursor 配置示例](examples/cursor.json)
- [工具入参和输出说明](docs/tools.md)
- [工具测试指南](docs/tool-testing.md)
- [魔塔社区服务配置](docs/modelscope-community-service.md)
- [故障排查](docs/troubleshooting.md)
- [安全说明](docs/security.md)

## 边界声明

本服务只展示已经发布的策略资产，不直接参与生产计算或交易。

它不会：

- 生成新的预测
- 生成新的交易信号
- 自动荐股
- 构成买入、卖出或持仓建议
- 下单或连接交易账户
- 运行回测
- 训练模型
- 暴露内部因子、模型分数、账户数据或私有策略参数

历史效果不代表未来收益。所有输出仅用于策略资产查看、研究辅助和信息展示，不构成投资建议。
