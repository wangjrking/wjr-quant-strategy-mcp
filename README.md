# WJR量化策略MCP

WJR量化策略MCP是一个面向 MCP 客户端的公网策略资产服务，提供已发布量化策略资产的只读查询能力。

适用客户端包括 TRAE、Cursor、Cherry Studio、Qwen Code，以及其他支持远程 SSE MCP Server 的工具。

## 服务地址

```text
http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse
```

## 认证方式

本服务通过上游 AI 网关进行消费者认证。

```text
Authorization: Bearer <你的AI网关消费者Token>
```

请勿把真实 Token 提交到 GitHub、截图、日志或公开 Issue 中。如果 Token 泄露，应立即在 AI 网关中禁用或重置。

## 能力范围

当前公开 3 个 MCP 工具：

| 工具名 | 中文说明 |
| --- | --- |
| `get_strategy_overview` | 查看可用策略清单，或查看指定策略的介绍、规则说明和适用边界 |
| `get_latest_signal` | 查看某个策略已经发布的最新信号 |
| `get_strategy_history_and_performance` | 查看某个策略的历史信号和历史效果材料 |

## 边界声明

本 MCP 服务只展示已发布策略资产，不直接参与生产计算或交易。

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

## TRAE 配置

在 TRAE 的 MCP 配置中加入下面内容，并把 Token 占位符替换为你的 AI 网关消费者 Token：

```json
{
  "mcpServers": {
    "wjr-quant-sse": {
      "type": "sse",
      "url": "http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse",
      "headers": {
        "Authorization": "Bearer <你的AI网关消费者Token>"
      }
    }
  }
}
```

## Cursor 配置

```json
{
  "mcpServers": {
    "wjr-quant-sse": {
      "type": "sse",
      "url": "http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse",
      "headers": {
        "Authorization": "Bearer <你的AI网关消费者Token>"
      }
    }
  }
}
```

## 工具入参

### get_strategy_overview

查看策略概览。

不传 `strategy_id` 时，返回可用策略清单。

```json
{}
```

传入 `strategy_id` 时，返回指定策略介绍。

```json
{
  "strategy_id": "策略ID"
}
```

### get_latest_signal

查看某个策略的最新发布信号。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

### get_strategy_history_and_performance

查看某个策略的历史信号和历史效果材料。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

## 推荐提问

```text
查看有哪些可用策略。
```

```text
查看某个策略的最新信号，并解释这些字段应该怎么理解。
```

```text
查看某个策略的历史信号和历史效果，说明主要风险。
```

## 魔塔 MCP 广场发布信息

在魔塔 MCP Server 创建页面可使用以下信息：

```text
GitHub地址：
https://github.com/wangjrking/wjr-quant-strategy-mcp

英文名称：
wjr-quant-strategy-mcp

中文名称：
WJR量化策略MCP

所有者：
wjr0808

是否公开：
公开

托管类型：
仅本地可用

自定义标签：
金融、量化、股票、策略、投资辅助、MCP
```

## 风险提示

本项目是策略资产信息服务，不是投资顾问服务。用户应结合自身风险承受能力、流动性、交易成本、仓位管理和相关监管要求独立判断。
