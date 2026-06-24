# Assessment 模板簇 · index（阶段评估索引 / 编排器）

> **模板簇**：`assessment`（**独立簇，完全自包含；不属于 eval 家族，无 eval 血缘**——本模板不继承任何 eval 共有脊、不声明 `eval/*` 文档性质、不从 eval 模板抽取模块）。
> **簇内成员**：`assessment-index`（本文，阶段编排器）+ [[assessment-analysis]]（单调查面深度评估）。两者配对使用：**index 编排 N 份 analysis**；analysis 的上游是 index 钉定的某一调查面 + 冻结分母。
>
> **一句话用途**：一个相位（phase）开工时，对"本阶段该调查哪些面、各面多大/多急、谁先谁后、哪些是上游已交付不要重做"做一张**总览导航图**，并以 **measure-first 预核查**冻结全阶段共享的**分母（denominators）**，作为 N 份单面深度评估（`assessment-analysis`）与所有下游制品的统一基线。
> **何时用**：① 一个多面相位的评估开场（≥2 个有界调查面）；② 需要先把"现状到底多大"测准、再分面深挖；③ 需要一张"评估地图 + owner-gate 候选 + 勿重做表"来编排后续工作。
> **何时不用**：① 只有单一调查面、无需编排 → 直接写一份 [[assessment-analysis]]；② 已经在排"怎么做/何序/怎么测"的执行序列 → 那是下游执行计划制品，不在本簇。
>
> **调查纪律（assessment 簇共有脊 · 两模板一致）**：
> 1. **定位**：assessment 是 **measure-first 分析制品**，为下游*规划 / 决策 / 执行*供料；它**不排执行序、不写落地验收、不替 owner 裁决**。
> 2. **measure-first 红线**：一切"现状"以 **HEAD 实测**为准（每条带 `path:line` + 可复现命令）；**先测量、后判断**；测得的关键规模/边界**冻结为分母**，作下游所有制品的统一基线，杜绝"凭叙事/凭记忆估值"。
> 3. **零决策、只 MARK**：凡需 owner/架构师拍板者，**列为 owner-gate 候选并 MARK**（不预设倾向、不在本文偷偷冻结），裁决交下游决策登记（`{PHASE}/pre-charter-qna.md` register）。
> 4. **防假绿 / 对账诚实**：参考/既有叙事与实测对不齐者**点名校正**；不把"参考怎么做"误当成"我方现状/机制"。
> 5. **共有脊**：头部 / 文档性质 / TL;DR / 输入与证据锚定 / 修订历史，在本簇两模板间结构一致。
>
> **状态词汇（本簇自有）**：`active index`（编排中，站②评估进行）→ `frozen index`（调查面与冻结分母锁定，作下游基线）→ `superseded`（被新版取代）。
> **占位符约定**：统一 `{UPPER_SNAKE}`，backtick 包裹。`[核心]` = 必填段；`[可选]` = 视相位删除。
> **流水线位置**：本文 = **站①**（编排 + 冻结分母）→ 站② = N 份 [[assessment-analysis]] → 站③+ = 下游规划/决策/执行制品。

---

# `{PHASE_NAME}` 评估索引

> **项目**：`{PROJECT_NAME}`
> **阶段（别名）**：`{PHASE_NAME}`（`{PHASE_ALIAS}`）
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（fleet / panel：`{AGENTS_OR_NONE}`）
> **文档性质**：`assessment / index`（阶段评估编排器；measure-first，零决策——只 MARK 不裁决）
> **文档状态**：`active index | frozen index | superseded`
> **流水线位置**：站① · 下一步 = 站② 逐面 [[assessment-analysis]]
> **关联 owner 意图 SSOT**：`{OWNER_INTENT_DOC_OR_Q_REFS}`
> **关联上游收口**：`{PREV_PHASE_CLOSURE_REFS}`
> **下游消费者**：`{PHASE}/proposed-planning.md` · `{PHASE}/pre-charter-qna.md` · `{PHASE}/final-execution-plan.md`

---

## 0. TL;DR / Owner 意图与本阶段范围 `[核心]`

> 一段话讲清：owner 想解决什么、为什么现在做、本阶段评估覆盖哪些面、不碰什么。

- **一句话**：`{ONE_LINER_WHAT_THIS_PHASE_ASSESSES}`
- **0.1 Owner 提出的方向 / 为什么现在**：`{OWNER_DIRECTIONS_AND_WHY_NOW}`
- **0.2 范围边界（Non-goals）**：`{WHAT_THIS_PHASE_EXPLICITLY_DOES_NOT_TOUCH}`
- **0.3 评估完成汇总**：`{N 面全 done / 站② 进度 / 待补}`

---

## 1. 评估地图 `[核心]`

> 一张表把全部调查面平铺：让读者一眼看清"有几面、各面多急多健康、详评在哪"。

| ID | 调查面 | 优先级 | 健康 | 预核查（站①） | 站② 详评文档 | 备注 |
|----|--------|--------|------|----------------|---------------|------|
| `01` | `{FACE_NAME}` | `P0/P1/P2` | `🟢/🟡/🔴` | `done/进行/待` | `assessment-analysis-01-{slug}.md` | `{NOTE}` |
| `0N` | `{FACE_NAME}` | `…` | `…` | `…` | `assessment-analysis-0N-{slug}.md` | `{NOTE}` |

