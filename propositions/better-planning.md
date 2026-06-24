# 统一规划模板（initial → proposed → final）对比分析与推荐

> 文档对象：多章节子阶段 / 附加章节的三段式策划链 `initial-planning → proposed-planning → final-execution-plan`
> 作者：Claude Opus 4.8（3 条完整 triptych 全量对读 + 2 路并行子代理 section 级对比）
> 日期：2026-05-30
> 文档性质：`re-design 建议 / 向 owner 的汇报`（不冻结决策）
> 文档状态：`draft — 待 owner 审阅`
> 调查输入：
> - MCX3-MCX4 triptych（主样本，最新最完整，194→340→464 行）
> - MCCM（context-manipulation）triptych
> - more-intelligence triptych（跨模型：proposed 由 GPT 写）
> - pro-to-product（2 段变体：initial → re-planning → 直接 charter，无 final）
> 关联：`eval-docs-re-design.md`（§3 F3 planning 家族）、`design-sketch.md`、`more-templated-appendix.md`

---

## 0. 一句话结论（TL;DR）

`initial-planning / proposed-planning / final-execution-plan` **不是三种文档，是同一份文档的三个成熟态**（open → narrowed → frozen）。它们共享一条**不变骨架**，差异全在"成熟度"；把它们三个各写一套模板是错的——应该做**一个 stage-aware 的统一模板 `eval-planning.md`**，用一个 `stage` 字段切换 initial/proposed/final，骨架恒定、阶段差异块开关。

**承重不变量**（也是判断"是否到位"的唯一标尺）：**每一阶段都对它的上一阶段做一次辨证裁定**——initial 裁定原始 evals/owner 提案，proposed 裁定 initial，final 裁定 proposed。这条"逐级 adjudicate 前序"的链，就是它们是"一个成熟文档"而非"三个文档"的铁证。

对 owner 的核心建议：**做 1 个 stage-aware 统一模板**（不是 3 个），骨架固定 + 阶段块开关 + 7 处变体参数化；它专治"多章节子阶段 / 需要多份 action-plan"的策划，final 阶段直接 1:1 派生并排序下游 action-plan。

---

## 1. 调查方法与语料

- **完整 triptych 3 条**：MCX3-MCX4（主）、MCCM、more-intelligence；**2 段变体 1 条**：pro-to-product（initial → re-planning → 直接 charter，**跳过 final**）。
- **section 级对读**：2 路子代理逐文件抽 `##/###` 标题 + 头部字段 + 自我宣告 role，做"同一子阶段三态"纵向对比 + "跨 lineage"横向对比。
- **一个直接信号**：主 triptych 行数 **194 → 340 → 464**——**文档随成熟而生长**（initial=速写、final=全量），而非三份独立文档。

## 2. 核心发现：不是 3 种文档，是 1 个文档的 3 个成熟态

### 2.1 不变骨架（三态恒定，13 段）

下列段在**所有 6 个文件**中都出现（措辞/编号略变，职责不变）：

| # | 段 | 职责 |
|---|----|------|
| 1 | 头部（作者/时间/**性质-role 自宣告**/上游输入） | 声明自己是哪一态、取代谁 |
| 2 | TL;DR / 综述 | 一段论点 + 一句话 |
| 3 | Reference anchors / 输入与依据 | 站在哪些 eval/anchor 之上 |
| 4 | **辨证审核（裁定上一阶段）** ★ | **状态推进的物化段——见 §2.3** |
| 5 | 范围与非范围（In/Out-Scope） | C1/C3/C4 in、C2 占位、FE/context out |
| 6 | 跨阶段贯穿主题（threaded themes） | 横切 red-line / 治理 / migration |
| 7 | DAG（关键路径 + 并行窗） | MCX3∥MCX4、MCX3 先行 |
| 8 | 逐 phase 工作台账 | X3-01..07 / X4-01..04 ID 恒定 |
| 9 | 测试计划（A/B/D + T0 分层） | 短途/spike/mega |
| 10 | Owner decision gates | G-X-1..5 |
| 11 | 风险登记 | — |
| 12 | 后继解锁（successor unlock） | 解锁 web-v90 / 下游 |
| 13 | Final recommendation + 修订历史 | 收尾（修订历史 = Opus 惯例，见 §4） |

