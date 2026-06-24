# Assessment 模板簇（truth 子簇）· per-cluster-value-proposition —— 簇级真值汇总 / 价值承诺

> **模板簇**：`assessment / truth`（真值奠基子簇——本文是把同簇 N 份逐域真相**上卷成给消费者（通常=前端）的「能建 / 围栏建 / 勿建」三态承诺台账**；它**不**重新勘察代码，只**汇总 + 裁定 + 翻译成可消费的 readiness 准绳**，证据一律回引各域 analysis）。
> **簇内成员（统一血统 · 三模板互证）**：[[truth/assessment-index]]（站① 编排器 + 判据 SSOT）+ [[truth/per-domain-analysis]]（站② 单域深勘）+ `per-cluster-value-proposition`（本文，**站③ 簇级上卷**）。
>
> **一句话用途**：一簇 `{M}` 个域全 attested 后，把它们的逐能力 T 层**上卷成三态价值台账**（🟢 能承诺 / 🟡 部分承诺 / 🔴 不能承诺），汇 GAP（P0-P2），并回答 owner 的终极一问——**「`{CONSUMER}` 今天能在本簇上建什么、必须围栏什么、绝不能据什么建」**，作下游 readiness 基线。
> **何时用**：[[truth/assessment-index]] 的某一簇下 `{M}` 域已全产 attested [[truth/per-domain-analysis]]、需要给前端一张**可直接消费的承诺地图 + verdict** 时；每簇产一份。
> **何时不用**：① 单域真相还没勘完 → 先补 [[truth/per-domain-analysis]]；② 还在切域 / 派活 → [[truth/assessment-index]]；③ 「建什么 / 能借什么」式 planning 前奏 → 顶层 `assessment-index`（另一簇）。
>
> **调查纪律（truth 簇共有脊 · 三模板一致 · 详见 [[truth/assessment-index]] §3）**：
> 1. **measure-first / 证据回引**：本文每条承诺**回引**某域 analysis 的 `file:line` / evidence（不另测、不放宽该域的 T 层裁定）。
> 2. **反假绿（灵魂）**：被各域抓的假绿 / 孤儿幻影**必进 🔴 表并点名**；上卷**不得**把 🔴/🟡 悄悄抬成 🟢。
> 3. **trust-code 亲验**：簇级承重订正经主进程亲验（附录留痕）；禁据二手。
> 4. **degraded≠green**：🟢 仅给 T1 或「强 T2 + mega live 间接背书」；离线绿独存 → 🟡。
> 5. **read-only-first**：纯汇总，零产品改。
> 6. **判据引用**：T1-T4（[[truth/assessment-index]] §2.1）、reopen 触发器纪律（同 §2.2 ⑥）引用不复制。
>
> **状态词汇（本簇自有）**：`draft rollup`（汇总中）→ `reviewed`（4-agent 复核 fleet + 亲验过）→ `frozen`（三态台账 + GAP + verdict 锁定，作前端 readiness 基线）→ `superseded`。
> **占位符约定**：`{UPPER_SNAKE}` backtick 包裹；`[核心]` 必填 / `[可选]` 视簇删除。
> **流水线位置**：本文 = **站③** · 上游 = `{M}` 份 [[truth/per-domain-analysis]]（本簇各域）· 下游 = `{CONSUMER}` readiness 准绳（对接 `{API_ADAPTER_INVENTORY_PATH}`）+ verdict 回填 [[truth/assessment-index]] §7。

---

# 簇 `{C}` · `{CLUSTER_NAME}` —— 簇级真值汇总 sub-index

> **项目**：`{PROJECT_NAME}`
> **本簇含域**：`{D_NN, D_MM, …}`（`{M}` 域，全 attested）
> **日期**：`{DATE}` · **作者**：`{AUTHOR}`（fleet：`{AGENTS_OR_NONE}`）
> **文档性质**：`assessment / truth-cluster`（簇级 measure-first 上卷 + 三态价值承诺；零决策）
> **文档状态**：`draft rollup | reviewed | frozen | superseded`
> **流水线位置**：站③ · 上游 = `{M}` 份 [[truth/per-domain-analysis]]
> **当前工作树锚**：`{HEAD_OR_DEPLOY_PIN}`（承诺对此树成立；如有 source-diff 证零变更，给锚）

---

## 1. 本簇的核心业务说明 `[核心]`

`{WHAT_THIS_CLUSTER_DOES_AS_A_WHOLE — 它在系统里承担的整体职责，一句话真值形状}`

---

## 2. 本簇的构建清单（构成锚）`[核心]`

> 把本簇「由什么构成」一次列清，作下文台账的锚池。

- **2.1 对外路由面**（消费者唯一入口）：`{ROUTES + ANCHORS}`
- **2.2 控制面 / 写者 / 引擎**：`{WRITERS_ENGINES + ANCHORS}`
- **2.3 D1 / DO schema（簇相关）**：`{TABLES + ANCHORS}`
- **2.4 测试体系（三层）**：`{UNIT/SPIKE/MEGA + ANCHORS}`

---

## 3. 当前已经可以承诺的价值台账（🟢 T1 / 强 T2-with-live —— `{CONSUMER}` 可信建）`[核心]`

> 判据：live evidence JSON 逐字段亲验（T1），或离线 gate-green 且有 mega live 间接背书（强 T2）。**对当前工作树成立**。

