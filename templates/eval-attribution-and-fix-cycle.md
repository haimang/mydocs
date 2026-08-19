# Nano-Agent Eval 模板 · attribution-and-fix-cycle

> **模板类型**：`eval / attribution-and-fix-cycle`
> **一句话用途**：对一次**已封存的正式 lane RED**做确定性取证与分平面归因，评价上一代修复包的真实分母，再给出 **path-cap 内**的下一代限缩修复设计 + 台账；owner 单独授权后，在文末 **append-only** 回填执行。
> **何时用**：owner-gate / 正式 journey 的 first-red 闭环（OG-08 的 **X 包**、**Y 包**及同形事故）。一份文件服务**一个修复包**对应**一个（或一对）封存 RED**。
> **何时不用**：
> 1. 还在想阶段装什么 → `eval-general-purpose`
> 2. 里程碑后回看水位/债务 → `eval-state-analysis`
> 3. 复盘一次决策失误（非本 lane 法医）→ `eval-retrospective`
> 4. owner-test 截图批次、无封存 lane root → `report/bug-analysis`
> 5. 多 Phase / 要派 ≥2 份 action-plan → `planning-final` → `action-plan`
> 6. 需要新的 owner 决策才能设计 → 先 `qna`，不要在本文偷偷冻结
> 7. 给阶段下收口结论 → `closure`
>
> **结构来源(dogfood)**：OG-08 X 系列（`FR-22/X11`、`FR-30/X18`）+ Y 系列成熟骨架（`Y8`～`Y10`）+ eval 共有脊 + `action-plan` 不可约三元组 + `code-execution-log` append 合同。
>
> **使用纪律（共有脊 · 所有 eval 模板一致 + 本 flavor 特化）**：
> 1. **头部 / 性质声明 / TL;DR / 输入锚定 / 修订历史**为 eval 共有脊。
> 2. **归因段冻结零决策**：§0～§4 只 CITE 封存证据 / 已冻 `Q` / HEAD `file:line`，不自冻新 owner 决策。
> 3. **修复设计是提案，不是授权**：§5～§11 写完后本包必须仍为 `NOT_EXECUTED_OR_AUTHORIZED`。编码 / deploy / preflight / 下一 lane **不得由本文自动授权**。
> 4. **Machine RED 不可改写**：反事实 GREEN、目标态、`{PACK} PASS` 条件都不能倒写成正式 lane PASS。
> 5. **分平面 verdict 禁止混写**：正式 lane / per-turn product / provider / 机制 / harness / 上代包 / 本代包必须分行。
> 6. **主体不回写**：授权后只允许 append §13 / §14；§0～§11 的事实、因果与（授权瞬间冻结的）设计原貌保持只读。对抗审查（§12）只允许在**授权前**回改 §5～§10。
>
> **占位符**：`{UPPER_SNAKE}` backtick 包裹。`[核心]` 必填 / `[核心·锁死]` 不可删或降为可选 / `[可选]` 视档删除 / `[阶段门]` 未到该阶段整节删除、留一句「未到阶段」。

---

## 怎么用这份模板（先选档 → 对阶段 → 再填）

### 档位（先选一档；不适用整节删除）

| 档 | 何时 | 对标 | 相对档 A 的增量 |
|----|------|------|-----------------|
| **A · 单 lane 焊件（默认）** | 一个 formal root、一个 first-red、一个修复包 | Y8 / Y10 / X18 | §0～§11 |
| **B · 双臂 / 多专项收敛** | 两臂对照（CC×RSP）或 ≥2 份专项报告必须并到同一 denominator | FR-30、Y9 | 启用 §2.5；§0.2 按臂/源分行 |
| **C · 手术刀补证** | 归因缺一条精确身份，owner **另行**授权有界 live 下载 | FR-22、FR-30 orphan | 下载前先冻 root；结果写入 §1.2 / §2.3，或授权来得晚则 **append §13** |

### 生命周期（文档状态 · 事故轨）

