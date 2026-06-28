# 工具入参和输出说明

WJR 量化策略 MCP 对外提供 6 个普通用户能理解的工具。设计原则是：先找策略，再按需要查看最新信号、历史信号、效果、风险或完整报告。

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

适合这样问：

```text
有哪些可用策略？
```

```text
帮我介绍一下这个策略，它适合什么场景？
```

## get_latest_signal

查看指定策略的最新信号。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

适合这样问：

```text
查看这个策略的最新信号，并解释 target_pct、rank 这些字段。
```

## get_historical_signals

查看指定策略的历史信号。

```json
{
  "strategy_id": "策略ID",
  "limit": 20
}
```

适合这样问：

```text
查看这个策略过去发过哪些信号。
```

```text
总结这个策略历史信号是否稳定。
```

## get_strategy_performance

查看指定策略的历史效果和核心指标。

```json
{
  "strategy_id": "策略ID"
}
```

适合这样问：

```text
查看这个策略的历史效果，解释最大回撤、年化指标和夏普比率。
```

## get_strategy_risk

查看指定策略的主要风险说明。

```json
{
  "strategy_id": "策略ID"
}
```

适合这样问：

```text
这个策略主要有哪些风险？用小白能懂的话解释。
```

## get_strategy_report

查看指定策略的完整报告。它会综合策略介绍、最新信号、历史信号、策略效果和风险说明。

```json
{
  "strategy_id": "策略ID",
  "report_type": "full",
  "limit": 20
}
```

`report_type` 仍支持以下值，方便兼容不同客户端自动生成的参数：

| report_type | 含义 |
| --- | --- |
| `latest_signal` | 最新信号 |
| `history` | 历史信号 |
| `performance` | 策略效果 |
| `risk` | 风险说明 |
| `full` | 完整报告 |

普通用户一般不需要手动填写 `report_type`，直接问“查看完整报告”即可。

## 输出理解

工具返回内容会尽量包含：

- 中文摘要
- 字段解释
- 风险提示
- 图表结构
- 下一步可以追问的问题

所有输出只展示已经发布的策略资产，不生成新预测、不生成新信号、不自动荐股，也不构成投资建议。