### 2.2 状态推进轴（同一内容 open → narrowed → frozen）

| 维度 | initial（开放） | proposed（收窄） | final（冻结） |
|------|----------------|------------------|---------------|
| **Owner gates** | OPEN（"要 owner 拍" + Opus 初步建议） | OPEN，依新 sizing 精炼 + 推荐 | **CLOSED**——每个 → 冻结 Q 答案；**无 OPEN 决策项** |
| **工作台账** | first-cut，"初判模块，待 pin" | 重分配 + verdict 标记 + worker 绑定 + a/b/c 拆解 | **action-plan 绑定**：lane + 复用 + 退出 + evidence + `[Qn]` |
| **范围(MCX4)** | 提案/条件式（0.5 vs 2-3 AP） | sized "够而不紧" 1.2-1.5 AP | **execution-ready 定档全量** 2.0-2.3 AP |
| **证据基** | 仅上游 gap-analysis | reference-anchor + HEAD ARCH 锚 + TR 过滤 | 冻结 QnA + ARCH 实测命中 + TR 红线 |
| **Δ 机制** | 无（它是原点） | **Δ 表 vs initial**（KEEP/REFRAME/CLOSED/NEW） | **critique vs proposed**（CONFIRM/REFINE/RESIZE/SCOPE↑↓）|
| **Migrations** | 未命名 | 036-038（条件于 gate） | 036/036'/037/038 固定 + schema-freeze |
| **自我 role** | "第①步，不是 baseline" | "取代 initial，唯一工作基线" | "取代两份，唯一执行基线，转 action-plan" |

> 单线追踪（X3-07 source_role）：initial 当开放选项"加列 vs json_extract"（G-X-5 OPEN）→ proposed **CORRECT 事实**（列根本不存在）→ final 冻结为 `[Q8] CLOSED`（加真列+CHECK+索引+backfill+扫所有 INSERT 写点）。**同一根线，open→narrowed→frozen。**

### 2.3 承重不变量：逐级辨证（每态裁定其前序）★

最关键的结构发现：**让状态转移"物化"的，是 §4 那张"辨证审核"表——每一态都对它的上一态做一次裁定**：

- **initial §辨证** 裁定**原始 evals / owner 的 7-part DAG**（"对 owner 7-part DAG 的辨证分析" / "相对 4 份 eval 的整合裁定"）。
- **proposed §辨证** 裁定 **initial**（"本计划相对 initial-planning 的修订裁定"）——**Δ 表在 proposed 是通用的**。
- **final §辨证** 裁定 **proposed**（"对 proposed-planning 的 critique" / "相对 GPT MI1~MI9 的增量"）。

这条"each stage adjudicates its predecessor"的链是**唯一贯穿三态的承重梁**，也是"它们是一个成熟文档而非三个文档"的最强证据。统一模板的 §4 必须是这张"裁定上一阶段"表，且**裁定动词随阶段升级**。

## 3. 逐阶段差异化（统一模板的阶段开关块）

### 3.1 initial（开放/速写）
- 模态：开放问题 + first-cut，文首明写"**不是 charter，不是 action-plan，第①步**"。
- 台账 first-cut，"初判模块，待 reference-anchor 期 pin"；**defer** file:line/详细测试/锚定。
- **无 Δ 表**（它是原点）；owner gates 真 OPEN；常**借用上一阶段 final 的骨架**（MCCM initial 以 MI final 为骨架）。

