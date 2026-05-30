# Nano-Agent 支线设计速写模板（design-sketch）

> **模板类型**：`design-sketch`（design 家族的**轻量支线变体**）
> **一句话定位**：给那些**紧贴某份 eval、从主线编号设计流水线分叉出来的"支线 / 插曲设计"**一个正规模板——它是 design（冻结决策 + 写验收），不是 eval（提案、冻结零）。
> **它解决什么**：历史上这类设计被直接写在 `docs/eval/**` 里（test-governance / spike / 韧性核 / 债务收束等），导致 design 内容寄生在 eval、`docs/design/` 查无户口、有的还没守冻结门槛（QNA 自答）。本模板把它们**规范化 + 给户口 + 设门槛**。详见 `docs/templates/re-design/eval-docs-re-design.md` §12–§18。
>
> **定位三角（用前先对号）**：
>
> | 你在做什么 | 用哪个模板 |
> |------------|------------|
> | 还在"提案该做什么、冻结零决策" | `eval-general-purpose.md`（eval） |
> | 对照参考找我方缺口 | `eval-gap-study.md`（eval） |
> | **支线/插曲设计**：要冻决策+写验收，但不需要完整三方参考对比与代码书签清单 | **`design-sketch.md`（本模板）** |
> | 主线大簇阶段设计（如 MID/MCD 编号链） | `design.md`（完整版） |
> | 排执行序列 | `action-plan.md` |
>
> **使用纪律（design 模态）**：
> 1. 本文是 **design**：会影响 contract/boundary/scope/runtime-posture/security 的问题**必须在本文或其 QNA register 冻结**，不留给 action-plan。
> 2. **冻结门槛（硬规则）**：embedded/引用的 QNA **必须由 owner 裁决**（有 `业主回答`）才能把 `文档状态` 标 `frozen`；**严禁 QNA 自答**（`答复来源=本设计`）——自答的只能停在 `draft`。
> 3. **户口规则（硬规则）**：一旦 `frozen`，必须在 `docs/design/<phase>/` 落正本或建**交叉索引**，不得只活在 `docs/eval/`。头部 `正规户口` 字段必填。
> 4. **轻量边界**：本速写**省略** `design.md` 的"§4 三方参考实现横向对比"与"§8 可借鉴代码位置清单"两块重型章节；如确需借鉴对照，压缩进 §3/§6 即可。其余 design 承重机制（边界 / scope / tradeoff / In-Scope 详列+验收 / QNA / Value Verdict）一个不少。

---

# `{SKETCH_TITLE}`

> **对象**：`{FEATURE_CLUSTER_OR_INTERLUDE}`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`design-sketch`（支线设计；冻结决策 + 写验收）
> **文档状态**：`draft | reviewed | frozen | superseded`
> **母本 / 触发 eval（必填）**：`{TRIGGER_EVAL_OR_母本}`（本设计紧贴/消费的那份 eval）
> **正规户口（frozen 前必填）**：`{CANONICAL_HOME_IN_docs/design_OR_CROSS_INDEX}`
> **QNA register**：`{EMBEDDED_§7 | 外置 {QNA_FILE}}`（冻结门槛=owner 裁决）
> **上游权威输入**：
> - `{INPUT_1}`
> **下游交接**：
> - `{ACTION_PLAN_OR_HANDOFF}`

---

## 0. 背景与前置约束

> 为什么现在做这个支线设计、它从哪份 eval / charter / closure 继承输入、母本是谁、本设计不再讨论什么。

- **本设计要回答的问题**：
  - `{DESIGN_QUESTION_1}`
- **继承的已冻结结论**：
  - `{FROZEN_PREMISE}`（来源：`{REF}`）
- **母本指认**：本设计直接消费 `{TRIGGER_EVAL}` 的 `{SECTION/FINDINGS}`。
- **显式排除**：
  - `{OUT_OF_DISCUSSION}`

---

## 1. 讨论对象与功能簇定义

- **一句话定义**：`{ONE_LINE_DEFINITION}`
- **边界**：包含 `{INCLUDED}`；不包含 `{EXCLUDED}`。
- **关键术语对齐**（必填；术语对不齐则后续 action-plan 不应开始）：

| 术语 | 定义 | 备注 |
|------|------|------|
| `{TERM}` | `{DEFINITION}` | `{NOTE}` |

---

## 2. 在 nano-agent 中的定位（精简）

- **一句话定位**：在 nano-agent 里，`{CLUSTER}` 是 **{ROLE}**，负责 **{RESPONSIBILITY}**，对上游提供 **{OFFERS}**，对下游要求 **{NEEDS}**。
- **关键相邻耦合**（只列强/中耦合，弱耦合可省）：

| 相邻 | 方向 | 耦合 | 说明 |
|------|------|------|------|
| `{NEIGHBOR}` | `{DIR}` | `强/中` | `{DETAIL}` |

---

## 3. 架构稳定性与边界

> 按需取用四类边界；不适用的删去。轻量但不能没有——支线设计最容易在这里漂移。

