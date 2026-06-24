# Planning 簇 · final —— 冻结派生（三态成熟链 · 站③）

> **模板血统**：`planning`（独立高频血统：[[planning-initial]] → [[planning-proposed]] → `planning-final`（本文）。取代旧 `eval-planning.md`[已 retired]）。
> **一句话用途**：拿 owner 在 `pre-charter-qna` 冻结的 execution 真相 + HEAD 实测，对 [[planning-proposed]] 逐项 **critique**，把全态真相收成一张统一台账、把工作 execution-ready 定档，并 **1:1 派生并排序下游 action-plan**——每份 AP 在 §7 带齐 **4 份锁死台账**。作 action-plan 制作前**唯一执行基线**。
> **何时用**：[[planning-proposed]] 已收窄、owner 已在 `pre-charter-qna` 冻结相关决策。**何时不用**：见 [[planning-initial]] 头部。
>
> **承重梁（planning 簇共有脊 · 三态一致 · 不可删）**：
> 1. **逐级辨证 + 调整溯因（§3 承重段）**：§3 = **critique 裁定 [[planning-proposed]]**（`CONFIRM/CORRECT/REFINE/RESIZE/GAP/SCOPE↕`），每项调整带**驱动真相 Truth-ID**。**§3 缺失 = 链断**。
> 2. **双门渐进冻结 + 真相台账（§2 · Module① · 终态全集）**：final 是**第二道 owner-gate（execution 门，`pre-charter-qna`）**落点。§2 真相台账**汇总全态真相**：foundational `T-O`（initial）+ reference-checked `T-R`（proposed）+ **新增 execution `T-O`（pre-charter-qna）+ HEAD-实测 `T-R`**。
> 3. **planning 文档冻结零决策（精确义）**：真相由 qna / reference-anchor / HEAD 冻结，本文件只**带类型 CITE**（引 `Q编号 / RA-n / file:line`），不自冻。
> 4. **逐级 supersede 不回改前序**：本文取代 initial + proposed 两份，作唯一执行基线；真相台账 append-only。
> 5. **族 → 链 → 态**：本文件是阶段族 `{FAMILY}` 下 `{CHAIN_NAME}` 链的**站③**。
>
> **★ owner NORMATIVE 锁死项（本态结构不可降级）**：
> - **§2 真相台账**为 `[核心·锁死]`：须含 execution `T-O`（pre-charter-qna 索引）+ **≥1 条 HEAD-实测 `T-R`**（修正前序前提——实测证明这是最高杠杆防自欺事实）。
> - **§7 每份下游 AP 必带齐 4 份表格化台账 A/B/C/D**（缺任一 = 该 AP 欠规格 = final 不得 frozen）。
>
> **状态词汇**：`draft | reviewed | frozen | superseded`。**命名提示**：`final-execution-plan[-on-<scope>][-by-<author>].md`（是 `-plan` 不是 `-planning`）。
> **占位符约定**：`{UPPER_SNAKE}` backtick 包裹；`[核心]` 必填 / `[核心·锁死]` 不可删 / `[可选]` 视删。

---

# `{SUBPHASE}` —— Final Execution Plan（planning · 站③ final）by `{AUTHOR}`

> **stage**：`final`（站③·冻结/权威）· **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）· **时间**：`{DATE}`
> **本链 scope-fence**：阶段族 `{FAMILY}` 下 `{CHAIN_NAME}` 链站③。
> **文档性质（自宣告）**：**取代 [[planning-initial]] + [[planning-proposed]] 两份**，作 action-plan 制作前**唯一执行基线**；本文件冻结零决策（仅 CITE 真相）。
> **输入权威次序（NORMATIVE）**：`冻结 QnA（pre-initial + pre-charter）> HEAD 代码实测 > design artifacts`。
> **下游消费者**：§11.A 枚举的 N 份 action-plan（每份头部逐字引用本 final + 台账 ID 区间）。
> **文档状态**：`draft | reviewed | frozen | superseded`

---

## 0. TL;DR `[核心]`

- **核心论点**：`{ONE_PARAGRAPH_THESIS}`
- **本态相对 proposed 做了什么**：`{① §3 critique N 项·M 处 CORRECT；② §2 新增 execution T-O + HEAD-实测 T-R；③ §7 每 AP 补齐 4 台账；④ §11.A 派生排序 N 份 AP}`

---

## 1. Reference anchors / 输入与依据 `[核心]`

| 输入 | 类型 | 提供了什么 | 锚点 |
|------|------|------------|------|
| `{INPUT}` | `proposed / pre-charter-qna / HEAD 实测 / reference-anchor` | `{WHAT}` | `{FILE_OR_LINE / Q编号}` |

---

## 2. 规划真相台账（Planning Truth Register · 终态全集）★ `[核心·锁死]`

> **Module① · 全态真相单一真源**（吸收旧「§HEAD 实测」+「owner-decision-freeze」+「contract-surface-freeze」，消重复记账）。CITE 不自冻。

### 2.1 真相全表（append-only · 截至 final）

| Truth-ID | 类型 | 子类型 | 真相内容（一句话）| 来源（冻结权威）| 析出态 | 下游约束 |
|----------|------|--------|--------------------|------------------|--------|----------|
| `T-O-1` | `owner-gated` | `foundational` | `{scope=分相, AP≤8-9}` | `pre-initial-qna [Q1]` | initial | `§4 / §7` |
| `T-R-1` | `reference-checked` | `reference-anchor` | `{KV 不能做权威热层}` | `{file:line / RA-n}` | proposed | `§7 substrate` |
| `T-O-9` | `owner-gated` | `execution` | `{如：正文出 D1=HOT DO-SQLite+COLD R2}` | `pre-charter-qna [Q12]` | **final** | `§7 GTF3` |
| `T-R-9` | `reference-checked` | **`HEAD-实测`** | `{如：buildCheckpoint 是 identity no-op，无 turn_end 写者}` | `{file:line}` | **final** | `§3 CORRECT / §7` |

### 2.2 ★ HEAD-实测真相（`[核心·锁死]` · ≥1 条 · 修正前序前提）
> **owner NORMATIVE**：final 必须用 HEAD 实测修正前序前提（三态实践实证这是最高杠杆防自欺事实，如 fail-open DO lease / merge-gate 实已 ff-resync / 死 covers 零写者）。逐条钉 `file:line`，并登记为 §2.1 的 `T-R[HEAD-实测]`。

| Truth-ID | HEAD 事实（实测锚 `file:line`）| 对前序前提的修正 | 触发的处置（→ §3 / §7）|
|----------|--------------------------------|------------------|-------------------------|
| `T-R-9` | `{FACT}` | `{CORRECTION，如催生新 Q?}` | `{HANDLING}` |

### 2.3 contract-surface-freeze（如适用）`[可选]`
- **冻结的 contract surface（N 个）**：`{SURFACES}` · **背书方式**：`{前端碰撞 review / consumer endorsement}`

---

## 3. 辨证审核（critique 裁定上一阶段）+ 调整溯因 ★ 承重段 `[核心]`

> 裁定动词（默认，可覆盖）：`CONFIRM / CORRECT / REFINE / RESIZE / GAP / SCOPE↑↓`。**每行带"驱动真相 Truth-ID"列**（Module②）。
> **★ 仪式量判据（R3）**：若 [[planning-proposed]] 已逐项 HEAD code-verified，本表**绝大多数合法为 CONFIRM**，final 做"**薄 confirm-delta**"（实质变更集中少数几条）——**诚实兑现，不是偷工**；反之底层未定则须出现实质 CORRECT/supersede（必有驱动 `T-R[HEAD-实测]` 或 execution `T-O`）。

| item-ID | 裁定（CONFIRM/CORRECT/REFINE/RESIZE/GAP/SCOPE↕）| 处置 | **驱动真相（Truth-ID）** | 依据（`[Q?]` / `file:line`）|
|---------|------------------------------------------------|------|--------------------------|---------------------------|
| `{X3-07}` | `{VERDICT}` | `{HANDLING}` | `{T-O-9 / T-R-9}` | `{[Q12] / file:line}` |

- **承重 CORRECT 摘要**：`{逐条点名 final 翻转了 proposed 的哪些前提，← 哪条真相}`

---

## 4. 范围与非范围（In/Out-Scope · execution-ready 定档）`[核心]`

- **In-Scope [S1]**：`{ITEM}`（execution-ready；受 `{T-?}`）
- **Out-of-Scope / 延后 [O1]**：`{ITEM}`（指向 job-ledger / 后继波次）

---

## 5. 跨阶段贯穿主题（threaded themes · 冻结版）`[核心]`

- **技术路线红线**：`{TR_RED_LINES}` · **治理冻结面（capstone 红线）**：`{独立 PR / 安全复核 / schema-freeze / 防假绿 gate}` · **migration inventory（冻结编号）**：`{036/037/...}`

