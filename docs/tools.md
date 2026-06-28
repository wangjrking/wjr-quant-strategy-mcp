# 工具入参和输出说明

本文说明 WJR量化策略MCP 当前公开工具的用途、入参和建议理解方式。

## get_strategy_overview

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

典型输出内容：

```json
{
  "strategies": [
    {
      "strategy_id": "example_strategy",
      "name": "示例策略",
      "summary": "策略简介",
      "status": "published",
      "risk_note": "风险提示"
    }
  ]
}
```

客户理解重点：

- 先用这个工具确认有哪些可用策略。
- 不要把策略介绍理解为买卖建议。
- 重点看策略适用边界、风险说明和状态。

## get_latest_signal

查看某个策略已经发布的最新信号。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

典型输出内容：

```json
{
  "strategy_id": "example_strategy",
  "as_of": "2026-06-28",
  "signals": [
    {
      "trade_date": "2026-06-28",
      "symbol": "000001.SZ",
      "signal": "watch",
      "score": 0.72,
      "note": "示例说明"
    }
  ]
}
```

客户理解重点：

- `limit` 建议先用 10 到 20。
- 信号是已经发布的策略资产，不代表实时交易指令。
- 需要结合风险、仓位、流动性和交易成本独立判断。

## get_strategy_history_and_performance

查看某个策略的历史信号和历史效果材料。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

典型输出内容：

```json
{
  "strategy_id": "example_strategy",
  "history": [
    {
      "trade_date": "2026-06-20",
      "symbol": "000001.SZ",
      "signal": "watch",
      "result_note": "示例历史结果"
    }
  ],
  "performance": {
    "period": "示例区间",
    "summary": "历史效果摘要",
    "risk_note": "历史效果不代表未来收益"
  }
}
```

客户理解重点：

- 历史效果只能说明过去表现。
- 更应该关注最大回撤、信号频率、失效场景和数据口径。
- 不要只看收益摘要。