- **精简点（哪里可砍）**：`{CUT}` — 理由 `{WHY}`；重评条件 `{REVISIT}`
- **接口保留点（哪里留扩展口）**：`{EXTENSION_POINT}` — 第一版行为 `{FIRST_BEHAVIOR}`
- **完全解耦点（哪里必须独立）**：`{DECOUPLED}` — 依赖边界 `{BOUNDARY}`
- **聚合点（哪里刻意收敛）**：`{AGGREGATED}` — 为什么不能分散 `{WHY}`

---

## 4. In-Scope / Out-of-Scope

### 4.1 In-Scope（本设计确认要支持）
- **[S1]** `{ITEM}` — `{WHY_REQUIRED}`

### 4.2 Out-of-Scope（确认不做）
- **[O1]** `{ITEM}` — `{WHY_DEFERRED}`；重评条件：`{REVISIT}`

### 4.3 边界清单（灰色地带）
| 项目 | 判定 | 理由 | 后续落点 |
|------|------|------|----------|
| `{ITEM}` | `in/out/defer` | `{WHY}` | `{ACTION_PLAN_OR_FUTURE}` |

---

## 5. Tradeoff 辩证

> 用"我们选择 X 而不是 Y，原因 Z，代价 W，重评条件 C"的句式写清每个会影响执行路径的取舍。

1. **取舍 1**：选 **`{X}`** 而非 **`{Y}`**
   - 为什么：`{WHY}`｜接受的代价：`{COST}`｜重评条件：`{REVISIT_OR_NEVER}`

### 5.1 风险与缓解
| 风险 | 触发 | 影响 | 缓解 |
|------|------|------|------|
| `{RISK}` | `{TRIGGER}` | `{IMPACT}` | `{MITIGATION}` |

---

## 6. In-Scope 功能详细列表（design-grade 核心）

> 把 §4.1 的 S1/S2 展开为**可验证的验收条件 + 一句话收口目标**。这是支线设计区别于 eval 提案的承重段——写收口判据，不写执行任务（不写 `[ ] 创建文件 X`）。

### 6.1 功能清单
| 编号 | 功能 | 描述 | 一句话收口目标 |
|------|------|------|----------------|
| F1 | `{NAME}` | `{DESC}` | ✅ `{DONE_CRITERION}` |

### 6.2 详细阐述

#### F1：`{NAME}`
- **输入 / 输出**：`{INPUT}` → `{OUTPUT}`
- **主要调用者**：`{CALLERS}`
- **核心逻辑**：`{CORE_LOGIC}`
- **契约 / schema（如涉及）**：`{CONTRACT_OR_SCHEMA}`
- **边界情况**：`{EDGE_CASES}`
- **一句话收口目标**：✅ **`{DONE_CRITERION}`**

### 6.3 非功能性与验证策略
- **可观测性 / 稳定性 / 安全**：`{NFR}`
- **测试覆盖要求**：`{TEST_REQUIREMENT}`
- **验证策略**：`{HOW_TO_PROVE_DESIGN_HOLDS}`（具体命令由 action-plan 写）

---

## 7. QNA / 决策登记（冻结门槛段）

> **硬门槛**：本段（或引用的 register）中每条 owner/architect 级决策**必须有 `业主回答`** 才能冻结。**自答（答复来源=本设计）不算冻结**，文档只能停 `draft`。可内嵌，也可引用 `qna.md` register（推荐跨文档时外置）。

| Q ID | 问题 | 影响范围 | 当前建议 | 状态 | 业主回答 / register |
|------|------|----------|----------|------|---------------------|
| `{Q1}` | `{QUESTION}` | `{IMPACT}` | `{RECOMMENDATION}` | `open / answered / frozen` | `{OWNER_ANSWER_OR_REGISTER_LINK}` |

> 内嵌单 Q 的完整槽位（影响范围 / 为什么必须确认 / 当前建议 / Reasoning / second opinion / 问题 / 业主回答）请复用 `qna.md` 的逐 Q 块。

---

## 8. Value Verdict

| 维度 | 评级 (1-5) | 一句话 |
|------|------------|--------|
| 对 nano-agent 定位的贴合度 | `{R}` | `{WHY}` |
| 第一版性价比 | `{R}` | `{WHY}` |
| 风险可控程度 | `{R}` | `{WHY}` |
| **综合价值** | `{R}` | `{WHY}` |

---

## 9. 收口、户口与下游

### 9.1 设计完成标准（frozen 前必满足）
1. 关键术语已对齐（§1）。
2. 所有影响执行路径的问题已在 §7 或引用 register 中**经 owner 裁决**冻结。
3. **正规户口已落实**：`docs/design/{phase}/` 有正本或交叉索引（头部 `正规户口` 字段已填）。
4. `{OTHER_EXIT_CRITERION}`

### 9.2 下一步
- **可解锁的 action-plan**：`{ACTION_PLAN_DOC}`
- **需同步的设计文档 / 索引**：`{RELATED_DESIGN_OR_INDEX}`
- **需进入 qna register 的遗留问题**：`{QNA_ITEM_OR_NONE}`

### 9.3 修订历史
| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿 |
