# Nano-Agent Charter-Lite 模板

> **适用范围**：`小阶段 phase charter | 快速代码迭代阶段 | 敏捷收尾/清理阶段`
> **不适用范围**：`foundation charter | boundary charter | 大型多月阶段 | auto-generated registry | code review | closure memo`
>   —— 上述场景仍用完整版 `docs/templates/charter.md`。
>
> **charter-lite 与完整 charter 的差异（设计意图）**：
> 1. **不产出 design 文档**：charter-lite 阶段 `eval → charter-lite → action-plan` 三段式,**跳过 design**。
> 2. **design 本该消除的模糊空间，由 owner QNA 在 eval 阶段提前冻结**：charter-lite 用一份**强制冻结的 QNA** 补偿 design 缺失带来的模糊空间。
> 3. **不要求引用 mini-agent / codex / claude-code 等参照产品代码**：charter-lite 以本仓库现实代码为唯一真相,不强制做三家参照产品的实现对照。
>
> **使用纪律**：
> 1. charter-lite 仍是**纲领文件**,不是 action-plan、不是 closure。它冻结：为什么做、做什么/不做什么、Phase 边界、收口条件。
> 2. **硬闸**：charter-lite 定稿前,§1.2 的 QNA 必须全部 `frozen`。**存在任何 `open` 的架构/owner 级问题 ⇒ charter-lite 不得定稿,不得进入 action-plan。** 不允许把模糊问题悄悄留给 action-plan(design 已被跳过,action-plan 不是模糊消除场所)。
> 3. 若某模糊问题大到 QNA 一两句话答不了 —— 那它就**不该用 charter-lite**,应回退到完整 charter + design 流程。

---

# `{CHARTER_TITLE}`（charter-lite）

