# Nano-Agent 设计速写模板（design-sketch）

> **模板类型**：`design-sketch`（design 家族 · **Track C 轻轨内的"净新逃生口"**）
> **一句话定位**：当一个 sub-phase 整体走 **combo 轻轨**（eval-planning 三态 + reference-anchor + qna，无 charter、无重轨 design），但其中**恰好有一处** combo 三件套装不下的**净新契约 / 净新架构接缝**时——给那一处写一份轻量设计补丁，而**不必为它把整条 sub-phase 升级到重轨**。
>
> ## 何时用 design-sketch —— 充要条件（三条同时成立）
> 1. 这个 sub-phase 整体走 **Track C（combo）**：没有独立 charter，主体由 `eval-planning + reference-anchor + qna` 承载；
> 2. 其中**恰好有一处（或一组紧耦合的）净新**触发了 `design 必要性测试`（**净新对外契约面 / 净新 decouple-aggregate 接缝 / 多字段非显然验收 / 安全信任边界**）；
> 3. 这一处净新**不足以让整条 sub-phase 升重轨**——它是一片扩展既有的海洋里的**净新孤岛**。
>
> **一句话**：design-sketch = combo 轻轨里，给"那一处 combo 装不下的净新东西"的轻量补丁。
>
> ## 何时**不**用（防止 owner 再次困惑）
> | 你的情形 | 该用什么，而不是 design-sketch |
> |----------|-------------------------------|
> | 整条 phase 是 foundation / 多月 / 净新契约多 / 争议架构 | **`design-neo.md`（重轨减法版）+ charter** |
> | 纯扩展既有 substrate、无净新（如 MCX3-MCX4 的扩展既有部分）| **不写任何 design**，combo 三件套足矣 |
> | 这是相位拆分 / 工作排期（initial→proposed→final）| **`eval-planning.md`** |
> | 这是"借哪些参考、怎么借"的盘点 | **`eval-reference-anchor.md`** |
> | 这是测试体系治理 / spike 设计（如 MCS3/MCS4）| **`eval-planning.md`**（它是 planning，不是 design）|
> | 想要完整三方参考对比 + Value Verdict 的最大化仪式 | **`design.md`（原全量版）** |
>
> ## design 家族三件套定位（共享于 design.md / design-neo.md / design-sketch.md）
> | 模板 | 轨道 | 何时选 | 范围 | charter | 户口 |
> |------|------|--------|------|---------|------|
> | `design.md`（原全量版） | D 重轨 | 需完整三方对比 + Value Verdict 的特殊/历史场景 | 全功能 | 有 | `docs/design/` |
> | `design-neo.md`（减法版·重轨默认）★ | D 重轨 | foundation/多月/净新多/争议架构；**跨功能一致性是核心** | 多功能·跨功能协调 | 有 | `docs/design/` |
> | **`design-sketch.md`（单簇补丁）** | **C combo 内** | combo 主体 + **一处净新** | **单簇（或紧耦合数簇）净新** | **无**（co-located in eval/） | frozen 后迁 `docs/design/` 或建交叉索引 |
>
> **使用纪律**：
> 1. 本文是 **design**（冻决策 + 写验收），不是 eval（提案、冻结零）。它只覆盖那**一处净新**，不复述 combo 已承载的扩展既有部分。
> 2. **冻结门槛（硬规则）**：本文的 QNA（§6）**必须由 owner 裁决**（有 `业主回答`）才能标 `frozen`；**严禁自答**。
> 3. **户口规则（硬规则）**：一旦 `frozen`，必须在 `docs/design/<phase>/` 落正本或建交叉索引；头部 `正规户口` 字段必填。
> 4. **委派纪律（做减法）**：既有边界/锚 → `reference-anchor`；owner 决策 → `qna`；相位/排期 → `eval-planning`；work-item exit → `action-plan`。本文**只写 combo 装不下的净新部分**。

---

# `{SKETCH_TITLE}`（design-sketch · 单簇净新）

