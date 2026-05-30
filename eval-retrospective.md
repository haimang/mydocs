# Nano-Agent Eval 模板 · retrospective

> **模板类型**：`eval / retrospective`
> **一句话用途**：把一次**决策失误 / 走错的弯路**固化成可检索的"学习化石"——时间线 + 根因 + 教训 + 现在的正确形态。
> **何时用**：发现某个 charter/design/action-plan 方向走错并已纠偏后（如 seam-misstep、action-plan-rewrite-required、对 owner 指令的内省式复盘）。
> **何时不用**：① 回看**代码现状/债务** → 用 `eval-state-analysis.md`；② 评审某份**制品** → 用 `code-review.md`；③ 给阶段收口 → 用 `closure.md`。
>
> **使用纪律（共有脊 · 所有 eval 模板一致）**：
> 1. 本文是 **eval**，分析**一次决策失误**而非代码现状或制品质量；**冻结零决策**。
> 2. 目标是 **recall**：让下次同类失误能被检索到并避免；根因要追到"机制/认知"层，不止于"这次手滑"。
> 3. 头部 / 性质声明 / TL;DR / 输入锚定 / 修订历史为**共有脊**，跨 eval 模板一致。

---

# `{RETROSPECTIVE_TITLE}`

> **对象**：`{WHAT_WENT_WRONG_AND_GOT_CORRECTED}`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`eval / retrospective`（决策失误复盘；冻结零决策）
> **文档状态**：`draft | reviewed | superseded`
> **上游权威输入**：
> - `{THE_WRONG_DOC_OR_DECISION}`
> - `{THE_CORRECTION_DOC}`
> **下游消费者**：`{NEXT_CYCLE_FRAMING_OR_OWNER}`

---

## 0. 一句话

> 一句话说清：错在哪、现在对的形态是什么。

- **一句话**：`{ONE_LINER}`

---

## 1. 时间线

> 从"做了什么 → 何时发现不对 → 谁纠偏 → 纠成什么"的事件流。

| 时间 / 节点 | 发生了什么 | 角色 |
|-------------|------------|------|
| `{T1}` | `{EVENT}` | `{ACTOR}` |
| `{T2}` | `{EVENT}` | `{ACTOR}` |

---

## 2. 根因表

> 追到机制/认知层，不止于"这次的具体表现"。

| 编号 | 根因 | 类型 | 为什么会发生 |
|------|------|------|--------------|
| `R1` | `{ROOT_CAUSE}` | `认知混淆 / 边界错置 / 信息缺失 / 流程缺口` | `{WHY}` |
| `R2` | `{ROOT_CAUSE}` | `{TYPE}` | `{WHY}` |

---

## 3. 教训

> 可迁移的教训。写成"下次遇到 X，应该 Y"。

1. `{LESSON_1}`
2. `{LESSON_2}`

---

## 4. 现在的正确形态

> 纠偏后到底应该长什么样；与错误形态的对比。

- **正确形态**：`{CORRECT_FORM}`
- **与错误形态的关键差异**：`{KEY_DIFF}`

---

## 5. [长版 · 可选] 接受批评 / 失败模式定位 / 重设计

> 当复盘较重（如对 owner 指令的内省、需要重写 action-plan）时启用。

### 5.1 接受批评
- `{ACKNOWLEDGED_CRITIQUE}`

### 5.2 失败模式定位
| 失败模式 | 表现 | 触发条件 |
|----------|------|----------|
| `{FAILURE_MODE}` | `{SYMPTOM}` | `{TRIGGER}` |

### 5.3 重设计
- `{REDESIGN_SUMMARY}`
- **对比矩阵（旧→新）**：

| 维度 | 旧 | 新 |
|------|----|----|
| `{DIM}` | `{OLD}` | `{NEW}` |

---

## 附录

### A. 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿 |
