# Nano-Agent Q&A 模板 · progressive（多轮渐进 · 业主决策册）

> **模板簇**：`qna`（业主决策册 · 单一真源 register）。两形态：[[qna-singular]]（单轮一次性）+ `qna-progressive`（本文，**多轮渐进**——问一批 → owner 直答 → 记录真相 → agent 中场评估 → 由真相驱动下一批 → … → 收口冻结）。取代旧 `qna.md`[已 retired]。
> **一句话用途**：当方向/真相需**逐轮梳理**才能收敛（技术路线、engine 选型、震中再架构）时，用多轮 append 的问答链，把每轮裁出的真相累积进 Truth-Gate 台账，并**用已锁定真相驱动下一轮提问**，直到方向钉死、收口冻结。
> **何时用**：典型 `deep-dive`（多 Round 锁真值）/ 复杂震中定调；一次问不清、需"记录→评价→再问"。**何时不用**：一批问完一次冻结 → [[qna-singular]]。
>
> **治理地位（qna 簇共有脊 · 两形态一致）**：
> 1. **单一真源**：业主只在本文件填 `业主回答`；引用方默认以本文件为唯一答复来源。
> 2. **Q 编号稳定 append**：分轮续编、不回收（Round 1=Q1-5 → Round 2=Q6+ …）；跨同 campaign Q 全局唯一。
> 3. **冻结后只引 `Q 编号 + 业主回答`**；推翻在本文件追加修订。
> 4. **★ 角色参数化（中性槽 · 文首一次性自填）**：`{ROLE_A}`=提问/架构角色（Opus/Fable/…）· `{ROLE_B}`=second-opinion 角色（GPT/none）· `owner`=裁决。字段名中性化：`{ROLE_B}的问题分解 / {ROLE_B}对{ROLE_A}推荐线路的分析 / {ROLE_B}的最终建议`（**禁写死模型名**）。
> 5. **second-opinion 模式三态**（**可逐轮变**）：`present`（{ROLE_B} 走完）/ `waived`（owner 直答、留空）/ `retired`（自第 N 轮起退役、之后各轮不含 second-opinion 栏）。
> 6. **truth-gate 台账（本形态的引擎）**：每轮裁出的 **owner-gated 真相**累积进 §1 Truth-Gate 台账，类型 `T-O`（子类型 `foundational`/`execution`），**ID 与 [[planning-initial]]/[[planning-final]] §2 共用 `T-O-*` 命名空间**，供 planning §2 CITE。**qna 只产 `T-O`**；`T-R` 来自 reference-anchor，不进本台账。
>
> **★ 渐进锁死三件（owner NORMATIVE · 不可降级）**：① **每轮 Truth-Gate 台账**（§1 累积本轮新增 `T-O`）；② **轮间「中场评估」段**（agent 评上一轮 + 说明为何注入下一轮）；③ **下一轮每题须标「由哪条 `T-O` 驱动」**。三件缺任一 = 渐进链断、不可审计。
>
> **状态词汇**：`draft | reviewed | frozen | superseded`（分轮可分别冻结）。**占位符约定**：`{UPPER_SNAKE}` backtick 包裹。

---

> **范围（scope）**：`{QNA_SCOPE}`
> **qna 位点**：`deep-dive | pre-charter（多轮）| spike-expansion | …`
> **角色配置（自填）**：提问 `{ROLE_A}` · second-opinion `{ROLE_B}` · 裁决 `owner`
> **second-opinion 模式（逐轮）**：`{如 Round 1 present → Round 2 起 retired}`
> **下游消费者**：`{planning-* §2 / 联合 update 研究 / charter}`
> **文档状态**：`draft | reviewed | frozen | superseded`

---

## 0. 分轮状态总览

| 轮次 | 题号区间 | 焦点 | second-opinion | 状态 |
|------|----------|------|----------------|------|
| Round 1 | `Q1–Q5` | `{FOCUS}` | `present / waived` | `已冻结 / 进行` |
| Round 2 | `Q6–Q{n}` | `{FOCUS}` | `retired` | `已答 / 进行` |
| `…` | `…` | `…` | `…` | `…` |

---

## 1. ★ Truth-Gate 台账（已锁定真值 · NORMATIVE · append-only across rounds）`[核心·锁死]`

> **渐进引擎**：每轮 owner 答复即固化为编号 `T-O`，作"下游唯一口径 + 下一轮提问的约束"。冲突以本表为准。**ID `T-O-*` 与 planning §2 共命名空间。**