### 3.2 proposed（收窄/重锚）增量
- **Δ-裁定表 vs initial（通用必备）**：逐项 `KEEP/REFRAME/CLOSED/NEW`（或 `采纳/调整/不纳入`、`CONFIRM/REFINE/CORRECT/RESIZE`）+ 重分配到 phase。
- **自我 supersession**："取代 initial，pre-charter-qna 前唯一精炼工作基线"。
- **新证据驱动翻新**：reference-anchor / ARCH-1..8 / TR 过滤（剔除 RLS/Redis/行锁/OTel/分片…非 substrate 机制）。
- 工作项**拆解** a/b/c；migrations 编号；加 DoD/reference 附录；gates 精炼但仍 OPEN。

### 3.3 final（冻结/权威）增量
- **critique 表 vs proposed**（`CONFIRM/CORRECT/REFINE/GAP` 或 `保留/升级/撤销/新增`）。
- **冻结声明** + **owner 裁决替换 OPEN gates**：§冻结 QnA 裁决索引（NORMATIVE）+ §gate-closure map（每 gate → 冻结 Q → CLOSED）→ "无 OPEN 决策项，可转 action-plan"。
- **action-plan 解锁图**：§per-phase 退出 + migration + evidence pack；§长程 Mega 命名下游 test-surface 文件。
- **DoD/整体收口**：evidence pack（每 phase）+ 治理冻结面（独立 PR + 安全复核 + schema-freeze 测）。
- **净新章节**：HEAD 代码实测（修正前序前提、甚至催生新 Q15）/ 前端 IF 债 / API surface / docs 台账（均标【新增章节】）。

## 4. 必须参数化的 7 处变体（统一模板要留口）

跨 lineage 对比发现：骨架不变，但有 7 处**作者/lineage 相关**的变体，模板须参数化而非写死：

1. **裁定动词词表**：`KEEP/REFRAME/CLOSED/NEW`(MCCM-Opus) vs `采纳/调整/不纳入`(MI-GPT) vs `CONFIRM/REFINE/CORRECT/RESIZE/SCOPE↑↓`(MCX/final) vs `保留/升级/撤销/新增`(MI-final) → 模板给**默认 rubric + 可覆盖**。
2. **冻结槽双填充**：owner-decision-freeze（QnA 索引 + gate-closure map，MCCM/MCX）**和/或** contract-surface-freeze（N 个 surface + 前端碰撞背书，MI）→ 模板 final 留**两个可选 filler**。
3. **跨模型 handoff**：proposed 可由不同模型写（MI proposed=GPT），并带入自己的约定（数字 Phase、T0-T6 分层），下一态**继承其骨架**而非重置 → 模板须容忍换作者。
4. **输入权威栈分层**（MCCM 设计三件套）：`冻结 QnA > HEAD 代码 > design artifacts`，final §1 显式排权威次序 → 模板留"权威次序"字段。
5. **phase 命名 + 工作项 ID 方案**：MCCM1-4/`C1-/F1-` vs MI1-9/`W-/L-/IF-/API-/DOC-` → 参数化。
6. **final 长净新章节**：HEAD 实测 / 前端 IF / API / docs → 模板允许 final append 事实核验 + 贯穿债章节。
7. **capstone 测试形态**：长程 mega（MCX/MCCM）vs flagship soak（MI）；**修订历史**是 Opus 惯例（GPT proposed 没有）→ 设为**可选**收尾。

## 5. 与 action-plan 的关系（直接回应"多 action-plan 需求"）

这正是 owner 关心的核心——**当一个子阶段需要多份 action-plan 时，final-execution-plan 是那唯一的派生基线**：