```text
draft
  → ANALYSIS_COMPLETE          §0～§4 闭环；§3.4 已判定能否设计
  → SCOPE_FROZEN               §5～§11 写完；allowlist / falsifier / 台账齐
  → ADVERSARIALLY_REVIEWED     §12 完成（可跳过，须在 §11 声明 waived）
  → AUTHORIZED_FOR_LOCAL       owner 单独授权编码与本地 test↔fix
  → EXECUTED_THROUGH_PREFLIGHT §14 回填至实际到达的最远闸
  → NEXT_LANE_READY_NOT_STARTED
  → superseded                 被后继包或后继文档取代
```

可与核心四态并用：分析未完成用 `draft`；设计已齐待授权用 `reviewed`；需要把 allowlist/因果锁死给执行者用 `frozen`（**文档定稿**，不是 owner 决策）。`executing | executed` 只描述执行面，写在头部「事故状态」串，不覆盖正式 lane 的 immutable RED。

### 阶段门：什么时候必须提供什么

| 阶段 | 必须已经有 | 本阶段必填 | 禁止做 |
|------|------------|------------|--------|
| **S0 开写** | 封存 lane 的 formal root / candidate SHA / 产品终态字符串；权限边界（本轮有无新 live） | 头部 + 档位 | 无 root 就写因果；无授权就远端读 |
| **S1 归因** `ANALYSIS_COMPLETE` | S0 | **§0～§4**（档 B 含 §2.5） | 因果未闭合就开 §5；把「未观察」写成「未发生」 |
| **S2 设计** `SCOPE_FROZEN` | §3.4 = `GO_DESIGN` | **§5～§11** | 撑破 cap 仍留在本文；未冻 Q 却当已决 |
| **S3 对抗** `ADVERSARIALLY_REVIEWED` | S2 初稿 | **§12**（或显式 `waived`） | 授权后再改 §5～§10 |
| **S4 授权执行** | owner 独立指令 + 授权范围 | **§14** 开始 append | 回写 §0～§11；local PASS 自动发下一 lane |
| **S5 补证（可插入）** | owner 有界 live 授权 | 当时在 S1 → 写入 §1/§2；已过 S2 → **只 append §13** | 用补证倒写原 machine RED |

§3.4 未放行时：**停在 `ANALYSIS_COMPLETE`**，§5～§11 整段删除，改写转出（见下方分支）。

### 逻辑分支（写到这里必须停或转出）

```text
§3.4 阶段门
├─ GO_DESIGN
│    因果 fit 高、残余 trigger 可用「同时关闭窗口」覆盖、无需新 Q、source/test 可压进 cap
│    → 继续 §5～§11
├─ HOLD_EVIDENCE
│    机制类已闭合、单一 trigger 未闭合，且现有 surface 无法再分
│    → 停；列精确缺什么；等 owner 授权档 C / §13，或接受「两窗口都关」的设计前提
├─ NEED_QNA
│    设计依赖尚未冻结的 owner 决策
│    → 转 qna；本文保持 draft/ANALYSIS_COMPLETE；不自冻
├─ ESCALATE_PLAN
│    必改 source 将超过 cap、需要 migration 簇以上、或必须拆 ≥2 份 AP
│    → 转 planning-final / action-plan；本文只保留归因，修复改下游
└─ NOT_THIS_TEMPLATE
     无封存 lane / 只是周期水位 / 只是决策复盘
     → 换模板（见「何时不用」）
```

**执行期 first-red（已授权后）**：撞上 §9.2 停止条件 → 停编码、在 §14 记 RED、回 owner。禁止在 test↔fix 循环里偷偷扩 allowlist。

**上代 over-reach**：§4 若判定上代 `PASS_LIVE` 越分母 → 必须在 §0.2 / §4.4 **撤回宣称**（不删历史 receipt）。

---

# `{LANE} 回放、{PREV_PACK} 评价与 {PACK} 限缩修复方案`

> **编号**：`{DOC_ID}`（例 `RUN-08-A9-FF03-ANALYSIS-WITH-GTZ7L-Y10`）
> **档位**：`A 单 lane | B 双臂/多源 | C 含手术刀`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`eval / attribution-and-fix-cycle`（事故闭环宿主：归因零决策；修复设计待授权；执行只追加。不是 closure / charter / planning-final / 普通 action-plan）
> **文档状态**：`draft | reviewed | frozen | superseded`
> **事故状态**：`ANALYSIS_COMPLETE | SCOPE_FROZEN | ADVERSARIALLY_REVIEWED | AUTHORIZED_FOR_LOCAL | EXECUTED_THROUGH_PREFLIGHT | NEXT_LANE_READY_NOT_STARTED | {PACK}_NOT_EXECUTED_OR_AUTHORIZED`
> **Formal root**：`{ROOT_UUID}`
> **封存 candidate**：`{DEPLOYED_SHA}`
> **分析 HEAD / harness**：`{ANALYSIS_HEAD}`（不得冒充已部署产品 epoch）
> **Session / Team**：`{SESSION_UUID}` / `{TEAM_UUID}`
> **产品终态**：`{PRODUCT_RED_AT_TURN / REASON_CODE}`
> **修复包**：`{PACK}`（例 `GTZ7l-Y10` / `GTZ7k-X18`）
> **上一代包**：`{PREV_PACK_OR_NONE}`
> **上游权威输入**：
> - `{SEALED_EVIDENCE_OR_SPECIAL_REPORT}`
> - `{FROZEN_Q_OR_TRUTH_DOC}`
> **下游消费者**：`owner 授权后的本包执行` 或 `{QNA / PLANNING_FINAL / NEXT_LANE}`
> **权限边界**：`{本轮是否新增 D1/R2/DO/provider/deploy；默认 0}`

---

## 0. 执行摘要 `[核心]`

### 0.1 一句话结论 `[核心]`

> 先写 exact 机制与首红落在哪一面，再写本包准不准动手。禁止用一个红/绿概括全篇。

`{ONE_PARAGRAPH}`

必要时钉机器裁决：

```text
{PRODUCT_RED} / {PROVIDER_GREEN_OR_RED} / {FAILURE_CLASS}
```

### 0.2 分平面 verdict `[核心·锁死]`

> **正式 verdict、机制 verdict、目标合同必须分开。** 档 B：每臂/每源各一行或分表。

| 平面 | Verdict | 说明 / 分母 |
|------|---------|-------------|
| 正式 lane | `{RED @ Txxx / NOT_SIGNED}` | immutable |
| per-turn product | `{N succeeded / N failed / N aborted}` | 不等于整 run PASS |
| provider | `{M/M completed}` | formal 与 forensic 分母分列 |
| 机制面（ASYNC/FULL/…） | `{PASS / PARTIAL / RED / NOT_OBSERVED}` | 没观察到写 `NOT_OBSERVED`，不写「没发生」 |
| harness / evidence | `{RED / PASS / INCOMPLETE}` | 产品绿不能洗掉 evaluator 红 |
| `{PREV_PACK}` | `{PASS / PARTIAL / 撤回}` | 只在其真实分母内 |
| `{PACK}` | `NOT STARTED` | 分析阶段必须保持此值 |

### 0.3 `{PACK}` 的准确边界 `[核心]`

> 用 0/不修改清单钉死。进入 §5 之后此处与 §6 禁区必须一致。

- **本包处理**：`{SEAM_1}`
- **本包明确不处理**：`{WATERLINE / PROMPT / RETRY / PREVIOUS_ARTIFACTS / …}`
- **0 修改面**：product Worker / migration / compact 算法 / … = `{0 或条件}`

---

## 1. Evidence authority、边界与完整性 `[核心·锁死]`

### 1.1 Authority 顺序 `[核心]`

本报告按以下顺序裁决（先到者覆盖后到者的叙事，不覆盖其 raw bytes）：

1. `{LANE}` operation root / opening / 逐 turn terminal
2. 已封存 provider usage map、D1/DO/R2 observation
3. `[档 C]` owner-authorized 有界补证（独立 root）
4. 当前 HEAD `file:line`（只解释机制，不改写封存事实）
5. 已冻 `Q` / truth 文档（只 CITE）

### 1.2 本轮 live / 远端操作 `[核心]`

- **本轮新增远端读写**：`none | 有界下载（root={UUID}）`
- **预算 / first-red / 禁止项**：`{ROWS_READ / NO_EXPORT / NO_RETRY / NO_WINDOW}`
- **未做**：`d1 export / SELECT * / provider probe / deploy / 时间窗口观察`

> 默认 `none`。任何 live 在第一条远端读取前必须已有独立 root。未授权却已读 → 本文不得标 `ANALYSIS_COMPLETE`。

### 1.3 身份与不可变水位 `[核心]`

| 字段 | 事实 |
|------|------|
| formal root | `{UUID}` |
| candidate / harness | `{SHA}` / `{SHA}` |
| wire / model | `{responses\|chat-completions}` / `{MODEL}` |
| 实际发送 turn | `{T001～T0xx}` |
| 水位 / pin / cap | `{H/B/S/hard}` / `{PINS}` |

### 1.4 可签 / 不可签 `[核心]`

| 主张 | 等级 | 依据 |
|------|------|------|
| `{CLAIM}` | `signed / observed-lower-bound / incomplete / not-adjudicated` | `{FILE_OR_RECEIPT}` |

---

## 2. 全量分轴回放 `[核心]`

> 不是只讲失败。没跑到的面写 `NOT_REACHED` / `CENSUS INCOMPLETE`。数字必须带分母。

### 2.1 发车前 / 配置 / 授权 `[核心]`

`{PREFLIGHT / ACTIVATION / PIN / ADMISSION}`

### 2.2 Turn 总表 `[核心]`

| turn | product terminal | provider | 备注 |
|------|------------------|----------|------|
| T001 | `{completed}` | `{N calls}` | `{NOTE}` |
| `{Txxx}` | `{aborted / failed}` | `{…}` | **first-red** |

### 2.3 首红精确取证 `[核心]`

> 时间线钉到 provider call / pump / capsule / billing join。档 C 的精确身份放这里。

`{TIMELINE_AND_JOINS}`

### 2.4 分轴回放 `[核心]`

> 至少交代：ASYNC / FULL / MICRO / T3 / billing / cache。币种不得混用（route meter ≠ provider prompt）。cache 无 owner-frozen floor → `NOT ADJUDICATED`。

| 轴 | 观察到什么 | 与首红关系 |
|----|------------|------------|
| ASYNC | `{…}` | `{cause / not-cause / census-incomplete}` |
| FULL | `{…}` | `{…}` |
| billing | `{…}` | `{…}` |
| cache | `{…}` | `{…}` |

### 2.5 `[档 B]` 多报告 / 双臂收敛

> 档 A 删除本节。把专项报告或 CC/RSP 并到**同一 denominator**，列出叙事修正。

| 源 | 原结论 | 收敛后 | 修正 |
|----|--------|--------|------|
| `{REPORT_OR_ARM}` | `{OLD}` | `{UNIFIED}` | `{AMENDMENT}` |

---

## 3. 完整因果链 `[核心·锁死]`

### 3.1 Exact causal chain `[核心]`

```text
{STEP_1}
  → {STEP_2}
  → {FIRST_RED_SURFACE}
```

每步钉 `file:line` 或封存 receipt。

### 3.2 Proven mechanism vs residual trigger `[核心]`

| 已闭合 | 未闭合 | 含义 |
|--------|--------|------|
| `{FAILURE_CLASS / INTERVAL}` | `{SINGLE_TRIGGER}` | 不得挑一个故事冒充已证事实 |

### 3.3 排除项 `[核心]`

| 排除 | 为什么不是根因 |
|------|----------------|
| `{PROVIDER_NETWORK}` | `{EVIDENCE}` |
| `{COMPACT_POLICY}` | `{EVIDENCE}` |

相邻成功面**不得洗掉**本面 RED（FULL 成功洗不掉 ASYNC RED；provider HTTP 200 写不成产品 PASS）。

### 3.4 阶段门判定 `[核心·锁死]`

```text
causal fit          = HIGH | MEDIUM | LOW
residual trigger    = CLOSED | TWO_WINDOWS_BOTH_IN_P0 | UNKNOWN
new owner Q needed  = no | yes（列题，转 qna）
fits path-cap       = yes | no（转 planning / AP）
§3.4 verdict        = GO_DESIGN | HOLD_EVIDENCE | NEED_QNA | ESCALATE_PLAN
```

- `GO_DESIGN` → 写 §5～§11
- 其它 → **删除或留空壳声明「未进入设计阶段」**，§11 handoff 指向转出文档

---

## 4. 上一代修复包评价 `[核心]`

> 无前代：写 `N/A` + 理由（本 lane 是该缝首次 RED）。有前代则必须给**真实分母**，禁止把 component canary / 单向 preflight 扩张成整链闭合。

### 4.1 `{PREV_PACK}` 的准确 denominator

`{WHAT_IT_ACTUALLY_TESTED}`

### 4.2 修对了什么 / 没有签署什么

- **正面**：`{HELD}`
- **未签**：`{NOT_SIGNED}`
- **为何本 lane preflight 没发现**：`{GAP}`

### 4.3 总体评价

`PASS 在分母内 | PARTIAL | 无效 | 撤回 over-reach`

撤回时：历史 receipt / commit **不删除、不回写**；只降级宣称。

---

## 5. `{PACK}` 修复设计 `[阶段门: §3.4 = GO_DESIGN]` `[核心]`

> 工作包，不是愿景。净新/高风险拆 a/b/c（含失败/降级）；复用既有一句话。

### 5.1 唯一目标

`{ONE_OR_TWO_SEAMS}`

### 5.2 工作包

#### `{PACK}-P0A` — `{NAME}`

- **invariant**：`{INVARIANT}`
- **落点**：`{FILE}`
- **不做**：`{NON_GOAL}`

#### `{PACK}-P0B` — `{NAME}`

`{…}`

### 5.3 明确不采用的伪修复

| 伪修复 | 为什么拒绝 |
|--------|------------|
| `{RETRY_AROUND_IT / SYNTHETIC_ZERO / USE_R2_AS_AUTHORITY}` | `{WHY}` |

### 5.4 核心 invariants（机器块）

```text
{INVARIANT_1}
{INVARIANT_2}
```

---

## 6. 精确 scope allowlist `[阶段门: 与 §5 同阶段]` `[核心·锁死]`

> 缺本段 = 本包欠规格，不得标 `SCOPE_FROZEN`。优先扩既有文件。

### 6.1 Source paths（硬上限 `{N}`）

| Path | 唯一允许目的 |
|------|----------------|
| `{path}` | `{WHY}` |

### 6.2 Test paths（硬上限 `{N}`，优先沿用）

| Path | 目的 | 来源 |
|------|------|------|
| `{test/…}` | `{WHAT}` | `🆕新增 / ♻️沿用 / 🔱fork` |

### 6.3 文档 / evidence

- 本分析 + 后续 §14
- `{OPTIONAL_FIXTURE}`
- **不修改**正式 `{LANE}` sealed artifacts

### 6.4 明确禁区

- `{WATERLINE / PROMPT / DEADLINE / ADMISSION / MIGRATION / PREVIOUS_ARTIFACTS}`

### 6.5 硬上限 + inflation verdict `[核心·锁死]`

```text
runtime semantic source paths  <= {N}
test paths                     <= {N}
new semantic migrations        = {0|1}
conditional extra source       = {0 或「每加入必须 §14 登记理由」}
remote objects / provider      = 0 during local {PACK}
```

- **causal fit**：`HIGH | …`
- **宽度定性**：`因果必要的横向宽度 | 功能扩张（禁止）`
- **scope verdict**：`PRECISE | PHASED | FAIL-CLOSED`

---

## 7. Falsifier / RED-first 矩阵 `[阶段门: 与 §5 同阶段]` `[核心·锁死]`

> 先写**当前 candidate 必红**的 exact fixture，再写修后必绿。禁止先改实现再补 RED。

| Test-ID | Plant / 验证什么 | 当前 expected | `{PACK}` exit | 映射工作项 |
|---------|------------------|---------------|---------------|------------|
| `{PACK}-T01` | `{FF03-shaped …}` | `{RED plant}` | `{VERIFIABLE}` | `{PACK}-P0A` |

分层：`短途 / spike` 为主；mega/soak 通常**不在**本包（那是 AP / 下 lane）。PASS 证据形态预填为四元组 `commit + 测试名 + （如有）D1 Q + UTC`。

---

## 8. 执行工作台账 `[阶段门: 与 §5 同阶段]` `[核心·锁死]`

### 8.1 状态合同 `[核心·锁死]`

禁止用一个 `DONE` 混 local / deployed / live。

```text
DONE_ANALYSIS     封存证据与归因已完成，不是已实现
TODO_LOCAL        只允许本地编码/测试
CONDITIONAL_LOCAL 仅当 failing fixture 证明必要时
WAIT_OWNER        deploy / preflight / live / 下一 lane
BLOCKED_SCOPE     不满足 allowlist 或 truth，回 owner
OUT_OF_SCOPE      本包明确不得做
PASS_LOCAL        本地矩阵绿，尚无 deployed truth
PASS_LIVE         独立 root + 预算 + exact readback
```

### 8.2 工作项 `[核心]`

> 不可约三元组：**落点 `file:line` 或将新建文件** + **收口目标** + **§7 Test-ID**。缺一即欠规格。

| ID | P | 工作项 | 工作内容（怎么建） | 收口目标 | Test-ID | 依赖 | State |
|----|---|---------|-------------------|----------|---------|------|-------|
| `{PACK}-E01` | P0 | `{ITEM}` | `{a/b/c 或一句}` | `{EXIT}` | `{PACK}-T01` | `{…}` | `DONE_ANALYSIS` |
| `{PACK}-P0-01` | P0 | `{ITEM}` | `{…}` | `{EXIT}` | `{PACK}-T02` | E01 | `TODO_LOCAL` |
| `{PACK}-DEP-01` | — | deploy | `{fleet readback}` | `{8/8 exact}` | — | local complete | `WAIT_OWNER` |

### 8.3 执行顺序

```text
E01..En DONE_ANALYSIS
  -> FX RED-first
  -> P0 修复
  -> gates
  -> CAND
  -> [WAIT_OWNER] DEP / PF / NEXT_LANE
```

---

## 9. 成功判据与 first-red stops `[阶段门: 与 §5 同阶段]` `[核心]`

### 9.1 成功判据（DoD = §7 全 PASS 映射）

```text
{LANE} attribution     COMPLETE / immutable
{PACK}-T01..Tn         PASS（四元组）
allowlist caps         HELD
local static/type      PASS
preview deploy         {WAIT_OWNER 或 PASS}
preflight              {WAIT_OWNER 或 PASS / provider=0}
next lane              NOT_STARTED
```

### 9.2 First-red stops

碰到即停、回 owner，**不得在循环里扩 scope**：

1. `{EXTRA_SOURCE_PATH}`
2. `{NEW_MIGRATION_OR_RETRY_LAYER}`
3. `{INTRODUCED_RED_OUTSIDE_DENOMINATOR}`
4. `{LIVE_WITHOUT_NEW_ROOT}`

---

## 10. Evidence / 源码 / git 索引 `[核心]`

| 类 | 锚 |
|----|----|
| formal evidence | `{PATH_OR_HASH}` |
| bounded supplement | `{PATH_OR_N/A}` |
| 承重 code seam | `{file:line}` |
| 当前 source SHA | `{SHA}` |
| 上代 / 相关文档 | `{LINK}` |

---

## 11. 综合 verdict 与 handoff `[核心]`

> **主体在此收束。** 分析阶段 `{PACK}` 必须仍是 `NOT STARTED / NOT AUTHORIZED`。

### 11.1 Analysis verdict

```text
{LANE} formal          = RED / immutable
mechanism              = {…}
{PREV_PACK}            = {…}
{PACK} causal fit      = {…}
{PACK} scope           = PRECISE / …
{PACK} implementation  = NOT STARTED
authorization          = NONE IN THIS DOCUMENT
```

### 11.2 对业主最重要的 1～3 条

1. `{KEY_1}`
2. `{KEY_2}`

### 11.3 Handoff

- **若 `GO_DESIGN`**：等待 owner 单独下达 `{PACK}` 编码指令；到达后从 §14 开始 append。
- **若转出**：`→ {qna / planning-final / action-plan / 档 C}`，本文不再写 §5～§10。
- **§12**：`will-run | waived（理由）`

---

# ── 附属结构（阶段门 · 授权后只追加）──

> 以下两节（§13 / §14）及 §12 的「授权后增补」**不是分析原貌的一部分**。
> - **§12**：授权前可写、并可回改 §5～§10；授权后冻结，再审实现走 `code-review` 或写入 §14。
> - **§13 / §14**：只 append。凡与 §0～§11 状态字段冲突，**以本节实际 receipt 为准**，不回写主体。

---

## 12. 对抗式审查与修订记录 `[阶段门: S2 初稿之后、owner 授权之前]` `[可选·授权前强烈建议]`

> 读-only 审查。攻击面至少覆盖：分母混写、币种冒充、因果唯一性、allowlist 膨胀、上代甩锅。
> HIGH 必须在授权前吸收进 §5～§10。跳过则在 §11.3 写 `waived` + 理由。

- **审查身份**：`{REVIEWER_OR_SUBAGENT}` · **终态**：`{N HIGH + M MED / OPEN HIGH = 0}`

| Finding | 攻击 | 处置 | 正文修订 |
|---------|------|------|----------|
| H1 | `{ATTACK}` | `ACCEPT / REJECT` | `{§x 改了什么}` |

授权之后若需再审实现：不要改本节冒充「计划审查 = 实现审查」；实现审查写入 §14 或独立 `code-review`。

---

## 13. 有界 live 补证 `[阶段门: owner 另授 live 且主体已过 S1]` `[可选 · append-only]`

> 仅当补证授权来得**晚于** §1/§2 定稿时启用。补证只**抬归因等级**，不把原 formal RED 改写成 PASS。
> 若补证发生在开写之时，不要用本节，直接写入 §1.2 / §2.3。

> **执行者**：`{WHO}` · **时间**：`{DATE}` · **补证 root**：`{UUID}` · **预算**：`{R/W/RETURNED}`

- **补了什么身份**：`{EXACT_JOIN}`
- **对 §3 的影响**：`抬级 / 确认 / 仍未闭合 trigger`（不回写 §3 原文）
- **是否触发重新设计**：`no | 需 owner 重看 §5`（重看 ≠ 偷偷改主体）

---

## 14. 执行日志回填 `[阶段门: owner 已授权执行]` `[append-only]`

> **挂载**：本节是 [`code-execution-log`](./code-execution-log.md) 在本模板上的宿主位（对应该模板的「厚版 §9」）。
> **谁写 / 何时**：执行者本人在进入 `AUTHORIZED_FOR_LOCAL` 之后开始 append；未授权则整节删除。
> **回链**：每一行必须对应 §8 台账 ID（`{PACK}-P0-01`），不许写「做了一些」。
> **多轮**：保留本节历史，追加 `### 14.B` / dated block，不改已写行。

> **执行者**：`{EXECUTOR}`
> **执行时间**：`{DATE}`
> **事故状态**：`{AUTHORIZED_FOR_LOCAL → EXECUTED_THROUGH_PREFLIGHT / …}`
> **产品 candidate**：`{SHA}`
> **代码改动统计**：`{N files / +X -Y / migrations}`

- **实际执行摘要**：`{对照 §8 ID}`
- **Phase 偏差（计划 vs 实际）**：`{逐条分类}`
- **阻塞与处理**：`{…}`
- **测试发现**：`{全绿计数 + 新暴露事实}`
- **后续 handoff**：`下一 lane = READY_NOT_STARTED`（不得自动发车）

### 14.1 逐工作项状态

| 工作项 | 状态 | Commit / root | 实际落点 | 备注 |
|--------|------|---------------|----------|------|
| `{PACK}-E01` | `✅ done` | `{sha}` | `{file:line}` | `{NOTE}` |
| `{PACK}-R05` | `❌ OOS handoff` | `—` | `—` | `{SUCCESSOR}` |

> 状态：`✅ done | 🟩 partial | ⚠️ env-blocked | ❌ OOS handoff`

### 14.2 关键指标演进

| 指标 | 执行前 | 执行后 | Δ / verdict |
|------|--------|--------|-------------|
| planted matrix | `{32/5 fail}` | `{97/97}` | `{…}` |
| source cap | `{plan N}` | `{actual}` | `cap held` |

### 14.3 时序执行日志

| 时点 | 步骤 | 决策 / 产出 |
|------|------|-------------|
| `T0` | RED-first | `{pre-fix expected RED}` |
| `T1` | `{FIX}` | `{…}` |

### 14.4 关键决策日志

#### Decision-1 — `{TITLE}`

- **背景**：`{…}` · **决议**：`{…}` · **理由**：`{…}` · **代价**：`{…}`

### 14.5 真实命令与 receipt 索引

`{COMMAND + ROOT + RECEIPT PATH}`

### 14.6 pre-existing 失败甩锅

| 失败项 | git / 命令证据 | 判断 |
|--------|----------------|------|
| `{OG-08 633/636}` | `{sha 先于 candidate}` | `pre-existing, non-blocking` |

### 14.7 文档状态与 handoff

`SCOPE_FROZEN → AUTHORIZED_FOR_LOCAL → EXECUTED_THROUGH_{GATE}（{DATE}）`。  
residual → `{successor pack / AP / qna}`，**不回填进本包归因**。  
下一正式 lane：`NOT_STARTED`。

---

## 附录 A · 阶段 × 段落速查

| 段 | S1 归因 | S2 设计 | S3 对抗 | S4 执行 | 备注 |
|----|---------|---------|---------|---------|------|
| 头部 / §0～§4 | **必填** | 只读 | 只读 | 只读 | machine RED 永不改 |
| §2.5 | 档 B 必填 | 只读 | 只读 | 只读 | 档 A 删除 |
| §5～§11 | 禁写（除非 GO_DESIGN 当轮连写） | **必填** | 授权前可改 | 只读 | 缺 allowlist/falsifier/台账 = 欠规格 |
| §12 | — | — | **必填或 waived** | 只读 | 实现再审不写这里 |
| §13 | 早补证走 §1/§2 | — | — | 可 append | 不得倒写正式 RED |
| §14 | 删除 | 删除 | 删除 | **必填** | `code-execution-log` 合同 |

## 附录 B · 命名与转出

- **落盘名**：`{GATE}-{LANE}-analysis-with-{PACK}.md`  
  例：`RUN-08-A9-FF03-analysis-with-GTZ7l-Y10.md`
- **包 ID**：沿用系列字母 + 序号（`X18` / `Y10`），不要在同一 lane 上新开字母。
- **转出后本文角色**：只作归因真源；下游 AP / qna **CITE 本文 §3 / §0.2**，不复制全文。

## 附录 C · 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（归因 / 设计 / 未授权） |
