# ModelScope MCP Square Publication Guide

Use this repository as the lightweight public landing page for WJR Quant Strategy MCP.

## Form Values

```text
GitHub address:
https://github.com/wangjrking/wjr-quant-strategy-mcp

English name:
wjr-quant-strategy-mcp

Chinese name:
WJR量化策略MCP

Owner:
wjr0808

Visibility:
Public

Hosting type:
Local only

Tags:
finance, quant, stock, strategy, investment-assistant, MCP
```

## Description

```text
WJR量化策略MCP提供已发布量化策略资产的只读查询能力，包括策略介绍、最新信号、历史信号和策略历史效果。服务不生成新预测，不自动荐股，不构成买入、卖出或持仓建议。历史表现不代表未来收益。
```

## Public Endpoint

```text
http://mcp.wjr.world/mcp-servers/wjr-quant-sse/sse
```

## Authentication

Use an AI gateway consumer token:

```text
Authorization: Bearer <your AI gateway consumer token>
```

Do not publish real tokens in this repository.
