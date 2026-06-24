# Assessment 模板簇（truth 子簇）· per-domain-analysis —— 单域真相深度勘察

> **模板簇**：`assessment / truth`（真值奠基子簇——与顶层 `assessment-analysis`[design-prelude 单面深评] **无血缘、不可混用**；本文做的是「**这个域的真值层到底是什么、哪些真能用、哪些是假绿**」的 measure-first 勘察，**不**做「能借什么 / 净新契约 / 验收格栅」）。
> **簇内成员（统一血统 · 三模板互证）**：[[truth/assessment-index]]（站① 编排器 + 判据 SSOT）+ `per-domain-analysis`（本文，**站② 单域深勘**）+ [[truth/per-cluster-value-proposition]]（站③ 簇级上卷）。
>
> **一句话用途**：对 [[truth/assessment-index]] 切出的**一个域**做一次 read-only、measure-first、code-anchored 的真相勘察——把现状测准、逐能力打 T1-T4、审计假绿、查 FE 可达性、编号缺口台账、用代码 reverse-water 证伪母体过度声称，**产一份可独立复核的逐域真值报告**，喂站③上卷与下游 readiness。
> **何时用**：[[truth/assessment-index]] 已立判据（§2）并在 §4 给本域一个锚定入口、开始派 sub-agent 逐域深勘时；每个域产一份。
> **何时不用**：① 还在编排「有哪些域、谁先谁后」→ [[truth/assessment-index]]；② 一簇 N 域已 attested、要上卷成给前端的承诺台账 → [[truth/per-cluster-value-proposition]]；③ 「建什么 / 能借什么」式 planning 前奏 → 顶层 `assessment-analysis`（另一簇）。
>
> **调查纪律（truth 簇共有脊 · 三模板一致 · 详见 [[truth/assessment-index]] §3）**：
> 1. **measure-first**：一切「现状 / 能用」以 HEAD 实测为准，每条带 `file:line` + 可复现命令**或** evidence 路径。
> 2. **反假绿（灵魂）**：假绿（假断言 / warn 当 pass / describe-污染 / vacuous gate / 孤儿幻影 adapter）必点名 + reverse-water 留痕（§9.2）。
> 3. **trust-code 亲验**：每条 T 层裁定逐源码 / 逐 evidence 帧核对；禁据二手 closure 措辞。
> 4. **degraded≠green**：离线绿 ≠ live 绿；未跑标 T2/T3，绝不 silent 标 T1。
> 5. **read-only-first + sub-agent 安全**：纯只读；产品源 / migration / schema 改须 owner-gate，真 bug → STOP + surface；禁对共享未提交态 git 写。
> 6. **判据引用**：T1-T4（[[truth/assessment-index]] §2.1）、7 点 rubric（同 §2.2）、红线（同 §3）**引用不复制**。
>
> **★ 7 点 rubric 覆盖核对（必全覆盖，见 [[truth/assessment-index]] §2.2）**：①构成→§2/§3 · ②数据真相→§3/§4a/§4b/§8 · ③真值层裁定→§9.1 · ④假绿审计→§4b/§7a/§7b · ⑤FE 可达性→§6 · ⑥缺口/deferred/blocker→§5/§9.3 · ⑦verdict→§9.4。
> **状态词汇（本簇自有）**：`draft`（sub-agent 初稿）→ `cross-reviewed`（复核 fleet 独立 re-verify 过）→ `attested`（主进程 trust-code 亲验，作站③上卷源）→ `superseded`。
> **占位符约定**：`{UPPER_SNAKE}` backtick 包裹；`[核心]` 必填 / `[可选]` 视域删除。
> **流水线位置**：本文 = **站②** · 上游 = [[truth/assessment-index]]（领一个域 + 继承 §2 判据）· 下游 = [[truth/per-cluster-value-proposition]]（被上卷）+ verdict 回填 index §7 Living Tracker。

---

# D`{NN}` — `{DOMAIN_NAME}`（真值奠基逐域评估）

> **项目**：`{PROJECT_NAME}`
> **域 scope-fence**：本文覆盖 `{WHAT_THIS_DOMAIN_COVERS}`；**本域不含**：`{EXPLICIT_OUT_OF_DOMAIN}`（交由 D`{OTHER_NN}`）。
> **日期**：`{DATE}` · **作者**：`{AUTHOR}`（sub-agent / fleet：`{AGENTS_OR_NONE}`）
> **文档性质**：`assessment / truth-domain`（单域 measure-first 真相勘察；零决策——owner 拍板点列 §9.3 并 MARK）
> **文档状态**：`draft | cross-reviewed | attested | superseded`
> **流水线位置**：站② · 上游 = [[truth/assessment-index]] §2（判据）+ §4 本域入口
> **上游权威输入**：[[truth/assessment-index]]（§2 判据 / §3 红线 / §4 本域母体初判）· `{MOTHER_REPORT_ANCHOR}`（待证伪）

---

## 0. TL;DR（先行结论）`[核心]`