---

## 6. DAG（关键路径 + 并行窗）—— 冻结版 + 调整溯因 `[核心]`

```text
{FROZEN_CRITICAL_PATH + 并行窗 + 硬前置}
```

### 6.1 DAG 调整溯因（Module② · 相对 proposed DAG 改了什么 ← 哪条真相）
| DAG 变更 | 相对 proposed | **驱动真相（Truth-ID）** | 说明 |
|----------|---------------|--------------------------|------|
| `{如：新增 [Q12] 扩列 migration → GTF5 三项硬前置}` | `{原 → 现}` | `{T-O-9}` | `{WHY}` |

---

## 7. 逐下游 action-plan 工作台账（★★ 终态核心 · 每 AP 锁死 4 份台账）`[核心·锁死]`

> **锁死结构（owner NORMATIVE，不可删、不可降为可选）**：§7 下每一个 `### 7.x` = **一份预期下游 action-plan**（与 §11.A 1:1 映射）。每个 7.x **必须**带齐下列 **4 份表格化台账 A/B/C/D**；缺任一即该 AP **欠规格**、final 不得 frozen。**这 4 份 1:1 预填下游 AP** 的 `action-plan.md` §3/§4（工作）、§7（reference-anchor）、§8（测试）、§10（收口）。
> 图例：复用 `✅复用 / ♻️重 substrate / 🆕净新`；借鉴 `✅正例 / ⛔反例 / 🔶参考 / 🆕净新`。

### 7.x `{AP_NAME}`（`{owner-gate / Q 簇}`）

**台账 A · 工作清单**（工作内容 + 工作量预估 + 说明）
> `工作内容` 是承重列：净新/高风险拆有序子步 a/b/c（含边界 + 失败/降级路径）；扩展既有/复用一句话不注水。`受约束真相` 引 §2 Truth-ID。

| 编号 | lane / 类型 | 工作项 | 工作内容（怎么一步步建）| 工作量预估 | 复用 | 风险 | 受约束真相（Truth-ID）|
|------|------------|--------|--------------------------|------------|------|------|------------------------|
| `{AP-01}` | `{LANE}` | `{ITEM}` | `{HOW_STEP_BY_STEP / a)b)c)}` | `XS/S/M/L` | `✅/♻️/🆕` | `low/med/high` | `{T-O-9 / [Q?]}` |

**台账 B · reference-anchor 清单**（来源 + `file:line` + 正反例 + 新增）
| 锚 ID | 来源（`path:line` / URL）| 落点（这是什么）| 借鉴类型 | 处置 | 备注 |
|-------|---------------------------|------------------|----------|------|------|
| `A-1` | `{path:line}` | `{WHAT_IT_IS}` | `✅正例 / ⛔反例 / 🔶参考 / 🆕净新` | `✅复用 / ♻️ / 🆕新增` | `{NOTE}` |

**台账 C · 测试用例**（新增 / 修改 —— 必答"是新增还是复用既有"）
| Test-ID | 验证什么 | 类型（短途/spike/mega/soak）| 层 | 来源 | 映射（工作项 → 收口目标）| PASS 证据（四元组）|
|---------|---------|------------------------------|----|------|---------------------------|---------------------|
| `{AP}-T01` | `{WHAT}` | `{TYPE}` | `unit/集成/契约/live(D1)` | `🆕新增 {file} / ♻️沿用 {file} / 🔱fork {base}+{断言}` | `{AP-01 → 收口目标}` | `commit {sha} + {测试名} PASS + D1 {Q?} + {UTC}` |

**台账 D · 收口评估方案与标准**（具体评估方式 + 可验证标准）
| 收口目标 | 评估方式（Test-ID 映射 / 查询 / gate）| PASS 标准（一句话可验证）| 证据形态 |
|----------|----------------------------------------|--------------------------|----------|
| `{EXIT_GOAL}` | `{AP}-T01 / grep / check-*.mjs` | `{VERIFIABLE_CRITERION}` | `{commit + 测试/查询 + UTC}` |

- **DoD 硬闸**：`{Definition of Done = 测试台账全 PASS 映射 + 具体硬闸（如 test:gates EXIT0）}`
- **NOT-成功识别**：`{什么算"没做到"——防假绿}`