### 1.1 Owner 方向 ↔ 调查面 映射
> 把 owner 的每个方向落到具体调查面，证明覆盖无遗漏、无越界。

| Owner 方向 | 命中调查面 | 覆盖说明 |
|------------|------------|----------|
| `{DIRECTION}` | `01 / 03` | `{HOW_COVERED}` |

---

## 2. 站① measure-first 预核查 `[核心]`

> 本节是 index 的灵魂：用真实代码把"现状到底多大"测准，冻结成全阶段统一分母。**先测后判，禁估值。**

### 2.1 证据基线与可复现命令
- **证据来源**：`{CODE_PATHS / GREP / TEST_RUNS}`
- **可复现命令**（任何人可重跑坐实下表每个数字）：
```bash
{COMMANDS_THAT_REPRODUCE_EVERY_DENOMINATOR}
```

### 2.2 ★ 冻结分母（FROZEN denominators · HEAD）
> 这些数字是**下游所有制品的统一基线**；一经冻结，下游不得另估。

| 分母 | HEAD 实测值 | 证据锚（`path:line` / 命令） | 用途 |
|------|-------------|------------------------------|------|
| `{DENOMINATOR}` | `{VALUE}` | `{EVIDENCE}` | `{FEEDS_WHICH_FACE}` |

### 2.3 贯穿主题（跨子系统根因）
> 多个面共有的根因/主题，避免在每份 analysis 里各自重述。

- **`{THEME}`**：`{ROOT_CAUSE_SPANNING_FACES}`

### 2.4 对参考 / 既有叙事的失真校正
> 把"参考实现/上游叙事/记忆"与 HEAD 实测对账，点名失真，防止把"别处怎么做"误当"我方现状"。

| 叙事/参考声称 | HEAD 实测 | 失真类型 | 证据 |
|---------------|-----------|----------|------|
| `{CLAIM}` | `{REALITY}` | `高估/低估/错置/不适用` | `{FILE_LINE}` |

### 2.5 须净新的 gate（gate registry）`[可选]`
> 若本阶段需要净新的测试/治理 gate（无既有可沿用），在此登记，喂下游执行计划。

| gate-ID | 用途 | 为什么净新 |
|---------|------|------------|
| `G-{PHASE}-{NN}` | `{PURPOSE}` | `{WHY_NET_NEW}` |

---

## 3. 逐调查面登记 `[核心]`

> 每个调查面一张卡片：比 §1 地图多一层"范围摘要 + 为什么评估 + 预核查初判"，但**不是深度评估本体**（本体在对应 `assessment-analysis`）。

### 3.{NN} `{FACE_NAME}`
- **优先级 / 健康**：`{P-LEVEL} / {HEALTH}`
- **调查范围**：`{SCOPE_BULLETS}`
- **为什么需要评估**：`{WHY_THIS_FACE}`
- **预核查初判（站①，待站②深挖）**：`{PRE_AUDIT_FINDINGS}`
- **详评文档**：`assessment-analysis-{NN}-{slug}.md`

---

## 4. Owner-gate 候选汇总 `[核心]`

> 把各面 MARK 的 owner-gate 候选收敛到一处，交下游决策登记。**只 MARK，不裁决，不预设倾向。**

| gate-ID | 决策点 | 影响范围 | 候选选项（不裁决） | 来源面 | 落点 |
|---------|--------|----------|--------------------|--------|------|
| `G-{PHASE}-1` | `{DECISION_POINT}` | `{IMPACT}` | `{OPTION_A / OPTION_B}` | `01` | `{PHASE}/pre-charter-qna.md` |

---

## 5. 阶段工作目标雏形（非冻结）`[核心]`

> 基于预核查给本阶段一个"打算达成什么"的雏形（charter 之前的草图），**非冻结边界**。

- **一句话目标**：`{PHASE_GOAL}`
- **拟纳入**：`{TENTATIVE_IN_SCOPE}`

---

## 6. 边界 / Out-of-Scope `[核心]`

> 显式划走不做的，并标注承接相位，防越界、防把已规划项误判遗漏。

| 编号 | 排除项 | 为什么不在本阶段 | 承接相位 |
|------|--------|------------------|----------|
| `[O1]` | `{OUT_ITEM}` | `{WHY_OUT}` | `{NEXT_PHASE_OR_OWNER}` |

---

## 7. 已交付 · 勿重做 `[核心]`

> 上游阶段已交付的 substrate，本阶段只做 delta；显式列出防止重复规划。

| 已交付项 | 交付于 | 本阶段对它的关系 |
|----------|--------|------------------|
| `{DELIVERED}` | `{PREV_PHASE}` | `沿用 / 仅 delta / 不动` |

---

## 8. 后续使用方式（流水线指引）`[核心]`

> 说明本 index 如何驱动后续：站② 逐面深挖 → 站③ 汇总规划 → 站④ owner 裁决 → 站⑤ 执行计划 → 站⑥ 落地。

- **站② 入口**：对 §1 每个面产出一份 [[assessment-analysis]]（消费 §2.2 冻结分母）。
- **站③+ 出口**：N 份 analysis 的缺口台账/契约草案/owner-gate 候选 → `{PHASE}/proposed-planning.md` → `pre-charter-qna.md`（裁决）→ `final-execution-plan.md` → `action-plan`。

---

## 9. 交叉引用 `[可选]`

- `{RELATED_DOCS}`

---

## 附录 · 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（站① 预核查 + 评估地图） |