- **headline T 层**：`{🟢/🟡/🟠/🔴 + 最关键能力一句话}`
- **一句话 verdict**：`{go / go-with-fence / blocked + ONE_LINE}`（详 §9.4）
- **最紧急围栏 / blocker**：`{TOP_FENCE_OR_NONE}`

---

## 1. 调查目标主体的介绍，调查的原因 `[核心]`

### 1.1 什么是「`{DOMAIN_NAME}`」
`{PLAIN_LANGUAGE_WHAT_THIS_DOMAIN_DOES}`

### 1.2 为什么调查（调查的原因）
`{WHY — 母体初判存疑 / 假绿风险 / FE 依赖 / owner 点名}`

### 1.3 本域要回答的关键问题（答案见对应节）
- `{Q1}` → §`{x}`
- `{Q2}` → §`{y}`

---

## 2. 主要负责的 worker 以及目标在系统中的价值地位 `[核心]`  ｜ rubric ①构成

### 2.x Worker `{X}` — `{WORKER_NAME}`（`{ROLE}`）
`{WHAT_IT_OWNS + KEY_FILE_LINE}`

### 2.y 本域的价值地位
`{WHY_THIS_DOMAIN_MATTERS_TO_CONSUMER}`

---

## 3. 目标的主体逻辑结构的树状代码依赖结构 `[核心]`  ｜ rubric ①构成 ②数据真相

> 主调用路径（带 `file:line`）、状态转移表、状态机、子系统。**先把「请求如何穿过系统」画清。**

### 3.1 主调用路径
```text
{CALL_PATH_TREE — entry → facade → RPC → DO/engine → durable}
```
### 3.2 逐动作状态转移表
| 动作 | 入口（`file:line`）| wire-path | 落点 / 状态转移 |
|---|---|---|---|
| `{ACTION}` | `{FILE_LINE}` | `{HOP_CHAIN}` | `{TRANSITION}` |

### 3.3 状态机 / 子系统 `[可选]`
`{STATE_MACHINE_OR_SUBSYSTEM_WITH_ANCHORS}`

---

## 4a. nacp 协议下的授权 / 沟通形状约束 `[核心]`  ｜ rubric ②数据真相

> 多-worker 拓扑、沟通形状（几跳）、授权头、跨租户守卫。

- **4a.1 拓扑**：`{WHO_PARTICIPATES}`
- **4a.2 沟通形状 + 授权头**：`{HOPS + AUTH_HEADERS}`
- **4a.3 授权守卫（关键发现）**：`{AUTHZ_GUARDS + ASYMMETRY_IF_ANY}`
- **4a.4 动作 → wire-path → authority → 跨租户守卫**（表）：

| 动作 | wire-path | authority | 跨租户守卫（`file:line`）|
|---|---|---|---|
| `{ACTION}` | `{PATH}` | `{AUTHORITY}` | `{TENANT_GATE}` |

- **4a.5 ownership / tenant gate**：`{OWNERSHIP_GATE_FN + ANCHOR}`

---

## 4b. nacp 协议下的 observability / 日志体系完备性 `[核心]`  ｜ rubric ②数据真相 ④假绿审计

- **4b.1 互不混淆的耐久面**：`{DURABLE_OBSERVABILITY_SURFACES}`
- **4b.2 转移 → 观测构件映射**（表）：

| 转移 / 事件 | 观测落点（durable?）| `file:line` |
|---|---|---|
| `{EVENT}` | `{SINK + DURABLE_OR_MEMORY}` | `{ANCHOR}` |

- **4b.3 完备性盲点（诚实）**：`{WHAT_IS_NOT_OBSERVED — 哪些转移零耐久行 / 标签夸大耐久}`
- **4b.4 脱敏安全**：`{REDACTION_STATUS — 是否泄漏原始 payload}`
- **4b.5 观测完备性 T 层**：`{T_LAYER_FOR_OBSERVABILITY}`

---

## 5. 黑斑 / 历史阶段遗留的技术债务台账 `[核心]`  ｜ rubric ⑥缺口

> 分四态。每条带 reopen 触发器 + 锚；**勿把已 RESOLVED 的重做、勿把 owner-gated 的当 bug 就地改**。

- **5.1 真·OPEN / owner-gated（live 行为未交付）**：`{ITEMS + reopen 触发器}`
- **5.2 机制已解但 RUNTIME-gated（live 视为半开）**：`{ITEMS}`
- **5.3 won't-fix / 设计有效**：`{ITEMS + WHY_BY_DESIGN}`
- **5.4 真·RESOLVED（代码证据，勿重做）**：`{ITEMS + RESOLVING_ANCHOR}`

---

## 6. 该目标负责的 RPC 接口清单与连通性现状 `[核心]`  ｜ rubric ①构成 ⑤FE 可达性

### 6.1 表 A — RPC 表面（暴露 + 消费）
| RPC verb | 暴露方 | 消费方 | WIRED? | orphan? | `file:line` |
|---|---|---|---|---|---|
| `{VERB}` | `{ENTRYPOINT}` | `{CALLER}` | `{是/否}` | `{是/否}` | `{ANCHOR}` |

