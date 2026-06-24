# Assessment 模板簇（truth 子簇）· index —— 真值奠基总纲领 + N 域评估索引 / 编排器

> **模板簇**：`assessment / truth`（**真值奠基子簇**——独立于顶层 `assessment-index` / `assessment-analysis`[design-prelude 风味，进 planning 前的前置研究]，二者**无血缘、不可混用**；本子簇关心「**已有系统的真相到底是什么、哪些真能用、哪些是构造假绿**」，不关心「要建什么 / 能借什么」）。
> **簇内成员（统一血统 · 三模板互证）**：`assessment-index`（本文，**站① 编排器**）+ [[truth/per-domain-analysis]]（**站② 单域深勘**，sub-agent 产物）+ [[truth/per-cluster-value-proposition]]（**站③ 簇级价值上卷**，给前端的承诺台账）。
>
> **一句话用途**：一次「系统真相奠基 campaign」的开场——立**统一判据**（T1-T4 真值分层 + 逐域 7 点 rubric + 反假绿红线），把待查系统切成 `{N}` 个域并各立锚定入口，**派 read-only sub-agent 逐域深勘**，verdict 回填 Living Tracker。**本文是全簇判据 / 分母 / 红线的单一真源（SSOT）**——另两份模板引用本文 §2/§3，不复制。
> **何时用**：owner 抛出「不知道真值层、不知道哪些接口真能用 / 哪些是构造假绿跑出来的」式**校准危机**，需对一个多域系统逐域摸清真实情况、产出**前端 readiness 准绳**时。
> **何时不用**：① 只有单一调查面、无需 campaign 编排 → 直接写一份 [[truth/per-domain-analysis]]；② 进入「建什么 / 怎么落地 / 借鉴矩阵 / 净新契约」式 planning 前奏 → 用**顶层** `assessment-index`（design-prelude，另一簇）；③ 已在排「怎么做 / 何序 / 怎么测」执行序 → 下游执行计划制品。
>
> **调查纪律（truth 簇共有脊 · 三模板一致）**：
> 1. **measure-first 红线**：一切「现状 / 能用」以 **HEAD 实测**为准，每条带 `file:line` + 可复现命令**或** evidence 路径；**先证可证性，再下判断**。
> 2. **反假绿（本簇灵魂）**：发现假绿（假断言 / warn 当 pass / describe-污染式 / vacuous gate / 孤儿幻影 adapter）→ **必点名 + reverse-water 留痕**；**禁为「看起来绿」放水**。
> 3. **trust-code 亲验**：每条真值层裁定**逐源码 / 逐 evidence 帧**核对；**禁据二手 closure 措辞**（母体报告本身亦是待核的二手）。
> 4. **degraded≠green / honest-segmentation**：「离线 gate 全绿」永远 ≠「live 真绿」；live / owner-gated 段不可冒充 T1；未跑标 T2/T3，**绝不 silent 标 T1**。
> 5. **read-only-first + sub-agent 安全**：评估纯只读（代码审查 + 既有 evidence 复核）；**任何产品源 / migration / schema / fixture 改动须 owner-gate**，发现真 bug → **STOP + surface**（新 charter），不就地改；**禁 sub-agent 对共享未提交态做 git checkout/stash/reset/commit**，主进程亲验汇总。
> 6. **判据 SSOT**：T1-T4 分层框架（§2.1）+ 逐域 7 点 rubric（§2.2）+ 红线（§3）**只在本文定义一次**；[[truth/per-domain-analysis]] 与 [[truth/per-cluster-value-proposition]] **引用**本文章节号，不另立。
>
> **状态词汇（本簇自有）**：`active campaign`（评估进行，Living Tracker 滚动）→ `closed`（全域闭合 + verdict 全回填 + 复核 fleet 过）→ `superseded`（被新一轮 campaign 取代）。
> **占位符约定**：统一 `{UPPER_SNAKE}`，backtick 包裹。`[核心]` = 必填段；`[可选]` = 视 campaign 删除。
> **流水线位置**：本文 = **站①**（立判据 + 切域 + 派活 + 追踪）→ 站② = `{N}` 份 [[truth/per-domain-analysis]] → 站③ = `{C}` 份 [[truth/per-cluster-value-proposition]] → verdict 回填本文 §7。

---

# `{CAMPAIGN_NAME}` 真值奠基 —— 总纲领 + `{N}` 域评估索引（Truth Assessment Index）

> **项目**：`{PROJECT_NAME}`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（fleet / panel：`{AGENTS_OR_NONE}`）
> **文档性质**：`assessment / truth-index`（campaign 编排器 + 判据 SSOT；**零决策**——owner 拍板点列 owner-gate 候选，交决策登记）
> **文档状态**：`active campaign | closed | superseded`
> **流水线位置**：站① · 下游 = [[truth/per-domain-analysis]]（站②）→ [[truth/per-cluster-value-proposition]]（站③）
> **上游输入**：`{MOTHER_REPORT_OR_NONE}`（母体初判来源，全部待证伪）· `{OWNER_CALIBRATION_QUOTE}`（校准危机原话）
> **对外唯一入口锚**：`{CANONICAL_FACADE_OR_ENTRYPOINT}`（如对外路由面单一入口）

---

## 0. TL;DR（总览先行）`[核心]`

- **一句话**：`{ONE_LINE_WHY_AND_WHAT}`——对 `{SYSTEM}` 的 `{N}` 域逐一摸清真值层，使每句「这个能用」都有 `file:line` + live 证据**或**诚实降级背书。
- **产出**：`{N}` 份 [[truth/per-domain-analysis]] + `{C}` 份 [[truth/per-cluster-value-proposition]] + 本索引统一结论 = 一组**新的认知核心**，作 `{CONSUMER}`（通常=前端）推进的 readiness 准绳。
- **当前进度**：见 §7 Living Tracker（`{DONE}/{N}` 域闭合）。

---

## 1. 任务纲领（为什么做这件事）`[核心]`

- **校准危机（owner 原话锚定）**：`{OWNER_QUOTE}`（如「不知道真值、连真值层都不稳固」「不知道哪些接口真能用、哪些是假的、哪些是构造假绿跑出来的」）。→ 在此之前任何「继续推进」都是空中楼阁。
- **奠基目标**：对 `{N}` 域**逐一摸清真实情况**，产出一组可信认知核心。
- **成功判据**：campaign 结束时，owner 能对任一域回答三问——(a) 它**真能跑到什么程度**（真值层）？(b) `{CONSUMER}` 今天能在它上面**建什么**？(c) 它有没有**未订正的假绿 / 被掩盖的缺口**？

---

## 2. 方法与判据（对 `{N}` 域统一生效）★ SSOT `[核心]`

> 本节是全簇判据真源。每份 [[truth/per-domain-analysis]] / [[truth/per-cluster-value-proposition]] **引用此处章节号**（如「按 index §2.2 7 点」「按 index §2.1 T 层」），不复制、不另立词表。

### 2.1 真值分层框架（每域逐能力打层）

| 层 | 标记 | 定义 | 可信度 |
|---|---|---|---|
| **T1 真·live-proven** | 🟢live | 部署 preview 上 real-LLM / real-D1 实跑 + evidence JSON / live 断言逐字段亲验 | 最高：真能跑 |
| **T2 离线 gate-green** | 🟡off | gate/test 绿，但未 live 重跑（或仅 short-verified） | 中：逻辑对、未现场验 |
| **T3 诚实降级 / deferred** | 🟠def | 公开标 owner-gated / 真 provider 待建 / 能力缺 / best-effort 降级 | 已知不可用、有围栏 |
| **T4 被抓的假绿** | 🔴fix | 曾声称绿、被证伪、已订正（或新发现待订正） | 已修 / 待修；**必留痕** |

### 2.2 逐域 7 点 rubric（每份 analysis 必答，保证 `{N}` 域可比）

1. **构成（composition）**：本域由哪些对外路由（`file:line`）/ 哪些 worker·RPC / 哪些 D1 表·DO storage 组成。
2. **数据真相（persistence truth）**：durable 落点、写者唯一性、状态机、跨租户作用域。
3. **真值层裁定（truth-layer verdict）**：逐能力打 T1/T2/T3/T4，每条给 live 证据**或**诚实缺口（§9.1 热力图）。
4. **假绿审计（fake-green / theater audit）**：本域 test/gate 是真牙齿还是 warn-only / vacuous / theater？有无 describe-污染式假绿？有无被掩盖的下游误诊？
5. **前端可达性（FE reachability）**：哪些路由 FE 可达、readiness 几何、`{CONSUMER}` 今天能建什么（对接 `{API_ADAPTER_INVENTORY_PATH}` 的 readiness 纪律）。
6. **缺口 / deferred / blocker**：逐条带 **reopen 触发器**；标明是否阻断 `{CONSUMER}`。
7. **裁定（verdict）**：`{CONSUMER}` 今天能否在本域建？`go / go-with-fence / blocked` + 置信度 + 一句话。

### 2.3 证据口径

- **可采信判据**：`file:line` 命中（可独立复核）= 代码事实；`evidence JSON / live 断言` = T1；`gate/test 绿但未 live` = T2；外部声称落一手文档。
- **trust-code 亲验**：见共有脊 §3——禁据二手 closure 措辞。
- **诚实分段**：live 段未跑就标 T2/T3，**绝不 silent 标 T1**；`degraded≠green`。

---

## 3. 约束 / 红线（NORMATIVE，对 `{N}` 域统一生效）`[核心]`

> 即头部共有脊的 NORMATIVE 展开。每域 analysis 默认继承，违背须显式 MARK 并交 owner。

1. **read-only-first**：评估阶段纯只读。产品源 / migration / schema / fixture 改须 owner-gate；真 bug → STOP + surface。
2. **反假绿（本 campaign 灵魂）**：假绿必点名 + reverse-water 留痕；禁放水。
3. **degraded≠green / honest-segmentation**：离线绿 ≠ live 绿；母体初判被证伪 → 以本域 analysis 为准并回填订正。
4. **锚点纪律**：每条结论带 `file:line` 或 evidence 路径；死锚 / 陈旧锚必须订正。
5. **sub-agent 安全**：逐域可派 read-only sub-agent；禁对共享未提交态做 git 写操作；主进程亲验汇总。
6. **交付格式**：每域产 `{DOMAINS_DIR}/D{NN}-{slug}.md`，按 §2.2 7 点 rubric + [[truth/per-domain-analysis]] 骨架；verdict 回填本索引 §7；簇级上卷产 [[truth/per-cluster-value-proposition]]。
7. **commit 待 owner（如适用）**：`{COMMIT_POLICY}`（如本索引 + 各域 analysis 均 owner 自提交，no Claude trailer）。

---

## 4. `{N}` 域评估索引（★ 本文核心 · 每域一锚定入口）`[核心]`

> 每域给：**定位（构成锚）· 当前真值层（母体初判，待核）· 已知 live 证据 / 假绿风险 · 评估目标 · 关键问题 · 交付物 · 状态**。当前真值层均为**母体快照初判**，本域 code-review 须证实 / 证伪 / 精修。路由锚来自 `{ROUTES_DIR}`。

---

### 簇 `{C}` · `{CLUSTER_NAME}`（`{CLUSTER_ROLE_ONE_LINE}`）

> 簇级上卷 → [[truth/per-cluster-value-proposition]]（`{CLUSTER_VALUE_DOC_PATH}`）

#### D`{NN}` — `{DOMAIN_NAME}`

- **定位 / 构成锚**：`{WHAT_THIS_DOMAIN_IS + KEY_FILE_LINE}`
- **当前真值层（母体初判，待核）**：`{🟢/🟡/🟠/🔴 + ONE_LINE}`
- **已知 live 证据 / 假绿风险**：`{EVIDENCE_OR_FAKE_GREEN_RISK}`
- **评估目标**：`{WHAT_THIS_ASSESSMENT_MUST_RESOLVE}`
- **关键问题**：`{KEY_QUESTIONS}`
- **交付物**：`{DOMAINS_DIR}/D{NN}-{slug}.md`（[[truth/per-domain-analysis]]）
- **状态**：`{未启 | 进行 | draft | cross-reviewed | attested}`

`{REPEAT_PER_DOMAIN_PER_CLUSTER}`

---

## 5. 研究计划 / DAG（建议排序 —— owner 裁）`[核心]`

> 给关键路径 + 并行窗；标哪些域可并行派 sub-agent、哪些需先行（共享地基）。

```text
{DAG_ASCII — 簇/域的依赖序与并行窗}
```

- **建议批次**：`{BATCH_1 (并行) → BATCH_2 → …}`
- **owner 裁定点**：`{ORDERING_DECISION_IF_ANY}`

---

## 6. 完成判据 / 终点（Endpoint —— 全闭合后回填）`[核心]`

- **campaign DONE 当且仅当**：(a) `{N}` 域全产 attested analysis；(b) `{C}` 簇全产 frozen value-proposition；(c) 复核 fleet（每域一名以证伪为目标的 verifier）过、0 refuted headline；(d) 本索引 §7 全回填 + reverse-water 全留痕。
- **交接下游**：`{HANDOFF — 前端 readiness 准绳 / 下游 eval / charter}`。

---

## 7. 状态总表（Living Tracker —— 每域完成即回填）`[核心]`

| 域 | 簇 | 母体初判 | 实测 verdict | headline T 层 | reverse-water? | 状态 | analysis 锚 |
|---|---|---|---|---|---|---|---|
| `D{NN}` | `{C}` | `{母体快照}` | `{go / go-with-fence / blocked}` | `{🟢/🟡/🟠/🔴}` | `{有/无 + 一句话}` | `{draft/cross-reviewed/attested}` | `{DOMAINS_DIR}/D{NN}-...md` |

---

## 8. 后续使用方式（流水线指引）`[可选]`

- **派活**：让 sub-agent 读本文 §2/§3 + 领一个 §4 域，按 [[truth/per-domain-analysis]] 骨架深勘；**独立纪律**（仅用自己的 reasoning，不参考其它 sub-agent）。
- **上卷**：一簇 N 域 attested 后，按 [[truth/per-cluster-value-proposition]] 上卷为三态价值台账。
- **复核**：簇级派 4-agent 对抗 fleet（每域一名 verifier）+ 主进程亲验。

---

## 附录 A · 复现 / 锚点

```bash
{REPRO_COMMANDS — 母体报告锚 / 路由锚 / live 证据目录 / 交付物目录}
```

## 附录 B · 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初版（纲领 + 判据 SSOT + `{N}` 域索引 + DAG + Living Tracker） |
