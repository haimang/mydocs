# Nano-Agent 代码审查质量评价模板

> 评价对象: `{REVIEWER_OR_REVIEW_SET}`
> 评价人: `{EVALUATOR}`
> 评价时间: `{DATE}`

---

## 0. 评价结论

- **一句话评价**：`{ONE_LINE_STYLE_AND_VALUE}`
- **最佳AGENT**：`{BEST_AGENT_OF_THIS_ROUND}`
- **最高价值 Finding**：`{BEST_VALUE_FINDING}`

---

## 1. Findings 质量清点

| AGENT | 问题编号 | 原始严重程度 | 事后判定 | Finding 质量 | 分析与说明 |
|---------|----------|--------------|----------|--------------|------------|
| {agent.name} | `{VF_ID}` | `critical | high | medium | low` | `true-positive | partial | false-positive | stale | missed-by-others` | `excellent | good | mixed | weak` | `{ANALYSIS}` |


---

## 2. 多维度评分 - 单向总分10分

| AGENT | 总分 | 证据链完整度 | 判断严谨性 | 修法建议可执行性 | 协作友好度 | 找到问题的覆盖面 | 严重级别准确度 |
|---------|------|------|------|------|------|------|------|

- 逐 AGENT 评分说明