### 6.2 表 B — HTTP 动作 → wire-path → FE 可达性 / readiness
| 动作 | HTTP 路由（`file:line`）| wire-path | FE 可达? | readiness | 备注（孤儿/幻影?）|
|---|---|---|---|---|---|
| `{ACTION}` | `{ROUTE}` | `{PATH}` | `{是/否}` | `{live/planned/orphan}` | `{NOTE}` |

> **FE 可达性纪律**：对接 `{API_ADAPTER_INVENTORY_PATH}`；**孤儿 / 幻影 adapter（inventory 误标 live）必点名**（这是 §9.2 reverse-water 常客）。

---

## 7a. 监管该目标的 spike 测试体系 + 假绿审计 `[核心]`  ｜ rubric ④假绿审计

| spike 文件 | 测什么不变量 | 真牙? | live? | 证据 | T | 锚 |
|---|---|---|---|---|---|---|
| `{SPIKE}` | `{INVARIANT}` | `{真断言 / warn-only / vacuous}` | `{是/否/skip}` | `{EVIDENCE}` | `{T1-4}` | `{ANCHOR}` |

- **7a.x 假绿审计**：`{THEATER_FINDINGS — describe-污染 / 非断言空壳 / 断 deployed 已不发的 union 成员 / live 0/0 stale}`

---

## 7b. 监管该目标的 mega-journey 测试体系 + 假绿审计 `[核心]`  ｜ rubric ④假绿审计

| MJ 文件 | 业务流 | HARD 断言的不变量 | live? | 证据帧 | T | 锚 |
|---|---|---|---|---|---|---|
| `{MJ}` | `{FLOW}` | `{HARD_INVARIANTS}` | `{是/否}` | `{evidence/...json}` | `{T1-4}` | `{ANCHOR}` |

- **7b.x 假绿审计 + live-run 真相**：`{捕获-但-不断言的软臂 / capability-deferred 诚实跟踪 / 曾 RED 后 test-side 修 / 覆盖洞}`

---

## 8. 该目标涉及的 D1 / DO schema 详细说明（亲验）`[可选]`  ｜ rubric ②数据真相

> 触达哪些持久化基质（DO 私有 SQLite / shared D1 / R2 / KV）；逐表给 PK / 关键列 / 持久化的业务片段 / 锚；跨基质边界声明。

| 表 | 基质 | PK | 关键列 | 持久化的片段 | 锚 |
|---|---|---|---|---|---|
| `{TABLE}` | `{DO/D1/R2}` | `{PK}` | `{COLS}` | `{WHAT_IT_HOLDS}` | `{ANCHOR}` |

- **跨基质边界声明**：`{ISOLATION + WHO_HOLDS_WHAT + 显式边界规则}`

---

## 9. 健康状况、推荐更新计划与最终 verdict `[核心]`  ｜ rubric ③真值层裁定 ⑦verdict

### 9.1 逐能力 T 层热力图
| 能力 | T 层 | 一句话 | 锚 |
|---|---|---|---|
| `{CAPABILITY}` | `{🟢T1 / 🟡T2 / 🟠T3 / 🔴T4}` | `{ONE_LINE}` | `{ANCHOR}` |

### 9.2 reverse-water（订正母体初判 + agent over-claim）
> **本节是反假绿的留痕**。逐条：母体 / 既有叙事**怎么说** → 代码**实测怎样** → **订正成什么**（带锚）。

1. **`{母体声称}` 被证伪**：`{实测}` → 建议订正为 `{CORRECTION}`（`{ANCHOR}`）。
2. `{...}`

### 9.3 推荐更新计划（owner 裁，read-only 阶段不就地改）
| 优先 | 项 | 动作 | 触发 charter | 锚 |
|---|---|---|---|---|
| `{P0/P1/P2}` | `{ITEM}` | `{ACTION}` | `{CHARTER}` | `{ANCHOR}` |

### 9.4 最终 verdict
**`{🟢 go / 🟡 go-with-fence / 🔴 blocked}`（`{置信度}`）。**

- **`{CONSUMER}` 今天能放心建（go）**：`{WHAT}`
- **必须围栏（fence）**：`{WHAT_TO_FENCE + WHY}`
- **置信度依据**：`{WHY_THIS_CONFIDENCE — 哪些 T1 live 帧亲验 / 哪些 code-verified / 哪些仅离线}`

> **一句话**：`{PLAIN_LANGUAGE_VERDICT_FOR_OWNER}`

---

## 附录 A · 调查方法与锚点复现

```bash
# {K} 路 read-only sub-agent 分轴 + 主进程 trust-code 亲验（本域）
#   {AXIS_SPLIT — 如 A 构成/依赖树(§2-3) · B nacp+observability(§4) · C 债务+RPC(§5-6) · D 测试(§7) · E schema(§8)}
# 主进程独立亲验的承重锚：
{REPRO_COMMANDS — sed/grep/git diff 钉每条承重结论}
```

## 附录 B · 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（7 点 rubric + 假绿审计 + reverse-water + T 层热力图 + verdict） |
