# Planning 簇 · initial —— 初步规划（三态成熟链 · 站①）

> **模板血统**：`planning`（**独立高频血统**，三态各成独立文件：`planning-initial`（本文）→ [[planning-proposed]] → [[planning-final]]。取代旧 `eval-planning.md`[已 retired]——旧版一文件装三态、靠 `[仅 X]` 开关，实测易漂移；现拆分以**每态一张干净、不挤、零开关的专用骨架**精确引导）。
> **一句话用途**：给"多章节子阶段 / 需派生 **≥2 份 action-plan**"的策划链开场——把原始 eval / owner 提案**整合裁定**成一份初步工作蓝图（命名相位、first-cut 工作项、暂定前提、待核方向），作下游 [[planning-proposed]] 的裁定对象。
> **何时用**：一个子阶段会派生 ≥2 份 action-plan、要走完整三态成熟。**何时不用**：① 一次性想清楚、单 action-plan 的轻量 scoping → `eval-general-purpose.md`；② 冻结阶段边界/退出判据 → `charter.md`；③ 写可验证验收 → `design.md`；④ 排单份执行序列 → `action-plan.md`。
>
> **承重梁（planning 簇共有脊 · 三态一致 · 不可删）**：
> 1. **逐级辨证 + 调整溯因（§3 承重段）**：让"成熟态推进"物化的唯一血脉 = **每态对其前序做一次辨证裁定**，并**把每次 AP/DAG 调整绑定到驱动它的真相**（§2 真相台账的 Truth-ID）。initial 裁定**原始 eval / owner 提案**、proposed 裁定 initial、final critique proposed。**§3 缺失 = 链断 = 防自欺失效**。
> 2. **双门渐进冻结 + 真相台账（§2 · Module①）**：owner-gate 不止 proposed→final 一次——**整个阶段开工前 owner 可能先定基本原则**（`pre-initial-planning-qna`）。真相**逐态析出**并记入 §2 **规划真相台账（Planning Truth Register）**，分类型：
>    - `T-O` **owner-gated**（子类型 `foundational`=开工前定调门 / `execution`=charter 前细化门）；
>    - `T-R` **reference-checked**（reference-anchor 回灌 + HEAD 实测的事实）；
>    - `T-P` **provisional**（暂定前提，未冻结，待 proposed 证实/证伪）。
> 3. **planning 文档冻结零决策（精确义）**：真相由 **qna register / reference-anchor / HEAD 冻结**，planning 文档的真相台账只是**带类型 CITE（索引）已冻结真相**（引 `Q编号 / RA-n / file:line`），**本文件不自冻**。
> 4. **逐级 supersede 不回改前序**：proposed 取代 initial、final 取代两者；前序保留作历史 Δ 基线，不回改。真相台账**跨态 append-only**（Truth-ID 稳定）。
> 5. **族 → 链 → 态**：一个**阶段族**可起**多条**三态链（如 auth-ready 顶层 ∥ test-fixes ∥ longterm）；本文件是**某条链的站①**。头部写清本链 scope-fence。
> 6. **锚点纪律**：每条结论 / 真相带 `file:line` / `Q编号` / evidence；first-cut 可标"待 reference-anchor 期 pin"。
>
> **状态词汇**：`draft | reviewed | superseded`（成熟态 = 文件名/血统轴，勿塞进 status）。
> **命名提示**：与 `truth/` 簇（系统真值奠基 T1-T4）不同——本簇真相台账是**规划期真相**（塑造 AP 的决策 + 核查事实），勿混。实例文件 `initial-planning[-on-<scope>][-by-<author>].md`。
> **占位符约定**：`{UPPER_SNAKE}` backtick 包裹；`[核心]` 必填 / `[可选]` 视子阶段删除。

---

# `{SUBPHASE}` —— 初步规划（planning · 站① initial）by `{AUTHOR}`

> **stage**：`initial`（站①·开放/速写）
> **作者**：`{AUTHOR}`（panel / 跨模型：`{PANEL_OR_NONE}`）· **时间**：`{DATE}`
> **本链 scope-fence**：阶段族 `{FAMILY}` 下 `{CHAIN_NAME}` 链站①；**本链覆盖** `{WHAT_THIS_CHAIN_COVERS}`，**不含** `{OUT_OF_THIS_CHAIN}`。
> **文档性质（自宣告）**：设计流程**第①步**；不是 charter、不是 action-plan，**本文件冻结零决策**（仅 CITE 已在 `pre-initial-planning-qna` 冻结的 foundational 真相，见 §2）。
> **上游权威输入**：`{原始 evals / owner 提案 / pre-initial-planning-qna（如已冻结）/ 上一阶段 closure}`
> **下游消费者**：[[planning-proposed]]（站②，将裁定本文）
> **phase 命名 & 工作项 ID 方案**：`{如 GTF1-8 / ARTF1-10}`（参数化，ID 跨态稳定）
> **文档状态**：`draft | reviewed | superseded`

---

## 0. TL;DR `[核心]`

- **核心论点**：`{ONE_PARAGRAPH_THESIS}`
- **一句话**：`{ONE_LINER}`
- **本态已锚定的 foundational 真相**：`{有/无——若 pre-initial-planning-qna 已冻结，一句话点名其定调，见 §2}`

---

## 1. Reference anchors / 输入与依据 `[核心]`

| 输入 | 类型 | 提供了什么 | 锚点 |
|------|------|------------|------|
| `{INPUT}` | `eval / 提案 / pre-initial-qna / closure` | `{WHAT}` | `{FILE_OR_LINE / Q编号}` |

- **纪律继承**：`{INHERITED_DISCIPLINE}` · **借用骨架**：`{以哪份上一阶段 final 为格式骨架，如有}`

---

## 2. 规划真相台账（Planning Truth Register · 站①）★ `[核心]`

> **Module① · 本态真相切片**。**CITE 已冻结真相，不自冻**（§共有脊 3）。initial 态可含：① **foundational owner-gated 真相**（若 `pre-initial-planning-qna` 已冻结 —— 这是双门模型的第一道门）；② **provisional 暂定前提**（未冻结，待 proposed 证实/证伪）。Truth-ID 跨态稳定、append-only。

### 2.1 已冻结真相（CITE · 截至本态）

| Truth-ID | 类型 | 子类型 | 真相内容（一句话）| 来源（冻结权威）| 对本链的约束 |
|----------|------|--------|--------------------|------------------|---------------|
| `T-O-1` | `owner-gated` | `foundational` | `{如：本波 scope = 分相，AP 上限 8-9}` | `pre-initial-planning-qna [Q1]` | `{限定 §4 scope / §7 工作量}` |
| `T-O-2` | `owner-gated` | `foundational` | `{如：D1 留指针，context-core 拥有上下文真相写逻辑}` | `pre-initial-planning-qna [Q4]` | `{定 §7 归属相位}` |

> initial 态**通常无 `T-R`**（reference 尚未回灌）；若无任何 foundational 门，本表可仅一行「截至本态：无已冻结真相」。

### 2.2 暂定前提（Provisional · 待 proposed 证实/证伪）

| Truth-ID | 暂定前提（一句话）| 依据强度 | 待核方向（喂 reference-anchor）|
|----------|--------------------|----------|--------------------------------|
| `T-P-1` | `{CONJECTURE}` | `叙事/记忆/低` | `{要回哪段代码/参考核实}` |

---

## 3. 辨证审核（整合裁定原始 eval / owner 提案）★ 承重段 `[核心]`

> **站①承重梁**：把原始 eval / owner 提案逐项整合裁定，落到候选相位。**无 Δ-vs-plan 表**（initial 是原点）。**受约束列**：标该裁定受哪条 foundational `T-O` 约束（如有）。裁定动词：`纳入 / refine / 不纳入`。

| 来源项（eval / owner 提案）| 整合裁定 | 落到哪个 phase | 受约束真相（Truth-ID）| 备注 |
|------|----------|----------------|---------------------|------|
| `{EVAL_ITEM}` | `纳入 / refine / 不纳入` | `{PHASE}` | `{T-O-1 / —}` | `{NOTE}` |