| Truth-ID | 子类型 | 已锁定真相（一句话）| 来源（Round / Q）| 驱动了哪些后续题 | 下游约束 |
|----------|--------|----------------------|--------------------|------------------|----------|
| `T-O-1` | `foundational / execution` | `{LOCKED_TRUTH}` | `Round 1 / [Q1]` | `{Q8 / Q16}` | `{planning §2 / scope}` |

---

## 2. Round 1 —— `{ROUND_1_FOCUS}`（`Q1–Q5`）

> 本轮 second-opinion 模式：`{present / waived}`。

### Q1 — `{QUESTION_TITLE}`（来源：`{SOURCE_DOCS}`）
- **影响范围**：`{IMPACT_SCOPE}`
- **为什么必须确认**：`{WHY}`
- **当前建议 / 倾向**（`{ROLE_A}`）：`{RECOMMENDATION}`
- **Reasoning**：`{REASONING_FOR_OWNER}`
- **`{ROLE_B}` 的问题分解 / 对 `{ROLE_A}` 推荐线路的分析 / 最终建议**：`{或 waived 留空}`
- **问题**：`{OWNER_FACING_QUESTION}`
- **业主回答**：`{🔒 冻结 → T-O-?}`

`{Q2–Q5 同骨架}`

---

## 3. ★ 中场评估 I（Round 1 → Round 2）`[核心·锁死]`

> **轮间承重段（锁死②）**：agent 评价上一轮 + 决定下一轮。

- **3.1 对 Round 1 的判定**：`{逐题答复是否决断；哪手最关键；有无遗留}`
- **3.2 本轮已锁定真相**：`{固化为 §1 的哪些 T-O}`
- **3.3 诚实反方制衡**：`{对已答方向的风险/反例，不掩盖}`
- **3.4 为什么提出 Round 2（注入哪些题 + 由哪条 T-O 驱动）**：`{Round 2 = Q6.. 之所以问，是因为 T-O-x 把方向钉死后，剩 {UNDECIDED} 未定}`

---

## 4. Round 2 —— `{ROUND_2_FOCUS}`（`Q6–Q{n}`）

> 本轮 second-opinion 模式：`{如 retired（自本轮起 owner 直答，不含 second-opinion 栏）}`。**每题须标「由哪条 `T-O` 驱动」（锁死③）。**

### Q6 — `{QUESTION_TITLE}`（**驱动真相：`{T-O-?}`** · 来源：`{SOURCE_DOCS}`）
- **影响范围**：`{IMPACT_SCOPE}`
- **为什么必须确认**：`{WHY，承接 T-O-? 后剩的未定点}`
- **当前建议 / 倾向**（`{ROLE_A}`）：`{RECOMMENDATION}`
- **Reasoning**：`{REASONING}`
- **问题**：`{OWNER_FACING_QUESTION}`
- **业主回答**：`{🔒 → T-O-?}`

`{Q7.. 同骨架，各标驱动真相}`

---

## 5. ★ 中场评估 II（Round 2 → Round 3）`[核心·锁死]`
`{同 §3 骨架：判定 Round 2 → 固化 T-O → 反方制衡 → 为何注入 Round 3（驱动真相）}`

---

## 6. Round 3+ —— `{…}`
`{按需续轮：Round N 题号续编、标驱动真相；轮间补「中场评估 III…」；收口轮把残留 🟡 题推进冻结}`

---

## 7. 收口（全轮冻结）

- **冻结判据**：方向钉死、§1 Truth-Gate 全 `T-O` 冻结、无 OPEN 残题（或残题显式 defer 并登记）。
- **交接**：§1 Truth-Gate 台账 → [[planning-initial]]/[[planning-final]] §2 CITE；下一步 `{联合 update 研究 / 统一 plan / 派生 AP}`。

---

## 8. 使用约束

- **进 qna 的判据 / Reasoning / 问题 / 业主回答**：同 [[qna-singular]] §4（治理一致）。
- **分轮纪律**：Q 编号 append 续编、不回收；每轮一个 focus；**严禁**一轮塞入与本轮 focus 无关的题（留下一轮）。
- **truth-gate 驱动**：下一轮的题必须能回答"它在 §1 哪条 `T-O` 钉死方向后、为补哪个未定点而问"——否则该题不该在本轮。
- **second-opinion 逐轮可变**：常见 `Round 1 present/waived → Round 2 起 retired`（owner 直答提速）；退役须在 §0 总览与对应轮标注，可随时恢复。

---

## 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（多轮 append + 中场评估 + 生成式 Truth-Gate 锁死三件）|