- final §6 的 per-phase 工作簇**1:1 映射**下游 action-plan 文件：`MCX3-MP1/MP2/MP3 → MCX3-*.md`；`MCX4-NP1/NP2/NP3 → MCX4-*.md`（两份 action-plan 头部"上游前序"逐字引用 final v1.0 + 台账 ID 区间）。
- final **枚举并排序**这些 action-plan：§时序与后继解锁给 `MCX3-MP1→MP2→MP3 ∥ MCX4-NP1→NP2→NP3` + `[Q1] MCX4 不抢 MCX3-C3 带宽`。
- 三态链最终落到真实 action-plan 并跑完（两份 action-plan 有匹配 closure）。**所以三态规划链的产出物，就是"一组有序、有依赖、有台账 ID 锚的 action-plan 工作安排"**——这就是 owner 要的"对多 action-plan 需求的统一工作安排"。

> 一个真实勘误也说明 final 的权威性：action-plan 顶部"⚠️ MIGRATION 编号勘误"box 把 final 的逻辑号（036/036'/037/038）映射到实际线性化文件（037/038/039/040 + 2nd-pass 加的 041），语义不变、以 `migrations-schema-freeze.test.ts` 为准。

## 6. 推荐：一个 stage-aware 统一模板 `eval-planning.md`

### 6.1 设计原则
**一套骨架（§2.1 的 13 段）+ 一个 `stage` 开关（initial/proposed/final）+ 阶段差异块（§3）+ 7 处变体参数化（§4）。** 作者随成熟度把模板复制三次、翻 `stage` 字段、填对应差异块——正如真实 triptych 三份独立文件、后者 supersede 前者。

### 6.2 与 `eval-general-purpose` 的边界（避免重复）
- `eval-general-purpose`（已建）= **轻量单次**规划/scoping（initial-thoughts、快速 scope，一份了事）。
- `eval-planning`（本推荐）= **重型三态**成熟链，**专用于"多章节子阶段 / 需要多份 action-plan"**，带逐级辨证 + 冻结 + action-plan 派生。
- 判据：**这个子阶段会派生 ≥2 份 action-plan、要走 initial→proposed→final 吗？** 是 → `eval-planning`；否（一次性想清楚）→ `eval-general-purpose`。

### 6.3 统一模板骨架草案（stage-conditional 标注）

```
# {SUBPHASE} —— {初步规划 | proposed-planning | Final Execution Plan}（by {AUTHOR}）
> stage: initial | proposed | final            ← 开关
> 作者 / 时间 / 上游输入
> 文档性质（自宣告 role）：
>   initial  = "第①步，不是 charter/action-plan"
>   proposed = "取代 initial，pre-charter-qna 前唯一精炼工作基线"
>   final    = "取代 initial+proposed，action-plan 前唯一执行基线"
> [仅 final] 输入权威次序：冻结 QnA > HEAD 代码 > design artifacts
> phase 命名 & 工作项 ID 方案：{MCCM1-4 / MI1-9 …}（参数化）

## 0. TL;DR
## 1. Reference anchors / 输入与依据
## 2. 辨证审核（裁定上一阶段）★ 承重段
   [initial] 裁定原始 evals / owner 提案（无 Δ 表）
   [proposed] Δ 表 vs initial：| item | 裁定(KEEP/REFRAME/CLOSED/NEW…可覆盖) | 重分配 phase | 复用(✅/♻️/🆕) |
   [final]    critique vs proposed：| item | 裁定(CONFIRM/CORRECT/REFINE/GAP…) | 处置 |
## 3. 范围与非范围（In/Out-Scope）
## 4. 跨阶段贯穿主题（red-line / 治理 / migration inventory）
## 5. DAG（关键路径 + 并行窗）
## 6. 逐 phase 工作台账
   [initial] first-cut（初判模块，待 pin）
   [proposed] 重分配 + verdict + worker 绑定 + a/b/c 拆解
   [final]    action-plan 绑定：lane + 复用 + 退出 + evidence + [Qn] + migration
## 7. Owner decision gates
   [initial] OPEN + 初步建议
   [proposed] OPEN + 依新 sizing 精炼
   [final]    gate-closure map：每 gate → 冻结 Q → CLOSED；声明"无 OPEN 决策项"
## 8. 测试计划（A 短途 / B spike / D mega + T0）
   [final] + 长程 capstone（mega 命名下游 test-surface 文件 / soak）+ evidence pack
## 9. 风险登记
## 10. 后继解锁 + action-plan 派生图
   [final] 命名并排序下游 action-plan 文件（§6 phase 簇 1:1 映射）
## 11. Final recommendation
## [仅 final · 可选净新章节] HEAD 代码实测 / 前端 IF 债 / API surface / docs 台账
## [仅 final · 冻结槽双填充] owner-decision-freeze（QnA 索引）和/或 contract-surface-freeze（碰撞背书）
## 12. 交叉引用与修订历史（修订历史 = 可选，跨模型 proposed 可缺）
```

## 7. 风险与落地

| 风险 | 判断 | 缓解 |
|------|------|------|
| 一个模板装三态，作者搞混该填哪块 | medium | `stage` 字段置顶 + 每段标 `[initial]/[proposed]/[final]`；提供三份最小示例 |
| 裁定动词词表写死，跨模型打架 | medium（已实测 GPT/Opus 词表不同）| 给默认 rubric + 显式"可覆盖"，§4.1 列四套已知词表 |
| 与 eval-general-purpose 重复 | medium | §6.2 判据划清：≥2 action-plan 且走三态 → eval-planning |
| 轻量子阶段被迫走三态、过度仪式 | medium | 2 段变体合法（pro-to-product: initial→re-planning→charter，跳 final）；模板允许"省略 proposed 或 final" |
| 跨模型 handoff 丢结构 | low | 模板声明"下一态继承上一态骨架"；修订历史设可选 |

**落地顺序**：① 先建 `eval-planning.md`（stage-aware 单文件）→ ② 用 MCX3-MCX4 三份历史 dogfood 回填三态各一次 → ③ 在 `eval-docs-re-design` 的 F3 planning 家族下登记它与 eval-general-purpose 的分工。

## 8. 一句话结论与给 owner 的决策问题

**一句话**：initial/proposed/final 是**一个文档的三个成熟态**，由"逐级辨证裁定前序"这条承重梁串起；应做**一个 stage-aware 统一模板 `eval-planning.md`**（骨架恒定 + 阶段块开关 + 7 处变体参数化），专治多 action-plan 子阶段，final 直接 1:1 派生并排序下游 action-plan。

**3 个决策问题**：
1. **采"一个 stage-aware 模板"**（我推荐），还是坚持三份独立模板？
2. **eval-planning 与 eval-general-purpose 的边界**用"是否 ≥2 action-plan + 是否走三态"切，可否？
3. **是否允许省略态**（2 段变体：initial→re-planning→charter 跳 final；或 initial→final 跳 proposed）作为合法用法？

---

## 附录 A · 三 triptych 的 section 对照（节选）

| 段 | MCX3-MCX4 | MCCM | more-intelligence |
|----|-----------|------|-------------------|
| 辨证裁定上一阶段 | initial§2 / proposed§3 / final§3 | initial§2 / proposed§2 / final§3 | initial§1 / proposed§2 / final§2 |
| 冻结机制 | owner-QnA（Q1-14）+ gate-closure | owner-QnA（Q1-15）+ gate-closure | contract-surface freeze（MI9 碰撞背书）|
| 跨模型 | 全 Opus | 全 Opus | **proposed=GPT**，initial/final=Opus |
| capstone | 长程 mega（A-J） | 长程 mega（A-K） | flagship soak（L-SOAK-14）|
| action-plan 派生 | MP1-3/NP1-3 → MCX3/MCX4 两份 | → web-v90 RW | → MI-Orchestrator + FE-MI |

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：3 triptych 对比 + "3 态非 3 型"结论 + stage-aware 统一模板 `eval-planning.md` 推荐 |
