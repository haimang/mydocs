# Nano-Agent Q&A 模板 · singular（单轮一次性 · 业主决策册）

> **模板簇**：`qna`（业主决策册 · 单一真源 register）。两形态：`qna-singular`（本文，**单轮一次性**——一批问题、业主逐题裁决、一次冻结）+ [[qna-progressive]]（多轮渐进——不断梳理真相驱动下一轮）。取代旧 `qna.md`[已 retired]。
> **一句话用途**：把会改变 contract surface / 实现边界 / 执行顺序 / 验收标准 / scope 的**业主决策**收敛到一份单一清单，逐题裁决、一次冻结，避免在多文档里重复回答、重复漂移、重复改口。
> **何时用**：决策点已基本梳清、可一批问完一次冻结（典型 `pre-initial-planning` 定调门 / `pre-charter` 关 gate 门）。**何时不用**：需"问一批→记录真相→评价→再注入下一批"的渐进梳理 → [[qna-progressive]]。
>
> **治理地位（qna 簇共有脊 · 两形态一致）**：
> 1. **单一真源**：业主只在本文件填 `业主回答`；其它 design / planning / action-plan / review 引用某 `Q` 编号，默认以本文件为唯一答复来源，不在别处重抄双方分析。
> 2. **Q 编号稳定 append**：补题往后续编（不回收旧号）；跨同 campaign 多份 qna 时 Q 编号全局唯一（接力续号）。
> 3. **冻结后只引 `Q 编号 + 业主回答`**；推翻已冻结答案须在本文件追加修订说明，不在他处悄改。
> 4. **★ 角色参数化（中性槽 · 文首一次性自填 · 取代旧"身份反转版特例"）**：
>    - `{ROLE_A}` = **提问 / 架构角色**（如 Opus / Fable / …）：负责 `影响范围 / 为什么必须确认 / 当前建议·倾向 / Reasoning / 问题`；
>    - `{ROLE_B}` = **second-opinion 角色**（如 GPT / none）：负责 second-opinion 三槽；
>    - `owner` = 裁决。
>    **角色就是普通头部字段，agent 自填，无需每次声明"反转"。** 字段名中性化：`{ROLE_B}的问题分解 / {ROLE_B}对{ROLE_A}推荐线路的分析 / {ROLE_B}的最终建议`（**禁写死模型名**）。
> 5. **second-opinion 模式三态**（头部声明）：`present`（{ROLE_B} 走完三槽）/ `waived`（owner 直答、三槽留空、不阻塞冻结）/ `retired`（不设 second-opinion 栏）。
> 6. **truth-gate 台账（冻结产物）**：qna 冻结的 **owner-gated 真相**记入 §(末) Truth-Gate 台账，类型 `T-O`（子类型 `foundational`=pre-initial 位点 / `execution`=pre-charter 位点），**ID 与 [[planning-initial]]/[[planning-final]] §2 真相台账共用 `T-O-*` 命名空间**，供 planning §2 直接 CITE。**qna 只产 `T-O`**（owner-gated）；`T-R`（reference-checked）来自 reference-anchor，不进本台账。
>
> **状态词汇**：`draft | reviewed | frozen | superseded`。**占位符约定**：`{UPPER_SNAKE}` backtick 包裹。

---

> **范围（scope）**：`{QNA_SCOPE}`
> **qna 位点**：`pre-initial-planning（开工前定调 scope/原则）| pre-charter（charter 前关 gate 执行细化）| deep-dive | spike-expansion`
> **角色配置（自填）**：提问 `{ROLE_A}` · second-opinion `{ROLE_B}` · 裁决 `owner`
> **second-opinion 模式**：`present | waived | retired`
> **下游消费者**：`{TARGET_DOCS_OR_PHASES，如 planning-* §2 / charter / action-plan}`
> **文档状态**：`draft | reviewed | frozen | superseded`

---

## 1. `{DECISION_CLUSTER_1}`

### Q{N} — `{QUESTION_TITLE}`（来源：`{SOURCE_DOCS}`）

- **影响范围**：`{IMPACT_SCOPE}`
- **为什么必须确认**：`{WHY_CONFIRMATION_IS_REQUIRED}`
- **当前建议 / 倾向**（`{ROLE_A}`）：`{CURRENT_RECOMMENDATION}`
- **Reasoning**（写给第一次参与该决策的业主）：`{PLAIN_LANGUAGE_REASONING_FOR_OWNER}`

