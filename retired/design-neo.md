# Nano-Agent 重轨设计模板（design-neo · 减法版）

> **模板类型**：`design-neo`（design 家族 · **Track D 重轨的默认 design**，原 `design.md` 的 refocus 减法版）
> **一句话定位**：重轨（有 charter）下，design **只做 combo 三件套（eval-planning + reference-anchor + qna）做不到的那几件事**——净新契约的叙述规格、**跨功能系统一致性**、深度 tradeoff 辩证、术语、净新架构边界。其余（既有边界/锚、决策、相位/排期、work-item exit、外部参考、Value Verdict）**一律委派或删除**。design 因此在重载下价值最锐利：它只在自己不可替代的地方出现。
>
> ## 何时用 design-neo —— 充要条件
> 满足"重轨"（有 charter / foundation / 多月）**且**命中下列任一"design 必要性测试"：
> 1. 新增**对外 contract surface**（从零定义，非扩展既有）
> 2. 新增**架构接缝**（净新 decouple/aggregate，reference-anchor 无既有 ARCH 可锚）
> 3. **跨 worker 不变量 / 多功能必须拼成一个整体形态**（← design-neo 的核心价值）
> 4. 验收是**多字段 / 非显然**的
> 5. 涉及**安全信任边界**（威胁模型）
> 6. **onboarding 关键**：需新贡献者能读懂的叙述式契约
>
> ## 何时**不**用
> | 你的情形 | 用什么 |
> |----------|--------|
> | 整体走 combo 轻轨，仅**一处**净新 | `design-sketch.md`（无需 charter）|
> | 纯扩展既有 substrate、无净新 | 不写 design，combo 三件套足矣 |
> | 相位拆分 / 排期 | `eval-planning.md` |
> | 参考借鉴盘点 | `eval-reference-anchor.md` |
> | 需要完整三方参考对比 + Value Verdict 的最大化仪式 | `design.md`（原全量版，保留）|
>
> ## design 家族三件套定位（共享于 design.md / design-neo.md / design-sketch.md）
> | 模板 | 轨道 | 何时选 | 范围 | charter | 户口 |
> |------|------|--------|------|---------|------|
> | `design.md`（原全量版） | D 重轨 | 需完整三方对比 + Value Verdict 的特殊/历史场景 | 全功能 | 有 | `docs/design/` |
> | **`design-neo.md`（减法版·重轨默认）★** | **D 重轨** | **foundation/多月/净新多/争议；跨功能一致性是核心** | **多功能·跨功能协调** | **有** | `docs/design/` |
> | `design-sketch.md`（单簇补丁） | C combo 内 | combo 主体 + 一处净新 | 单簇净新 | 无 | frozen 后迁 `docs/design/` |
>
> ## 委派清单（做减法的本质 —— 这些 design-neo **不做**）
> | 不做 | 委派给 | 依据 |
> |------|--------|------|
> | 决策冻结（原 §9）| **`qna.md` register** | action-plan 一律绕过 design §9 直引 qna |
> | 既有架构边界 / 仓内 file:line 锚（原 §8）| **`reference-anchor`** | reference-anchor 的 ARCH/TR + 锚台账就是它的家 |
> | 外部三方参考对比（原 §4）| **`reference-anchor`** | 命名三件套已腐烂；reference-anchor 是正经家 |
> | scope/phase 边界 / 退出判据 | **`charter`** + `eval-planning final` | 重轨纲领归 charter |
> | work-item exit / 执行台账 | **`eval-planning final` / `action-plan`** | design 给契约规格，不给执行台账 |
> | Value Verdict（原 §10）| **删除** | 自评仪式，下游不消费 |
>
> **使用纪律**：本文是 design（冻决策 + 写验收）。会影响净新 contract/boundary/security 的问题必须在本文或其 qna register 冻结，不留给 action-plan。**只写净新与一致性**；任何"扩展既有"的部分指向 reference-anchor，不在此重写。

---

# `{DESIGN_TITLE}`（design-neo）

> **对象**：`{FEATURE_CLUSTER}`
> **日期**：`{DATE}`　**作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`design-neo`（重轨减法版 design；冻净新决策 + 写验收）
> **文档状态**：`draft | reviewed | frozen | superseded`
> **上游（已就位）**：
> - charter：`{CHARTER_DOC}`（scope/phase/exit 已冻）
> - qna register：`{QNA_DOC}`（owner 决策唯一真源；本文只读引用）
> - reference-anchor：`{REFERENCE_ANCHOR_DOC}`（既有 ARCH/TR + 借鉴锚；本文只读引用）
> **下游**：`{ACTION_PLANS_OR_EVAL_PLANNING}`
> **正规户口**：`docs/design/{phase}/`

---

## 0. 背景与委派声明

- **本设计要回答的（净新/一致性）问题**：
  - `{NET_NEW_OR_COHERENCE_QUESTION}`
- **继承的已冻结结论（只读）**：charter `{REF}` / qna `{Q-IDs}` / reference-anchor `{ARCH/TR}`。
- **本设计显式不做**（见头部委派清单）：决策→qna、既有边界/锚/参考→reference-anchor、scope/phase→charter、work-item exit→eval-planning/action-plan、Value Verdict→删。

---

## 1. 功能簇定义与术语对齐

- **一句话定义**：`{ONE_LINE_DEFINITION}`
- **边界**：包含 `{INCLUDED}`；不包含 `{EXCLUDED}`。
- **关键术语对齐**（必填）：

| 术语 | 定义 | 备注 |
|------|------|------|
| `{TERM}` | `{DEFINITION}` | `{NOTE}` |

---

## 2. 跨功能系统一致性（★ design-neo 的首要价值）

> combo 的 per-work-item 台账只见树木；这一节是**整片森林的形状**——N 个功能如何拼成一个连贯整体。这是 eval-planning / reference-anchor / qna 结构上都给不出的东西，是重轨 design 不可替代的核心。

### 2.1 整体形态一句话
> `{ONE_PARAGRAPH：本簇 N 个功能合起来构成什么系统形态}`

### 2.2 功能间一致性契约

| # | 一致性约束（跨功能不变量） | 涉及功能 | 为什么必须一致 | 违反后果 |
|---|----------------------------|----------|----------------|----------|
| C1 | `{CROSS_FEATURE_INVARIANT}` | `F1,F3` | `{WHY}` | `{IF_VIOLATED}` |

### 2.3 数据 / 控制流贯穿图

```text
{F1} ──▶ {shared seam} ──▶ {F3}
        └──▶ {F2}            （标出共享 seam / 单一真源 / 谁不能各写各的）
```

### 2.4 跨 worker 不变量（如涉及）
- `{CROSS_WORKER_INVARIANT}`（如：单一 lifecycle truth / 单一 status 词表 / 单一 contract 真源）

---

## 3. 净新架构边界（仅净新；既有 → reference-anchor）

> 只定义**净新**的 decouple/aggregate 接缝（reference-anchor 无既有 ARCH 可锚的部分）。落在既有 substrate 上的边界，指向 reference-anchor ARCH，不重写。

- **净新解耦点**：`{DECOUPLED}` — 依赖边界 `{BOUNDARY}`
- **净新聚合点**：`{AGGREGATED}` — 为什么收敛 `{WHY}`
- **将生成的新建文件 / 落点结构**（= action-plan 新建文件清单的来源）：`{NEW_FILES}`
- **既有边界（委派）**：见 reference-anchor ARCH-`{x}`。

---

## 4. 净新契约叙述规格（从零定义的对外契约）

> 逐净新功能写**叙述式契约**（input/output/core-logic/edge-cases/schema）。扩展既有契约的功能不在此——指向 reference-anchor / eval-planning。

### 4.x `{NET_NEW_FEATURE}`
- **输入 / 输出**：`{INPUT}` → `{OUTPUT}`
- **主要调用者**：`{CALLERS}`
- **核心逻辑**：`{CORE_LOGIC}`
- **净新 schema / 契约 shape**：`{SCHEMA_OR_CONTRACT}`
- **边界情况**：`{EDGE_CASES}`
- **与 §2 一致性约束的关系**：`{HOW_IT_HONORS_CROSS_FEATURE_INVARIANTS}`

---

## 5. 深度 Tradeoff 辩证（仅争议性架构）

> 用"选 X 不选 Y / 原因 Z / 代价 W / 重评 C"。只写**真正有争议、reference-anchor TR 的机制裁定覆盖不了**的方案级取舍。非争议可省。

1. 选 **`{X}`** 而非 **`{Y}`**
   - 为什么：`{WHY}`｜接受代价：`{COST}`｜重评条件：`{REVISIT_OR_NEVER}`

### 5.1 风险与缓解
| 风险 | 触发 | 影响 | 缓解 |
|------|------|------|------|
| `{RISK}` | `{TRIGGER}` | `{IMPACT}` | `{MITIGATION}` |

---

## 6. 验收格栅（feature-level；work-item exit 归 action-plan）

> 逐功能的可验证收口目标，键到 Test-ID。这是 design 产出、action-plan 与测试套件**双双消费**的格栅。注意：这里是**功能级验收**，不是 work-item 级执行 exit（后者归 eval-planning final / action-plan）。

| 功能 | 一句话收口目标 | Test-ID | 测试层（短途/spike/mega）|
|------|----------------|---------|---------------------------|
| F1 | ✅ `{VERIFIABLE_DONE}` | `{T01}` | `{LAYER}` |
| F2 | ✅ `{VERIFIABLE_DONE}` | `{T02}` | `{LAYER}` |

---

## 7. 收口、户口与下游

### 7.1 设计完成标准（frozen 前必满足）
1. 术语对齐（§1）+ 跨功能一致性契约（§2）确立。
2. 净新契约规格（§4）+ 验收格栅（§6）可验收。
3. 净新边界（§3）= action-plan 新建文件清单可机械展开。
4. 影响净新 contract/boundary/security 的问题已在本文或引用的 qna register **经 owner 裁决**冻结。
5. **户口已落实**：`docs/design/{phase}/` 正本。

### 7.2 下一步
- **解锁的 action-plan**：`{ACTION_PLAN_DOCS}`
- **委派回执**：决策→`{qna}`；既有边界/锚/参考→`{reference-anchor}`；scope/phase→`{charter}`；work-item exit→`{eval-planning/action-plan}`。

### 7.3 修订历史
| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（重轨减法版）|