---

## 4. 范围与非范围（In/Out-Scope · 提案态）`[核心]`

> **范围模态 = 提案/条件式**（非冻结边界）。**若 §2 有 foundational `T-O` 定了 scope/工作量上限，本节须遵从并引其 Truth-ID。**

- **In-Scope [S1]**：`{ITEM}` — `{WHY}`（受 `{T-O-?}`）
- **Out-of-Scope / 延后 [O1]**：`{ITEM}` — `{WHY_DEFER}`；重评条件：`{REVISIT}`

---

## 5. 跨阶段贯穿主题（threaded themes · 初判）`[可选]`

- **技术路线红线**：`{TR_RED_LINES}` · **治理冻结面**：`{…}` · **migration 初判**：`{编号待 proposed pin}`

---

## 6. DAG（关键路径 + 并行窗 · 初判）`[核心]`

```text
{PHASE}1 ──▶ {PHASE}2 ──▶ {PHASE}3        关键路径：{CRITICAL_PATH}
```

---

## 7. 逐 phase 工作台账 —— first-cut（初判，待 pin）`[核心]`

> **台账模态 = first-cut**：给候选工作项命名 + 粗估，**defer** `file:line` / 详细测试 / 锚定到 proposed。ID 跨态稳定。

### 7.x `{PHASE_NAME}`

| 编号 | 工作项 | 涉及模块（初判，待 pin）| 规模 | 风险 | 受约束真相（如有）|
|------|--------|-------------------------|------|------|--------------------|
| `{X3-01}` | `{ITEM}` | `{MODULE}` | `XS/S/M/L` | `low/med/high` | `{T-O-? / —}` |

---

## 8. Owner decision gates —— 开放 gates `[核心]`

> 把**仍 OPEN**（未冻结）的决策点列出 + 初步倾向。**已冻结的 foundational gate 不在此重列——它们已是 §2 的 `T-O`。**

| 编号 | 决策点 | 影响 | 当前建议 / 倾向 | 状态 |
|------|--------|------|------------------|------|
| `G-X-1` | `{DECISION}` | `{IMPACT}` | `{RECOMMENDATION}` | `OPEN` |

---

## 9. 测试计划（概要）`[可选]`

- **A 短途 / B spike / D mega**：`{SCOPE}`

---

## 10. 风险登记 `[核心]`

| 风险 | 触发 | 影响 | 缓解 |
|------|------|------|------|
| `{RISK}` | `{TRIGGER}` | `{IMPACT}` | `{MITIGATION}` |

---

## 11. 后继解锁 + 下游链意图声明 `[核心]`

- **解锁的下游价值**：`{web-v90 / FE / 下游 charter}`
- **★ 下游链意图（省略/停链须在此预告）**：
  - `[ ]` **满三态**：→ [[planning-proposed]] → [[planning-final]] → 派生 ≥2 action-plan；
  - `[ ]` **省略 proposed**：initial → final；
  - `[ ]` **停链转 charter**：initial → re-planning → charter（re-planning = proposed 的重型替身，喂 charter 而非 final）。
  > 勾选一项 + 一句话理由；**不得**只停在 initial 而不声明终点。

---

## 12. 交叉引用与修订历史 `[可选]`

- **交叉引用**：下游 [[planning-proposed]]
- **修订历史**：

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（整合裁定 + first-cut + 真相台账[foundational/provisional]）|

---

## 附录 · 站① 速用（本态填哪些）

| 段 | 站① initial 填法 |
|----|------------------|
| §2 真相台账 | foundational `T-O`（若 pre-initial-qna 已冻结）+ `T-P` 暂定前提（待核）|
| §3 辨证审核 | 整合裁定原始 eval / owner（**无 Δ 表**；标受 `T-O` 约束）|
| §7 工作台账 | first-cut（初判模块，待 pin）|
| §8 gates | 仍 OPEN 的 gate（已冻结 foundational gate 归 §2）|
| §11 | 解锁价值 + **下游链意图声明** |
| 自宣告 role | "第①步，本文件冻结零决策，仅 CITE foundational 真相" |