| # | 能力 | 域 | T 层 | 证据 / 锚 |
|---|---|---|---|---|
| `C-1` | `{CAPABILITY}` | `D{NN}` | `🟢 T1 / 强 T2` | `{EVIDENCE_BACK_REF — 域 analysis §x + evidence/...json}` |

---

## 4. 当前部分承诺的价值台账（🟡 T2 —— 离线绿 / 逻辑对，live 未独立重证；功能在线但有缺口）`[核心]`

> 判据：实现完整且接线，离线 gate-green（部分带 falsify 镜像），但 **live 线缆未重跑**（spike 0/0 stale）或有诚实的功能 / 观测缺口。`{CONSUMER}` 可建，但**须知缺口**。

| # | 能力 | 域 | T 层 | 缺口 / 一句话 |
|---|---|---|---|---|
| `P-1` | `{CAPABILITY}` | `D{NN}` | `🟡 T2` | `{GAP_ONE_LINE + 指向 §5 / §6 编号}` |

---

## 5. 当前不能承诺的价值台账（🔴 T3 降级 / T4 假绿 / 占位 / 孤儿 —— `{CONSUMER}` 必须围栏或勿建）`[核心]`

> 判据：诚实空壳（executor noop）、被抓假绿（T4，已订正或待订正）、observe-only / best-effort 降级、孤儿 / 幻影 adapter。`{CONSUMER}` **不得**呈现为「可用」或据此建。

| # | 能力 | 域 | T 层 | 真相 / 围栏 |
|---|---|---|---|---|
| `N-1` | `{CAPABILITY}` | `D{NN}` | `🔴 T3 / T4` | `{TRUTH + REQUIRED_FENCE + ANCHOR}` |

---

## 6. GAP 汇总（P0–P2 分类）`[核心]`

> P0 = 阻断 `{CONSUMER}` / 最紧急围栏（用户会撞到，或会误信假绿）；P1 = 应补的纵深 / 观测 / 测试兑现；P2 = 卫生 / 债 / 元缺口。每条带触发 charter + 锚。

### P0（阻断 / 最紧急）
| GAP | 域 | 说明 | 锚 / charter |
|---|---|---|---|
| `G-P0-1` | `D{NN}` | `{BLOCKING_GAP}` | `{ANCHOR}`（对应 §5 N-x）|

### P1（纵深 / 观测 / 测试兑现）
| GAP | 域 | 说明 | 锚 |
|---|---|---|---|
| `G-P1-1` | `D{NN}` | `{DEPTH_GAP}` | `{ANCHOR}` |

### P2（卫生 / 债 / 元缺口）
| GAP | 域 | 说明 | 锚 |
|---|---|---|---|
| `G-P2-1` | `D{NN}` | `{HYGIENE_GAP}` | `{ANCHOR}` |

### 复核 fleet 已修订项（留痕）`[可选]`
> 4-agent 复核 + 主进程亲验对本簇各域报告的订正（read-only on 产品；仅改 truth 报告 + 索引）：
- **[实质] `{域}`**：`{OVER_CLAIM → 订正}`（亲验锚）。
- **[refuted 子claim] `{域}`**：`{原记 → 实为 → 订正}`。
- **复核未发现**：`{0 refuted headline / 0 dead-anchor / 0 报告自身假绿 / 跨域 0 架构矛盾 — 列已对齐的不变量}`。

---

## 7. 本簇对 `{CONSUMER}` 的意义，以及应该利用的方法 `[核心]`

### 7.1 意义：`{CONSUMER}` 今天能站在什么上
`{ONE_LINE_TRUTH_SHAPE — 如「热路径真、mutation 半真、X 空壳、观测 best-effort」}`。体验质量取决于是否尊重这几层。

### 7.2 应利用的方法（按域 / 按能力分组）
**① `{主流程簇}`（建在 `C-x/C-y` 上，可信）**
- `{HOW_TO_USE + 必走的耐久对账 / 兜底纪律}`

**② `{半真簇}`（建在 `C-z/P-x` 上，半真）**
- `{HOW_TO_USE + 勿建什么 UI（因后端缺口）}`

**③ `{围栏簇}`（涉及 `N-x`，必围栏）**
- `{WHAT_TO_DISABLE_OR_LABEL_EXPERIMENTAL}`

### 7.3 `{CONSUMER}` readiness 准绳 `[可选]`
`{HOW_THIS_MAPS_TO_API_ADAPTER_INVENTORY — 哪些标 live / planned / 必须降级或删孤儿}`

---

## 8. 最终 verdict `[核心]`

**`{🟢 go / 🟡 go-with-fence / 🔴 go-with-heavy-fence / blocked}`** —— `{ONE_PARAGRAPH — 本簇核心是否诚实可用 + owner 最关心的几件事各自真相}`。

1. `{KEY_TRUTH_1}`
2. `{KEY_TRUTH_2}`

**对 `{CONSUMER}` 的含义**：`{WHAT_FE_CAN_AND_CANNOT_RELY_ON}`。

---

## 附录 · 复核方法与锚

```text
# {K}-agent 复核 fleet（read-only，对 {M} 份域报告独立 re-verify + trust-code 亲验）：
#   {FLEET_AXIS_SPLIT — 如 R1 D{NN} claim re-verify · R2 … · R_last 跨报告一致性+诚信+FE+死锚}
# 主进程亲验的承重订正锚：
{LOAD_BEARING_CORRECTION_ANCHORS}
```

## 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初版（三态价值台账 + GAP P0-P2 + 对 `{CONSUMER}` 意义 + verdict） |
