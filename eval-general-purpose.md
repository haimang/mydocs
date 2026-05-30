# Nano-Agent Eval 模板 · general-purpose

> **模板类型**：`eval / general-purpose`
> **一句话用途**：charter 之前，对"这个阶段/功能簇应该装什么、怎么拆相位"做开放式提案；也是不归其它 flavor 的 eval 的**默认兜底骨架**。
> **何时用**：initial-planning / proposed-planning / re-planning / scope-analysis / work-inclusions / 任何"想清楚接下来做什么"的发散思考。
> **何时不用**：① 要冻结边界 → 用 `charter.md`；② 要写可验证验收条件 → 用 `design.md`；③ 要排执行序列 → 用 `action-plan.md`；④ 已经是"对照参考找缺口" → 用 `eval-gap-study.md`。
>
> **使用纪律（共有脊 · 所有 eval 模板一致）**：
> 1. 本文是 **eval**，**冻结零决策**——不是 charter（冻边界）、design（冻决策+写验收）、action-plan（排序+执行）、closure（收口）。
> 2. 凡必须 owner/architect 拍板的问题，**列为 OPEN 决策门**（§6）或回 `qna.md` register 冻结，**不在本文偷偷冻结**。
> 3. 头部 / 性质声明 / TL;DR / 输入锚定 / 修订历史为**共有脊**，跨 eval 模板保持一致。

---

# `{PROPOSAL_TITLE}`

> **对象**：`{PHASE_OR_CLUSTER}`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`eval / general-purpose`（本文是提案，冻结零决策；不是 charter / design / action-plan / closure）
> **文档状态**：`draft | reviewed | superseded`
> **上游权威输入**：
> - `{INPUT_DOC_1}` — `{RELEVANT_PART}`
> - `{INPUT_DOC_2}` — `{RELEVANT_PART}`
> **下游消费者**：`{CHARTER_OR_DESIGN_THIS_FEEDS}`

---

## 0. TL;DR / 论点

> 一段话 + 一句话收尾。说清"本文提议做什么、为什么、留给 owner 决断什么"。

- **核心论点**：`{ONE_PARAGRAPH_THESIS}`
- **一句话**：`{ONE_LINER}`

---

## 1. 上游输入与锚定

> 本提案站在哪些已冻结的 charter / closure / eval 之上；逐条带文件锚点，便于 review 与 handoff 引用。

| 输入 | 类型 | 提供了什么 | 锚点 |
|------|------|------------|------|
| `{INPUT}` | `charter / closure / eval / qna` | `{WHAT_IT_GIVES}` | `{FILE_OR_LINE}` |

- **本提案不重新讨论的既有结论**：
  - `{FROZEN_PREMISE_1}`（来源：`{REF}`）

---

## 2. In-Scope / Out-of-Scope（提案边界）

> 这里是**提案**边界，不是冻结边界。冻结由 charter 完成。

### 2.1 提议纳入

- **[S1]** `{IN_SCOPE_ITEM}` — `{WHY}`
- **[S2]** `{IN_SCOPE_ITEM}` — `{WHY}`

### 2.2 提议排除 / 延后

- **[O1]** `{OUT_ITEM}` — `{WHY_DEFER}`；重评条件：`{REVISIT}`

### 2.3 灰色地带判定

| 项目 | 倾向判定 | 理由 | 后续落点 |
|------|----------|------|----------|
| `{ITEM}` | `proposed-in / proposed-out / defer` | `{WHY}` | `{CHARTER_OR_FUTURE}` |

---

## 3. 提议的相位 / 工作簇

> 给候选单元命名（如 `{P}1 / {P}2 / WB-1`）。命名是为了后续 charter 能稳定引用；**命名不等于冻结**。

| 编号 | 名称 | 一句话职责 | 规模 | 复用-vs-净新 |
|------|------|------------|------|--------------|
| `{P}1` | `{NAME}` | `{RESPONSIBILITY}` | `XS/S/M/L/XL` | `复用 {REF} / 净新` |
| `{P}2` | `{NAME}` | `{RESPONSIBILITY}` | `XS/S/M/L/XL` | `复用 {REF} / 净新` |

---

## 4. 逐簇工作台账

> 每个相位/工作簇展开为工作项。这里写"打算做什么"，不是 action-plan 的执行任务（不写 `[ ] 创建文件 X`）。

### 4.1 `{P}1 — {NAME}`

| 编号 | 工作项 | 来源 / 诱因 | 复用-vs-净新 | 规模 | 风险 |
|------|--------|-------------|--------------|------|------|
| `{P}1-01` | `{ITEM}` | `{SOURCE}` | `复用 {REF} / 净新` | `XS/S/M/L` | `low/med/high` |

### 4.2 `{P}2 — {NAME}`

| 编号 | 工作项 | 来源 / 诱因 | 复用-vs-净新 | 规模 | 风险 |
|------|--------|-------------|--------------|------|------|
| `{P}2-01` | `{ITEM}` | `{SOURCE}` | `复用 {REF} / 净新` | `XS/S/M/L` | `low/med/high` |

---

## 5. 依赖图（DAG）

> 用树/箭头展示候选相位的依赖、关键路径与并行窗。

```text
{P}1 ──▶ {P}2 ──▶ {P}4
          └──▶ {P}3   （{P}2 之后 {P}3/{P}4 可并行）
关键路径：{CRITICAL_PATH}
并行窗：{PARALLEL_WINDOWS}
```

---

## 6. Owner 决策门 / 开放问题

> 本文不冻结，但要把"必须 owner 拍板的点"显式列为 OPEN，交给 charter / `qna.md` 收口。

| 编号 | 决策点 | 影响范围 | 当前倾向 | 状态 | 落点 |
|------|--------|----------|----------|------|------|
| `G-1` | `{DECISION}` | `{IMPACT}` | `{RECOMMENDATION}` | `OPEN` | `{CHARTER_OR_QNA}` |

---

## 7. 风险册

| 风险 | 触发条件 | 影响 | 缓解 / 应对 |
|------|----------|------|-------------|
| `{RISK}` | `{TRIGGER}` | `{IMPACT}` | `{MITIGATION}` |

---

## 8. 建议与下一步

- **推荐序列**：`{RECOMMENDED_SEQUENCE}`
- **可解锁的下游**：`{CHARTER_OR_DESIGN_TO_PRODUCE}`
- **需进入 qna register 的问题**：`{QNA_ITEMS_OR_NONE}`
- **一句话总结**：`{CLOSING_ONE_LINER}`

---

## 附录

### A. （可选）二次意见 / round-trip

> 若本文走了 panel 二次意见或被回填回应，记在此。保留作者/审查者身份。

- **second opinion（`{REVIEWER}`）**：`{NOTE}`

### B. 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿 |
