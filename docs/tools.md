# 工具入参和输出说明

WJR 量化策略 MCP 对外只保留两个工具。这样普通用户不用理解内部资产目录、技术测试、发布索引等开发概念，只需要先选策略，再看报告。

## get_strategy_overview

查看策略概览。

不传 `strategy_id` 时，返回可用策略清单：

```json
{}
```

传入 `strategy_id` 时，返回指定策略介绍：

```json
{
  "strategy_id": "策略ID"
}
```

典型输出内容：

```json
{
  "tool_view": "strategy_overview",
  "strategies": [
    {
      "strategy_id": "example_strategy",
      "name": "示例策略",
      "summary": "策略简介",
      "status": "published",
      "latest_signal_available": true,
      "historical_signal_available": true,
      "performance_available": true
    }
  ],
  "disclaimers": [
    "历史表现不代表未来收益。",
    "实际投资需结合仓位、流动性、交易成本和个人风险承受能力。"
  ]
}
```

适合这样问：

```text
有哪些可用策略？
```

```text
帮我介绍一下这个策略，它适合什么场景？
```

## get_strategy_report

查看某个策略的报告。这个工具覆盖最新信号、历史信号、策略效果、风险说明和完整报告。

入参：

```json
{
  "strategy_id": "策略ID",
  "report_type": "full",
  "limit": 20
}
```

`report_type` 可选值：

| report_type | 含义 |
| --- | --- |
| `latest_signal` | 最新信号 |
| `history` | 历史信号 |
| `performance` | 策略效果 |
| `risk` | 风险说明 |
| `full` | 完整报告 |

`limit` 用来控制信号记录最多返回多少条，默认 20，最大 200。

典型输出内容：

```json
{
  "tool_view": "strategy_report",
  "strategy_id": "example_strategy",
  "report_type": "full",
  "report_title": "完整策略报告",
  "summary": "这是已发布策略资产的只读报告，用于理解策略、信号、历史效果和风险，不构成投资建议。",
  "report": {
    "overview": {},
    "latest_signal": {},
    "history_and_performance": {},
    "risk": {}
  },
  "next_questions": [
    "先解释最新信号。",
    "再解释历史效果和风险。",
    "帮我总结这个策略适合什么用户。"
  ],
  "disclaimer": "本报告不生成新信号，不自动荐股，不构成买入、卖出或持仓建议；历史表现不代表未来收益。"
}
```

适合这样问：

```text
查看这个策略的完整报告。
```

```text
查看这个策略最新信号，并解释 target_pct、rank 这些字段。
```

```text
查看这个策略历史信号和历史效果，重点说风险。
```

```text
只看这个策略的风险说明。
```

## 使用建议

- 第一步先用 `get_strategy_overview` 找到策略。
- 第二步用 `get_strategy_report` 查看报告。
- 不需要直接调用内部资产、健康检查或发布索引工具。
- 输出里如果包含图表字段，MCP 客户端可以把它渲染为柱状图、时间线或指标图；不支持图表的客户端也能直接读取文本和 JSON。
- 所有输出都只是已发布资产展示，不构成投资建议。
