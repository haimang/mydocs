# Nano-Agent Charter-Lite 模板

> **适用范围**：`小阶段 phase charter | 快速代码迭代阶段 | 敏捷收尾/清理阶段`
> **不适用范围**：`foundation charter | boundary charter | 大型多月阶段 | auto-generated registry | code review | closure memo`
>   —— 上述场景仍用完整版 `docs/templates/charter.md`。
>
> **charter-lite 在工作流中承担的责任（精确版 · 勿过度声称）**：
> 1. **它承担 charter 角色**：为什么做、做什么/不做什么、Phase 边界、收口条件、下一阶段触发——这是它的本职。
> 2. **它只替代 design 的「决策冻结」一项**：通过 §1.2 强制冻结的 QNA 冻结 owner 二元决策。它**不替代** design 的**净新契约规格 / 架构边界 / 跨功能一致性**——这三件由 §1.4 的 design-necessity gate 判定，命中即升级（见下）。
> 3. **grounding（架构边界 + 仓内 file:line 锚）不是免费的**：若本阶段是**纯扩展既有 substrate**，grounding 可省；若 grounding 非平凡，应配一份 `eval-reference-anchor` 作上游输入（见输入包 §1.5），**不要把 grounding 漏给 action-plan**（历史教训：MIX5 SSRF 因 charter-lite 丢 grounding，威胁模型漏进了 action-plan）。
>
> **四轨定位（charter-lite 是 Track B；见 `docs/templates/re-design/workflow-tracks.md`；下表 `AP` = action-plan）**：
> | 轨 | 文件组合 | 何时用 |
> |----|----------|--------|
> | A 单遍 | eval-general-purpose → AP | trivial、无契约 |
> | **B charter-lite（本模板）** | **eval(+可选 reference-anchor) → charter-lite → AP** | **小·低模糊·扩展既有 substrate·无净新** |
> | C combo ★ | eval-planning三态 + reference-anchor + qna → AP | sub-phase·≥2 AP·需 grounding |
> | D 重轨 | charter + design-neo + qna → AP | foundation·净新多·争议架构 |
>
> > **取舍提醒**：Track C(combo) = charter-lite + reference-anchor，在需要 grounding 时严格更强。**charter-lite 的纯净适配区 = 既不需要多 AP 规划、grounding 又平凡（扩展既有）的小阶段**；一旦 grounding 非平凡或要派生多份 AP，优先 Track C。
>
> **使用纪律**：
> 1. charter-lite 仍是**纲领文件**，不是 action-plan、不是 closure。它冻结：为什么做、做什么/不做什么、Phase 边界、收口条件、QNA 答案。
> 2. **硬闸一（QNA）**：定稿前 §1.2 的 QNA 必须全部 `frozen`。存在任何 `open` 的架构/owner 级问题 ⇒ 不得定稿、不得进入 action-plan。
> 3. **硬闸二（design-necessity）**：§1.4 的 6 条 design-necessity 测试若命中任一 ⇒ charter-lite **不足**，必须升级到 `{Track C combo + design-sketch}`（单簇净新）或 `{Track D + design-neo}`（foundation/多净新）。不允许把净新契约/架构边界/跨功能一致性悄悄留给 action-plan。
> 4. 若某模糊问题大到 QNA 一两句话答不了、或命中 design-necessity ⇒ 它就**不该用 charter-lite**，应升级。

---

# `{CHARTER_TITLE}`（charter-lite）

