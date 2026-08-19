## 9. 执行日志回填（仅宿主已进入可执行态时使用）

> **用法（respond- 附加章节，append-only）**：
> 1. **宿主**（二选一，不得独立成篇）：
>    - `action-plan`：本节是 `action-plan.md` 执行回填的**厚版**（薄占位在 AP §11；历史文档或称 §9）。
>    - `eval-attribution-and-fix-cycle`：挂该模板 **§14**（事故包授权后的执行账）。
> 2. **挂载位置**：
>    - AP：append 到计划主体之后，作 `## 9` / `## 11`（以宿主现行编号为准）。**不改写计划主体**。
>    - 事故闭环：append 为 `## 14`。**不改写 §0–§11 归因与设计原貌**。
> 3. **谁写 / 何时**：由**执行者本人**在宿主进入可执行态后回填——AP 为 `executed`；事故闭环为 `AUTHORIZED_FOR_LOCAL` 起。未到该态则本节省略/删除。
> 4. **回链 item-ID**：每一行必须对应计划/包台账 ID（`P1-01 / X3-01 / Y10-P0-01`），不许模糊写"做了一些"。
> 5. **诚实纪律**：计划 vs 实际**偏差必须逐条**；测试 `degraded` 必带机器 `reason`；**pre-existing 失败须带 git 证据甩锅**，不写 success-shaped fallback；residual 交后继 charter / 后继包，**不回填本阶段**。事故闭环另：local PASS 不得自动授权下一 lane。
> 6. **多轮**：多步/多轮用时序表或 `Round 1/2/3` / `§14.B`；版本 bump 落在产物 baseline，不在标题后缀。

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