- **`{ROLE_B}` 的问题分解**：`{或留空——见 second-opinion 模式}`
- **`{ROLE_B}` 对 `{ROLE_A}` 推荐线路的分析**：
- **`{ROLE_B}` 的最终建议**：

- **问题**：`{OWNER_FACING_QUESTION}`
- **业主回答**：`{冻结后 🔒 标 FROZEN}`

### Q{N+1} — `{QUESTION_TITLE}`（来源：`{SOURCE_DOCS}`）

- **影响范围**：`{IMPACT_SCOPE}`
- **为什么必须确认**：`{WHY}`
- **当前建议 / 倾向**（`{ROLE_A}`）：`{CURRENT_RECOMMENDATION}`
- **Reasoning**：`{REASONING}`

- **`{ROLE_B}` 的问题分解**：
- **`{ROLE_B}` 对 `{ROLE_A}` 推荐线路的分析**：
- **`{ROLE_B}` 的最终建议**：

- **问题**：`{OWNER_FACING_QUESTION}`
- **业主回答**：

---

## 2. `{DECISION_CLUSTER_2}`

### Q{N+2} — `{QUESTION_TITLE}`（来源：`{SOURCE_DOCS}`）

`{同上逐字段骨架}`

---

## 3. ★ Truth-Gate 台账（冻结产物 · owner-gated 真相 · 供 planning §2 CITE）`[核心]`

> **冻结后填**：把本 qna 逐题裁决出的 **owner-gated 真相**一次性列表，作交接给下游 [[planning-initial]]/[[planning-final]] §2 真相台账的成品。**ID 用 `T-O-*`**（与 planning 共命名空间，append-only，跨同 campaign 多份 qna 不撞号）。

| Truth-ID | 子类型 | 真相内容（一句话 · 下游唯一口径）| 来源 Q | 下游约束 |
|----------|--------|----------------------------------|--------|----------|
| `T-O-1` | `foundational / execution` | `{FROZEN_CONCLUSION}` | `[Q{N}]` | `{planning §2 / §4 scope / §7 …}` |

---

## 4. 使用约束

### 4.1 哪些问题应进 qna
- 会直接改变 **contract surface / 实现边界 / 执行顺序 / 验收标准 / 支持面披露 / scope** 的问题；
- 需 owner / 架构师拍板、实现阶段无法自行收敛的；
- 不先拍板会导致多个后续文档一起漂移的。

### 4.2 哪些问题不应进
- 实现细节微调（命名 / 内部脚本组织 / 单测布局）；已有 frozen answer 的重复提问（除非正式推翻）；只影响单包内部、不动外部治理边界的。

### 4.3 `Reasoning` 写法
- 写给非作者但要决策的人；解释：① 问题为何出现；② 推荐路线为何更稳；③ 不拍板的工程/业务后果。避免只写"建议这样做"而不给 trade-off。

### 4.4 `问题` 写法
- 必须是业主可直接作答的句子；尽量一题一决策；天然含两子决策须写明"如确认，请同时回答 X / Y"。

### 4.5 `业主回答` + 角色 + second-opinion 模式
- 业主回答简洁可执行；一旦填写即成下游唯一口径；推翻在本文件追加修订。
- **角色分配在头部一次性声明即可**（`{ROLE_A}` 提问 / `{ROLE_B}` second-opinion）；不再每题/每文重复声明"反转"。
- **second-opinion 模式**：`present` 须三槽走完；`waived` 三槽留空 + 头部注明"owner 直答、不阻塞冻结"；`retired` 直接不渲染 second-opinion 栏。三态都**不改变 qna 的信息密度与治理地位**。

---

## 5. 最小示例

### Q1 — `{EXAMPLE_QUESTION_TITLE}`（来源：`{EXAMPLE_SOURCE}`）

- **影响范围**：`{PACKAGE_A / DOC_B / PHASE_C}`
- **为什么必须确认**：`{EXAMPLE_WHY}`
- **当前建议 / 倾向**（`Opus`）：`{EXAMPLE_RECOMMENDATION}`
- **Reasoning**：`{EXAMPLE_REASONING}`
- **`GPT` 的问题分解**：`{或 waived 留空}`
- **`GPT` 对 `Opus` 推荐线路的分析**：
- **`GPT` 的最终建议**：
- **问题**：`{EXAMPLE_OWNER_FACING_QUESTION}`
- **业主回答**：`🔒 {FROZEN_ANSWER} → T-O-1`

---

## 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（角色参数化 + 三态 second-opinion + 冻结后 Truth-Gate 台账）|
