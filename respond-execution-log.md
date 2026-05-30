## 9. 执行日志回填（仅 `executed` 状态使用）

> **用法（respond- 附加章节，append-only）**：
> 1. **宿主**：`action-plan`。本节是 `action-plan.md` §9 的**厚版**；薄占位仍保留在 `action-plan.md §9`，需要详细回填时改用本模板。
> 2. **挂载位置**：append 到 action-plan 主体 §8 之后，作 `## 9`。**不改写 §0–§8 计划主体**，只回填实际发生了什么。
> 3. **谁写 / 何时**：由**执行者本人**在 plan 进入 `executed` 后回填（通常同会话）；文档状态不是 `executed` 时本节可省略。
> 4. **回链 item-ID**：每一行必须对应计划台账 ID（`P1-01 / X3-01 / F1-06`），不许模糊写"做了一些"。
> 5. **诚实纪律**：计划 vs 实际**偏差必须逐条**；测试 `degraded` 必带机器 `reason`；**pre-existing 失败须带 git 证据甩锅**，不写 success-shaped fallback；residual 交后继 charter，**不回填本阶段**。
> 6. **多轮**：多步/多轮用 §9.3 时序表或 `Round 1/2/3`；版本 bump 落在产物 baseline，不在标题后缀。

> 执行者：`{EXECUTOR}`
> 执行时间：`{DATE}`
> 文档状态：`draft → executing → executed`
> 代码改动统计：`{N 文件修改 / M 新建 / schema bump 数}`

- **实际执行摘要**：`{逐 phase / cluster 落地 vs 台账 ID}`
- **Phase 偏差（计划 vs 实际）**：`{编号列表，每条带 (计划偏差 | substrate-fit | 顺序调整 | …) 分类 + 理由}`
- **阻塞与处理**：`{编号列表}`
- **测试发现**：`{含 re-pin 结果 / negative 基线 / 全绿计数}`
- **后续 handoff**：`{下游解锁条件 + successor charter}`

### 9.1 逐工作项状态

| 工作项 | 状态 | PR | 实际落点（file:line） | 备注 |
|--------|------|----|------------------------|------|
| `{P1-01}` | `✅ done` | `{PR}` | `{FILE_LINE}` | `{NOTE}` |
| `{P1-02}` | `⚠️ env-blocked No-Go` | `{PR}` | `{FILE_LINE}` | `{NOTE}` |
| `{P2-01}` | `❌ OOS handoff` | `-` | `-` | `{SUCCESSOR}` |

> 状态枚举：`✅ done | ⚠️ env-blocked No-Go | ❌ OOS handoff | 🟩 partial`。

### 9.2 关键指标演进（可选，有 before/after 时）

| 指标 | `{prev land}` | `{this land}` | Δ |
|------|---------------|---------------|---|
| `{METRIC}` | `{V0}` | `{V1}` | `{DELTA}` |

### 9.3 时序执行日志（可选，多步 / 多轮时）

| 时点 | 步骤 | 决策 / 产出 |
|------|------|-------------|
| `T0` | `{STEP}` | `{DECISION_OR_OUTPUT}` |
| `T1` | `{STEP}` | `{DECISION_OR_OUTPUT}` |

### 9.4 关键决策日志（可选）

#### Decision-1 — `{TITLE}`
- **背景**：`{CONTEXT}`
- **决议**：`{DECISION}`
- **理由**：`{WHY}`
- **代价**：`{COST}`

### 9.5 pre-existing 失败甩锅（可选）

> 仅当某验证失败**早于本轮**时使用；必须给证据（git mtime + clean git status）证明非本轮引入，否则按本轮 blocker 处理。

| 失败项 | 证据（git / 命令） | 判断 |
|--------|---------------------|------|
| `{FAILURE}` | `{GIT_OR_CMD_EVIDENCE}` | `pre-existing, non-blocking` |

### 9.6 文档状态

`draft → executing → executed（{DATE}）`。
residual / follow-up → `{successor charter}`（**不回填本阶段**）。