**[可选] ⚖️ 争议/讨论点 · 本 AP 详设**：`{external review / 跨模型争议点就地详设，如失败语义 / 验收口径}`

---

## 8. Owner decision gates —— gate-closure map `[核心]`

> 每 gate 由冻结 QnA 关闭，引对应 `T-O` Truth-ID，给下游唯一口径。

| gate | 对应冻结 `[Q]` / Truth-ID | 裁决结论（下游唯一口径）| 状态 |
|------|----------------------------|--------------------------|------|
| `G-X-1` | `[Q2] / T-O-2` | `{FROZEN_CONCLUSION}` | `CLOSED` |

- **结论**：`{设计阶段无 OPEN 决策项，可转入 action-plan / 仍余 N 项待 owner}`

---

## 9. 测试计划（+ 长程 capstone + evidence pack）`[核心]`

- **A 短途 / B spike / D mega**：`{SCOPE}`
- **长程 capstone**：`{命名下游 test-surface 文件，如 test/mega-journey/...mega.test.mjs；A–J 步}`
- **Evidence pack（每 phase 收口）+ DoD**：`{EVIDENCE_AND_DOD}`

---

## 10. 风险登记 `[核心]`

| 风险 | 触发 | 影响 | 缓解 |
|------|------|------|------|
| `{RISK}` | `{TRIGGER}` | `{IMPACT}` | `{MITIGATION}` |

---

## 11. 后继解锁 + action-plan 派生图 `[核心]`

- **解锁的下游价值**：`{web-v90 / FE / 下游 charter}`

### 11.A action-plan 派生与排序
> §7 的每个 AP 簇 **1:1 映射**一份下游 action-plan 文件；在此枚举并排序。

| AP 簇（§7.x）| 派生的 action-plan 文件 | 台账 ID 区间 | 时序 / 依赖 |
|--------------|--------------------------|--------------|-------------|
| `{7.1 GTF1}` | `{docs/action-plan/.../GTF1-*.md}` | `{GTF1-01..06}` | `{ORDER + 依赖约束}` |

> **路径纪律**：此处 action-plan 文件路径须与实际落盘路径一致（含子目录）；ID/名一旦写定，下游 AP 头部逐字引用。

---

## 12. Final recommendation `[核心]`

- **推荐序列**：`{RECOMMENDED_SEQUENCE}` · **一句话总结**：`{CLOSING_ONE_LINER}`

---

## 13. 交叉引用与修订历史 `[可选]`

- **交叉引用**：上游 [[planning-initial]] · [[planning-proposed]] · 下游 §11.A 的 N 份 action-plan
- **修订历史**：

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v1.0 | `{DATE}` | `{AUTHOR}` | 冻结版（critique + 真相台账全集 + 4 台账/AP + 派生图）|

---

## 附录 A · 站③ 速用（本态填哪些）

| 段 | 站③ final 填法 |
|----|----------------|
| §2 真相台账 | **全态全集**（+ execution `T-O` + HEAD-实测 `T-R` ≥1 + contract-surface-freeze）`[锁死]` |
| §3 辨证审核 | 2.C critique vs proposed + **驱动真相列**（薄 confirm-delta 合法，见 §3 R3）|
| §6 DAG | 冻结版 + 6.1 DAG 调整溯因（← Truth-ID）|
| §7 工作台账 | **每 AP 锁死 4 台账 A/B/C/D** `[锁死]` |
| §8 gates | gate-closure map（全 CLOSED ← T-O）|
| §11 | + 11.A action-plan 派生排序图 |
| 自宣告 role | "取代两份，唯一执行基线" |

## 附录 B · 裁定动词 rubric 参考（§3 可覆盖，随作者/lineage 变）

| 来源 lineage | proposed 阶段词表 | final 阶段词表 |
|------|-------------------|----------------|
| MCCM（Opus）| `KEEP / REFRAME / CLOSED / NEW` | `CONFIRM / CORRECT / REFINE / GAP` |
| MCX（Opus）| `CONFIRM / REFINE / CORRECT / RESIZE` | `+ SCOPE↑ / SCOPE↓` |
| MI（GPT proposed）| `采纳 / 调整后采纳 / 不纳入` | `保留 / 升级 / 撤销 / 新增` |
| first-skill（Fable）| `KEEP / REFRAME / RESIZE↓ / NEW / FENCE` | `CONFIRM / CORRECT / EXPANDS` |

> 复用判定符通用：`✅ 复用 / ♻️ 重 substrate / 🆕 净新`。