> **对象**：`{ONE_NET_NEW_CLUSTER}`（本 sub-phase 中唯一/紧耦合的净新孤岛）
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`design-sketch`（Track C 内净新补丁；冻决策 + 写验收）
> **所属 sub-phase（走 combo）**：`{EVAL_PLANNING_FINAL + REFERENCE_ANCHOR + QNA}`
> **触发的必要性条件**：`{净新契约面 | 净新接缝 | 多字段非显然验收 | 安全信任边界}`（写明命中哪条）
> **正规户口（frozen 前必填）**：`{CANONICAL_HOME_IN_docs/design_OR_CROSS_INDEX}`
> **文档状态**：`draft | reviewed | frozen | superseded`

---

## 0. 背景：为什么这一处需要 design，而其余不需要

- **本 sub-phase 整体形态**：`{大部分为扩展既有，由 combo 承载；列出 combo 三件套链接}`
- **这一处为什么是净新（combo 装不下）**：`{为什么 reference-anchor 无既有 ARCH 可锚 / qna 一句话答不清 / 涉及新契约}`
- **本文不覆盖什么**：`{扩展既有部分明确交回 combo，不在此复述}`

---

## 1. 净新簇定义与术语对齐

- **一句话定义**：`{ONE_LINE}`
- **边界**：本簇**包含** `{INCLUDED}`；**不包含** `{EXCLUDED, → combo}`。
- **关键术语对齐**（必填；净新概念尤其要消歧）：

| 术语 | 定义 | 备注 |
|------|------|------|
| `{TERM}` | `{DEFINITION}` | `{NOTE，如"当前 schema 不存在此枚举"}` |

---

## 2. 净新架构边界（仅净新；既有 → reference-anchor）

> 只写这一处的净新 decouple/aggregate 接缝；任何落在既有 substrate 上的边界，指向 reference-anchor 的 ARCH 锚，不在此重写。

- **净新解耦点**：`{DECOUPLED}` — 依赖边界 `{BOUNDARY}`
- **净新聚合点**：`{AGGREGATED}` — 为什么收敛 `{WHY}`
- **将生成的新建文件**（= 本簇落点结构）：`{NEW_FILES}`
- **既有边界（委派）**：见 `{REFERENCE_ANCHOR}` ARCH-`{x}`。

---

## 3. 净新契约叙述规格（核心）

> design-sketch 的承重段：把这一处净新对外契约**从零叙述清楚**（reference-anchor 锚既有、无可锚的净新必须有人写）。扩展既有契约的部分不写，指向 reference-anchor / eval-planning。

### 3.x `{NET_NEW_FEATURE}`
- **输入 / 输出**：`{INPUT}` → `{OUTPUT}`
- **核心逻辑**：`{CORE_LOGIC}`
- **契约 / schema（净新）**：`{CONTRACT_OR_SCHEMA_SHAPE}`
- **边界情况**：`{EDGE_CASES}`
- **一句话收口目标**：✅ **`{VERIFIABLE_DONE_CRITERION}`**

---

## 4. In-Scope / Out-of-Scope（仅本簇）

- **In**：`{NET_NEW_ITEMS}`
- **Out / 交回 combo**：`{ADDITIVE_ITEMS → combo}`；交回 `{WHERE}`

---

## 5. Tradeoff（仅当本簇有争议性取舍时填）

> 选 X 不选 Y / 原因 / 代价 / 重评条件。非争议可省。

1. 选 **`{X}`** 而非 **`{Y}`**：为什么 `{WHY}`｜代价 `{COST}`｜重评 `{REVISIT}`

---

## 6. QNA / 决策登记（冻结门槛段）

> 硬门槛：每条 owner/architect 级决策**必须有 `业主回答`** 才能冻结。自答不算冻结。可内嵌，亦可引用 `qna.md` register。

| Q ID | 问题 | 影响 | 当前建议 | 状态 | 业主回答 / register |
|------|------|------|----------|------|---------------------|
| `{Q1}` | `{QUESTION}` | `{IMPACT}` | `{REC}` | `open/answered/frozen` | `{OWNER_ANSWER_OR_LINK}` |

---

## 7. 收口、户口与下游

1. **完成标准**：术语对齐 + 净新契约规格可验收 + §6 QNA 经 owner 裁决冻结。
2. **正规户口已落实**：`docs/design/{phase}/` 正本或交叉索引（头部字段已填）。
3. **解锁的 action-plan**：`{ACTION_PLAN}`（本簇净新落地）。
4. **委派回执**：既有部分 → reference-anchor / qna / eval-planning（不在本文）。

### 修订历史
| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（单簇净新补丁）|