> **文档对象**：`{PHASE_OBJECT}`
> **状态**：`draft | active | reviewed | closed | superseded`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`
> **文档性质**：`charter-lite（小阶段纲领 · Track B）`
> **一句话定义**：`{ONE_LINE_DEFINITION}`
>
> **修订历史**：
> - `{REVISION_1}`
>
> **直接输入包（authoritative）**：
> 1. `{UPSTREAM_EVAL_DOC}` —— eval 阶段分析（必填）
> 2. `{FROZEN_QNA_DOC_OR_SECTION}` —— 冻结 QNA（必填；见 §1.2）
> 3. `{REFERENCE_ANCHOR_DOC_OR_NA}` —— reference-anchor（**grounding 非平凡时必填**；纯扩展既有可填 `N/A — grounding 平凡`，并在 §1.5 说明）
> 4. `{OTHER_UPSTREAM_OR_NA}`
>
> **下游预期产物**：
> - action-plan：`{ACTION_PLANS_TO_PRODUCE}`（逐 Phase 完整路径锚定见 §7.2 —— 强制）
> - closure / handoff：`{CLOSURE_OR_HANDOFF_DOC}`
> - **不产出独立 design 文档**；若 §1.4 命中 ⇒ 升级，改由 design-sketch / design-neo 承载净新部分。

---

## 0. 为什么现在做 + 本文件不替代什么

> 三到六句话即可。charter-lite 不要写长篇背景。

### 0.1 为什么是现在

`{WHY_NOW}`

### 0.2 为什么用 charter-lite 而不是 Track C / 完整 charter

> 必须显式回答两问：
> 1. 本阶段的模糊空间是否小到能被 QNA 一次性冻结？（否 ⇒ 回退完整 charter + design-neo）
> 2. 是否**未命中** §1.4 任一 design-necessity 条件，且 grounding 平凡（扩展既有 substrate）？（命中/grounding 非平凡 ⇒ 用 Track C combo 或升重轨）

`{WHY_LITE_IS_ENOUGH}`

### 0.3 职责边界

- **本 charter-lite 负责冻结**：阶段目标、In/Out-of-Scope、Phase 边界、收口条件、QNA 答案（owner 决策）。
- **本 charter-lite 不做**（命中即升级）：净新对外契约的叙述规格、净新架构边界、跨功能系统一致性——这些是 design 的活，由 §1.4 gate 判定后交 design-sketch / design-neo。
- **不在本文件展开**：逐任务执行（→ action-plan）、执行日志（→ action-plan §9 / closure）。

---

## 1. Owner Decisions、冻结 QNA、与 design-necessity 闸（charter-lite 的核心）

> 本节冻结 owner 决策（qna）——这是 charter-lite 对 design 的**部分**替代：它替代 design 的**决策冻结**职责，但**不替代** design 的净新契约规格/架构边界/跨功能一致性（后者由 §1.4 判定）。

### 1.1 Owner Decisions（直接生效）

| 编号 | 决策 | 影响范围 | 来源 |
|------|------|----------|------|
| D1 | `{DECISION}` | `{AFFECTED_SCOPE}` | `{SOURCE}` |
| D2 | `{DECISION}` | `{AFFECTED_SCOPE}` | `{SOURCE}` |

### 1.2 冻结 QNA（硬闸一 —— decision-freezing）

> **规则**：
> - 本表收录**全部**会影响实现方向的架构 / 接口 / 边界 / 取舍**决策类**问题。
> - 每一条 `状态` 必须 `frozen`。存在任何 `open` ⇒ charter-lite 不得定稿。
> - 答案必须是**可执行的二元/具体结论**，不允许"视情况而定"。
> - QNA 应在 **eval 阶段**由 owner 完成冻结；charter-lite 只是把冻结结果搬进来。
> - **注意**：QNA 冻结的是"做哪个（决策）"。"做完长什么样（验收规格）"和"接缝在哪（架构边界）"**不是** QNA 能承载的——那是 §1.4 判定是否需要 design 的范畴。

| QID | 问题 | 冻结答案 | 状态 | 冻结来源 / 时间 |
|-----|------|----------|------|-----------------|
| Q1 | `{ARCHITECT_LEVEL_DECISION}` | `{FROZEN_ANSWER}` | `frozen` | `{OWNER · DATE}` |
| Q2 | `{INTERFACE_OR_CONTRACT_DECISION}` | `{FROZEN_ANSWER}` | `frozen` | `{OWNER · DATE}` |

### 1.3 QNA 完整性自检（必填）

- **本阶段已知的全部架构/接口/边界**决策**模糊点**：`{LIST_OR_NONE}`
- 上述是否都已进 §1.2 并 `frozen`：`yes`（若 `no` ⇒ charter-lite 不得定稿）
- **声明**：`本阶段不存在留给 action-plan 自行决断的架构级决策模糊。`

### 1.4 design-necessity 闸（硬闸二 —— 是否需要 design）★ 新增

> charter-lite 的关键边界。**逐条勾选；任一为 `是` ⇒ charter-lite 不足，按路由升级。**

| # | design-necessity 条件 | 命中？ | 命中则 |
|---|------------------------|--------|--------|
| 1 | 新增**对外 contract surface**（从零定义，非扩展既有） | `否` | 升级 |
| 2 | 新增**架构接缝**（净新 decouple/aggregate；reference-anchor 无既有 ARCH 可锚） | `否` | 升级 |
| 3 | **跨 worker 不变量 / 多功能必须拼成一个整体形态** | `否` | 升级 |
| 4 | 验收是**多字段 / 非显然**的（一两句 QNA 答不清“做完长什么样”） | `否` | 升级 |
| 5 | 涉及**安全信任边界**（威胁模型） | `否` | 升级（强制） |
| 6 | **onboarding 关键**：需新贡献者读懂的叙述式契约 | `否` | 升级 |

**升级路由**：
| 命中情形 | 升级到 |
|----------|--------|
| 仅**一处**净新（其余仍扩展既有） | **Track C combo + 一份 `design-sketch`**（仍可无完整 charter） |
| **多处净新 / foundation / 争议架构 / 命中第 5 条安全** | **Track D：完整 `charter` + `design-neo`** |

- **本阶段勾选结论**：`全部为否 ⇒ charter-lite 足够` / `命中第 N 条 ⇒ 已升级到 {…}，本 charter-lite 作废/降级`。

### 1.5 grounding 充足性自检（必填）★ 新增

> 防止"把架构边界 + 仓内锚漏给 action-plan"（MIX5 教训）。

- **本阶段 grounding 性质**：`纯扩展既有 substrate（grounding 平凡，可无 reference-anchor）` / `grounding 非平凡（须配 reference-anchor）`
- 若非平凡：reference-anchor 文档 = `{REFERENCE_ANCHOR_DOC}`（ARCH/TR + file:line 锚已就位）。
- **声明**：`本阶段不存在留给 action-plan 自行摸索的架构边界 / 代码锚。`

### 1.6 明确不再重讨论的前提

1. `{FROZEN_PRECONDITION_1}`
2. `{FROZEN_PRECONDITION_2}`

---

## 2. 现实起点（Reality Snapshot · 精简版）

> 防止把"理想态"误当"仓库现实"。charter-lite 用紧凑表，不展开。

### 2.1 已成立的 shipped / frozen 真相

| 主题 | 当前现实 | 证据 |
|------|----------|------|
| `{AREA}` | `{REALITY}` | `{EVIDENCE}` |

### 2.2 本阶段要处理的 gap

| 编号 | gap | 为什么本阶段处理 | 若不处理 |
|------|-----|------------------|----------|
| G1 | `{GAP}` | `{WHY_IN_SCOPE}` | `{RISK}` |

### 2.3 上阶段 defer / KI 碰撞结果（必填）

> 经验纪律：closure 里的 known-issue / defer 会腐烂。开工前必须对上阶段 closure 的 KI/defer 做一次代码碰撞，标 `已完成(stale-done)` / `仍 open` / `继续 defer`。

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

### 3.3 Out-of-Scope（本阶段明确不做）

| 编号 | 项目 | 为什么不做 | 重评条件 / 下游落点 |
|------|------|------------|----------------------|
| O1 | `{OUT_OF_SCOPE_ITEM}` | `{WHY_DEFERRED}` | `{REVISIT_OR_NEXT_DOC}` |

### 3.4 灰区判定（消除模糊）

| 项目 | 判定 | 理由 | 翻案需要什么新事实 |
|------|------|------|---------------------|
| `{GREY_ITEM}` | `in-scope / out-of-scope / defer` | `{WHY}` | `{REOPEN_CONDITION}` |

### 3.5 硬纪律

> 写死本阶段不可违反的工程纪律（如：零契约变更、stop-the-bleed 单调下降、layering gate、零破坏等）。

1. `{HARD_DISCIPLINE_1}`
2. `{HARD_DISCIPLINE_2}`

---

## 4. Phase 总览（精简）

> charter-lite 阶段小，Phase 少（建议 ≤4）。Phase 类型只有 `freeze | implementation | migration | closure` —— **无 `design`**（若需要 design，已在 §1.4 升级，不在 charter-lite 内）。

### 4.1 Phase 总表

| Phase | 名称 | 类型 | 核心目标 | 进入条件 | 主要风险 |
|------|------|------|----------|----------|----------|
| `{P0}` | `{PHASE_NAME}` | `{freeze \| implementation \| migration \| closure}` | `{GOAL}` | `{ENTRY}` | `{RISK}` |
| `{P1}` | `{PHASE_NAME}` | `{TYPE}` | `{GOAL}` | `{ENTRY}` | `{RISK}` |

### 4.2 各 Phase 精简说明

> 每个 Phase 填 6 个字段（含 action-plan 锚定）。
> **action-plan 锚定为强制项**：每个 Phase 必须写出其 action-plan 文件的**完整路径 + 文件名**（及对应 closure 路径），文件名统一以**阶段代号为前缀**。

#### `{P0} — {PHASE_NAME}`

- **目标**：`{PHASE_GOAL}`
- **In-Scope**：`{PHASE_IN_SCOPE}`
- **交付物**：`{DELIVERABLES}`
- **收口标准**：`{EXIT_CRITERIA}`
- **什么不算完成**：`{NOT_DONE_CASES}`
- **action-plan 锚**：`{ACTION_PLAN_PATH}` → closure：`{CLOSURE_PATH}`

*（按需继续扩展；Phase 多于 4 个 ⇒ 考虑回退完整 charter。）*

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
| **QNA Gate**（硬闸一） | 进入 action-plan 的前提 | §1.2 QNA 全部 `frozen`；§1.3 完整性自检通过 |
| **design-necessity Gate**（硬闸二）★ | 进入 action-plan 的前提 | §1.4 全部为 `否`（未命中）；§1.5 grounding 自检通过。命中任一 ⇒ 已升级，本 charter-lite 不再驱动 action-plan |
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
| `full close` | 阶段目标 + 硬闸全满足，无残留 | closure 记录证据 |
| `close-with-known-issues` | 主线完成，残留问题已明确降级且不破坏阶段目标 | closure **必须**复写残留问题 + 影响范围 + 下游落点 |
| `cannot close` | 仍有 blocker / truth drift / 证据不足 | 记录 blocker，保持阶段 open |

### 6.3 Primary Exit Criteria（硬闸）

1. `{PRIMARY_EXIT_1}`
2. `{PRIMARY_EXIT_2}`

### 6.4 NOT-成功退出识别

以下任一成立 ⇒ **不得**宣称收口：

1. `{NOT_SUCCESS_CASE_1}`
2. 存在曾标 `frozen` 的 QNA 在执行中被发现答案错误且未重新冻结。
3. 执行中发现命中 §1.4 design-necessity 却未升级、把净新契约/架构边界塞进了 action-plan。

---

## 7. 下一阶段触发 + 后续文档

### 7.1 下一阶段触发条件

1. `{NEXT_PHASE_PRECONDITION}`

### 7.2 后续文档生产清单（强制锚定）

> **规则**：用**完整路径 + 文件名**锚定每个 Phase（含 sub-stage）的 action-plan 与 closure 文件。action-plan / closure 文件名统一以**阶段代号为前缀**。

| Phase / sub-stage | action-plan 文件（完整路径 + 文件名） | closure 文件（完整路径 + 文件名） |
|-------------------|----------------------------------------|-------------------------------------|
| `{P0}` | `{ACTION_PLAN_PATH}` | `{CLOSURE_PATH}` |
| `{P1}` | `{ACTION_PLAN_PATH}` | `{CLOSURE_PATH}` |

- **action-plan 索引 README**：`{ACTION_PLAN_README_PATH}`
- **阶段总 closure / handoff**：`{STAGE_CLOSURE_PATH}`
- **不产出独立 design 文档**（若 §1.4 命中已升级，对应 design-sketch / design-neo 路径：`{DESIGN_DOC_PATH_OR_NA}`）。
- **建议撰写顺序**：`{WRITE_ORDER}`

---

## 8. 维护约定

1. charter-lite 只更新冻结边界、Phase 定义、收口条件、QNA 答案；不回填逐任务执行日志。
2. **若执行中发现某 `frozen` QNA 答案错误**：必须停下，由 owner 重新冻结该 QID，并在文首修订历史记录；不允许 action-plan 自行改写 QNA 答案。
3. 若某项 in-scope ↔ out-of-scope 互转，同步更新 §3、§4、§6。
4. 若采用 `close-with-known-issues`，closure 必须复写残留问题、影响范围、下游落点。
5. **若阶段中途命中 §1.4 design-necessity（如发现净新契约/安全边界）或模糊超出 QNA 承载**：说明本阶段不该用 charter-lite —— 在修订历史记录，并按 §1.4 路由升级到 `{Track C + design-sketch}` 或 `{Track D + design-neo}`，不得把净新/grounding 留给 action-plan。