> **文档对象**：`{PHASE_OBJECT}`
> **状态**：`draft | active | reviewed | closed | superseded`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`
> **文档性质**：`charter-lite（小阶段纲领）`
> **一句话定义**：`{ONE_LINE_DEFINITION}`
>
> **修订历史**：
> - `{REVISION_1}`
>
> **直接输入包（authoritative）**：
> 1. `{UPSTREAM_EVAL_DOC}` —— eval 阶段分析(必填)
> 2. `{FROZEN_QNA_DOC_OR_SECTION}` —— 冻结 QNA(必填;见 §1.2)
> 3. `{OTHER_UPSTREAM_OR_NA}`
>
> **下游预期产物**：
> - action-plan：`{ACTION_PLANS_TO_PRODUCE}`
> - closure / handoff：`{CLOSURE_OR_HANDOFF_DOC}`
> - **不产出 design 文档**（charter-lite 设计意图）。

---

## 0. 为什么现在做 + 本文件不替代什么

> 三到六句话即可。charter-lite 不要写长篇背景。

### 0.1 为什么是现在

`{WHY_NOW}`

### 0.2 为什么用 charter-lite 而不是完整 charter

> 必须显式回答：本阶段的模糊空间是否小到能被 QNA 一次性冻结?
> 若答案为否 —— 停止使用本模板,回退完整 charter + design。

`{WHY_LITE_IS_ENOUGH}`

### 0.3 职责边界

- **本 charter-lite 负责冻结**：阶段目标、In/Out-of-Scope、Phase 边界、收口条件、QNA 答案。
- **不在本文件展开**：逐任务执行(→ action-plan)、执行日志(→ action-plan §9 / closure)。
- **本阶段不产出 design 文档**；不要求参照 mini-agent / codex / claude-code 代码。

---

## 1. Owner Decisions 与冻结 QNA（charter-lite 的核心）

> 这是 charter-lite 最重要的一节 —— 它替代了 design。
> design 本会做的"消除架构/接口/边界模糊",在这里以 QNA 的形式一次性冻结。

### 1.1 Owner Decisions（直接生效）

| 编号 | 决策 | 影响范围 | 来源 |
|------|------|----------|------|
| D1 | `{DECISION}` | `{AFFECTED_SCOPE}` | `{SOURCE}` |
| D2 | `{DECISION}` | `{AFFECTED_SCOPE}` | `{SOURCE}` |

### 1.2 冻结 QNA（强制 —— 硬闸）

> **规则**：
> - 本表必须收录**全部**会影响实现方向的架构 / 接口 / 边界 / 取舍问题。
> - 每一条的 `状态` 必须是 `frozen`。**存在任何 `open` ⇒ charter-lite 不得定稿。**
> - 答案必须是**可执行的二元/具体结论**,不允许"视情况而定""后续再说"。
> - QNA 应在 **eval 阶段**由 owner 完成冻结;charter-lite 只是把冻结结果搬进来。

| QID | 问题 | 冻结答案 | 状态 | 冻结来源 / 时间 |
|-----|------|----------|------|-----------------|
| Q1 | `{ARCHITECT_LEVEL_QUESTION}` | `{FROZEN_ANSWER}` | `frozen` | `{OWNER · DATE}` |
| Q2 | `{INTERFACE_OR_CONTRACT_QUESTION}` | `{FROZEN_ANSWER}` | `frozen` | `{OWNER · DATE}` |
| Q3 | `{BOUNDARY_OR_TRADEOFF_QUESTION}` | `{FROZEN_ANSWER}` | `frozen` | `{OWNER · DATE}` |

### 1.3 QNA 完整性自检（必填）

> 回答："还有没有任何会影响实现的模糊问题，没进上表?"

- **本阶段已知的全部架构/接口/边界模糊点**：`{LIST_OR_NONE}`
- 上述是否都已进 §1.2 并 `frozen`：`yes`（若 `no` —— charter-lite 不得定稿)
- **声明**：`本阶段不存在留给 action-plan 自行决断的架构级模糊问题。`

### 1.4 明确不再重讨论的前提

1. `{FROZEN_PRECONDITION_1}`
2. `{FROZEN_PRECONDITION_2}`

---

## 2. 现实起点（Reality Snapshot · 精简版）

> 防止把"理想态"误当"仓库现实"。charter-lite 用紧凑表,不展开。

### 2.1 已成立的 shipped / frozen 真相

| 主题 | 当前现实 | 证据 |
|------|----------|------|
| `{AREA}` | `{REALITY}` | `{EVIDENCE}` |
| `{AREA}` | `{REALITY}` | `{EVIDENCE}` |

### 2.2 本阶段要处理的 gap

| 编号 | gap | 为什么本阶段处理 | 若不处理 |
|------|-----|------------------|----------|
| G1 | `{GAP}` | `{WHY_IN_SCOPE}` | `{RISK}` |
| G2 | `{GAP}` | `{WHY_IN_SCOPE}` | `{RISK}` |

### 2.3 上阶段 defer / KI 碰撞结果（必填）

> 经验纪律：closure 里的 known-issue / defer 会腐烂。开工前必须对上阶段 closure 的 KI/defer 做一次代码碰撞,标 `已完成(stale-done)` / `仍 open` / `继续 defer`。

| 上阶段 defer/KI | 碰撞结果 | 本阶段处置 |
|------------------|----------|------------|
| `{ITEM}` | `stale-done / 仍 open / 继续 defer` | `{IN_SCOPE / OOS}` |

### 2.4 本阶段必须拒绝的错误前提

- `{FALSE_ASSUMPTION}` —— 为什么错：`{WHY_FALSE}`

---

## 3. 阶段目标与边界

### 3.1 一句话目标

> **阶段目标**：`{ONE_SENTENCE_GOAL}`

- **一句话产出**：`{ONE_SENTENCE_OUTPUT}`
- **一句话非目标**：`{ONE_SENTENCE_NON_GOAL}`

### 3.2 In-Scope（本阶段必须完成）

| 编号 | 工作主题 | 为什么必须本阶段做 | 对应 Phase |
|------|----------|--------------------|------------|
| I1 | `{IN_SCOPE_THEME}` | `{WHY}` | `{PHASE}` |
| I2 | `{IN_SCOPE_THEME}` | `{WHY}` | `{PHASE}` |

### 3.3 Out-of-Scope（本阶段明确不做）

| 编号 | 项目 | 为什么不做 | 重评条件 / 下游落点 |
|------|------|------------|----------------------|
| O1 | `{OUT_OF_SCOPE_ITEM}` | `{WHY_DEFERRED}` | `{REVISIT_OR_NEXT_DOC}` |
| O2 | `{OUT_OF_SCOPE_ITEM}` | `{WHY_DEFERRED}` | `{REVISIT_OR_NEXT_DOC}` |

### 3.4 灰区判定（消除模糊）

| 项目 | 判定 | 理由 | 翻案需要什么新事实 |
|------|------|------|---------------------|
| `{GREY_ITEM}` | `in-scope / out-of-scope / defer` | `{WHY}` | `{REOPEN_CONDITION}` |

### 3.5 硬纪律

> 写死本阶段不可违反的工程纪律(如：零契约变更、stop-the-bleed 单调下降、layering gate、零破坏等)。

1. `{HARD_DISCIPLINE_1}`
2. `{HARD_DISCIPLINE_2}`

---

## 4. Phase 总览（精简）

> charter-lite 阶段小,Phase 少(建议 ≤4)。Phase 类型只有 `freeze | implementation | migration | closure` —— **无 `design`**。

### 4.1 Phase 总表

| Phase | 名称 | 类型 | 核心目标 | 进入条件 | 主要风险 |
|------|------|------|----------|----------|----------|
| `{P0}` | `{PHASE_NAME}` | `{freeze \| implementation \| migration \| closure}` | `{GOAL}` | `{ENTRY}` | `{RISK}` |
| `{P1}` | `{PHASE_NAME}` | `{TYPE}` | `{GOAL}` | `{ENTRY}` | `{RISK}` |
| `{PN}` | `{PHASE_NAME}` | `{TYPE}` | `{GOAL}` | `{ENTRY}` | `{RISK}` |

### 4.2 各 Phase 精简说明

> 每个 Phase 填 5 个字段即可(比完整 charter 少一个"风险"块 —— 风险已进 §4.1 表)。

#### `{P0} — {PHASE_NAME}`

- **目标**：`{PHASE_GOAL}`
- **In-Scope**：`{PHASE_IN_SCOPE}`
- **交付物**：`{DELIVERABLES}`
- **收口标准**：`{EXIT_CRITERIA}`
- **什么不算完成**：`{NOT_DONE_CASES}`

#### `{P1} — {PHASE_NAME}`

- **目标**：`{PHASE_GOAL}`
- **In-Scope**：`{PHASE_IN_SCOPE}`
- **交付物**：`{DELIVERABLES}`
- **收口标准**：`{EXIT_CRITERIA}`
- **什么不算完成**：`{NOT_DONE_CASES}`

*（按需继续扩展;Phase 多于 4 个 ⇒ 考虑回退完整 charter）*

---

## 5. 执行顺序与 Gate

### 5.1 推荐执行顺序 / DAG

```text
{P0}
├── {P1}
└── {P2}
```

### 5.2 Gate 规则

| Gate | 含义 | 必须满足的条件 |
|------|------|----------------|
| **QNA Gate**（charter-lite 特有，硬闸） | 进入 action-plan 的前提 | §1.2 QNA 全部 `frozen`;§1.3 完整性自检通过 |
| Start Gate | 阶段可开工 | `{CONDITION}`（含 §2.3 defer 碰撞已完成） |
| Closure Gate | 阶段可收口 | `{CONDITION}`（见 §6） |

### 5.3 为什么这样排

`{WHY_THIS_ORDER}`

---

## 6. 验证与收口

### 6.1 验证策略

> charter-lite 不列到测试文件级。冻结：需要哪几层证据 + 本阶段不变量。

- **继承的验证层**：`{INHERITED_LAYERS}`
- **本阶段新增验证重点**：`{NEW_VALIDATION_FOCUS}`
- **本阶段不变量**：`{INVARIANTS}`
- **证据不足时不允许宣称**：`{OVERCLAIM_GUARD}`

### 6.2 收口类型判定

| 收口类型 | 使用条件 | 文档要求 |
|----------|----------|----------|
| `full close` | 阶段目标 + 硬闸全满足,无残留 | closure 记录证据 |
| `close-with-known-issues` | 主线完成,残留问题已明确降级且不破坏阶段目标 | closure **必须**复写残留问题 + 影响范围 + 下游落点 |
| `cannot close` | 仍有 blocker / truth drift / 证据不足 | 记录 blocker,保持阶段 open |

### 6.3 Primary Exit Criteria（硬闸）

1. `{PRIMARY_EXIT_1}`
2. `{PRIMARY_EXIT_2}`
3. `{PRIMARY_EXIT_3}`

### 6.4 NOT-成功退出识别

以下任一成立 ⇒ **不得**宣称收口：

1. `{NOT_SUCCESS_CASE_1}`
2. `{NOT_SUCCESS_CASE_2}`
3. 存在曾标 `frozen` 的 QNA 在执行中被发现答案错误且未重新冻结。

---

## 7. 下一阶段触发 + 后续文档

### 7.1 下一阶段触发条件

1. `{NEXT_PHASE_PRECONDITION}`

### 7.2 后续文档生产清单

- **action-plan**：`{ACTION_PLAN_LIST}`
- **closure / handoff**：`{CLOSURE_DOC}`
- **不产出 design 文档**。
- 建议撰写顺序：`{WRITE_ORDER}`

---

## 8. 维护约定

1. charter-lite 只更新冻结边界、Phase 定义、收口条件、QNA 答案;不回填逐任务执行日志。
2. **若执行中发现某 `frozen` QNA 答案错误**：必须停下,由 owner 重新冻结该 QID,并在文首修订历史记录;不允许 action-plan 自行改写 QNA 答案。
3. 若某项 in-scope ↔ out-of-scope 互转,同步更新 §3、§4、§6。
4. 若采用 `close-with-known-issues`,closure 必须复写残留问题、影响范围、下游落点。
5. **若阶段中途发现模糊空间超出 QNA 可承载范围**：说明本阶段不该用 charter-lite —— 应在修订历史记录,并评估升级到完整 charter + design 流程。
