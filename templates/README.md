# Nano-Agent 文档模板体系 —— 索引 · 功能价值 · 统一约定（canonical）

> 本文件是 `docs/templates/` 的**单一权威入口**，三个用途：
> 1. **模板选择**：按目标快速命中正确模板 / 流水线位点（§1）。
> 2. **功能价值 + 模块分解**：每份 active 模板**是什么、何时用 / 何时不用、承重模块**（§2）。owner 可据此让 agent 自选模板或跨模板组合模块（§3）。
> 3. **统一约定（canonical）**：状态词汇、真相 ID 命名空间、符号图例、核心名词、交叉引用的唯一真源（§4）。任何模板与本表冲突，**以本表为准**。
>
> 设计/裁定背景见 `propositions/`（9 份再设计分析，非模板）。历史/停用模板见 `retired/`（§5）。

---

## 0. 怎么用这份 README（给 owner 与 agent）

- **要 agent 自选模板**：让它读 §1 决策树 + §2 各模板「何时用/何时不用」，命中一个，并在产物头部声明 `文档性质`。
- **要 agent 组合模块**（需求跨单一模板时）：读 §2 + §3，从不同模板抽模块拼骨架，头部写一行 `结构来源(dogfood):<模板A 模块> + <模板B 模块>`（已有真实先例，§3.2）。
- **模板是默认骨架，模块是可拆装零件**。绝大多数工作选一个模板即可。

---

## 1. 快速选择

### 1.1 选择决策树（先问目标）

```text
你要产出什么?
├─ 还在"想做什么/怎么拆/可行吗/对照缺什么" ───▶ eval 家族(§2.1)
├─ 进 planning 前的「前置研究评估」(借鉴/缺口/契约草案) ▶ assessment 簇·design-prelude(§2.5)
├─ 摸清「已有系统真值层/哪些真能用/哪些假绿」 ─▶ truth/ 子簇·truth-grounding(§2.6)
├─ 多章节子阶段·要派 ≥2 份 action-plan 的策划链 ─▶ planning 三态(§2.2)
├─ 冻结 owner 决策(单轮一次性 / 多轮渐进) ─────▶ qna 簇(§2.3)
├─ 写"完工长什么样 + 净新契约 + 跨功能一致性" ─▶ design(§2.4)
├─ 排"怎么做/何序/怎么测/怎么收口" ───────────▶ action-plan(§2.4)
├─ 评审 / 跨 reviewer 合并 / 回应 / 收口 ───────▶ review·closure·respond(§2.7/2.8)
└─ API 合规 / bug 根因 / 项目 README 专科 ──────▶ report/(§2.9)
```

### 1.2 主流水线（近期实践 · grounding-truth 范式）

```text
eval(想做什么) ─┐
                ├─▶ [pre-initial-planning-qna：foundational 门·定 scope/原则]
                │        │
  [前置研究]    │        ▼
 assessment ────┼──▶ planning-initial(站①·整合裁定+真相台账)
 reference-anchor│        ▼ (reference-anchor 回灌事实)
 truth/ (如需)  └──▶ planning-proposed(站②·Δ重锚+T-R)
                          │
                          ▼ [pre-charter-qna：execution 门·关 gate]
                       planning-final(站③·critique+全态真相台账+每AP锁4台账)
                          │  1:1 派生
                          ▼
                       action-plan ×N ──▶ 执行(code-execution-log) ──▶
                       code-review → code-review-findings-ledger → code-review-respond ──▶
                       closure ──▶ eval-state-analysis(开下周期)
```

- **轻量变体**：trivial 无契约 → `eval-general-purpose → action-plan`；决策少 → `qna-singular` 一次冻结即可，不必走三态。
- **charter 已退役**：旧"重轨 charter / 轻轨 charter-lite"的「定边界 + 冻决策」角色，现由 **planning 三态（scope/phase/exit）+ qna 双门（决策冻结）** 共同承担（§5）。历史四轨设计见 `propositions/workflow-tracks.md`。

### 1.3 家族索引（active 26）

| 家族 / 簇 | 模板 | 一句话角色 |
|------|------|------------|
| **eval(6)** | `eval-general-purpose` | 提案"做什么"（兜底骨架）|
| | `eval-gap-study` | 我方缺口台账（对照参考找缺什么）|
| | `eval-state-analysis` | 交付快照 + 对账诚实 + 前瞻交接（周期铰链）|
| | `eval-reference-anchor` | grounding 借鉴锚台账（verdict + substrate-fit/TR 过滤）|
| | `eval-feasibility-study` | go/no-go 探针（token 化结论）|
| | `eval-retrospective` | 失误复盘（时间线 + 根因 + 教训）|
| **planning 簇(3)** | `planning-initial` | 站①：整合裁定原始 eval + 真相台账（foundational T-O / 暂定 T-P）|
| | `planning-proposed` | 站②：Δ 重锚 + reference-checked 真相（T-R）+ 调整溯因 |
| | `planning-final` | 站③：critique + 全态真相台账 + **每 AP 锁 4 台账** + 派生排序 |
| **qna 簇(2)** | `qna-singular` | 单轮一次性决策册 + 冻结后 truth-gate 终态台账 |
| | `qna-progressive` | 多轮渐进决策册（轮间评估 + 生成式 truth-gate 锁死三件）|
| **design(1)** | `design` | 功能簇设计（净新契约 + 跨功能一致性 + tradeoff + 验收）|
| **action-plan(1)** | `action-plan` | 执行序列（工作总表 + 内置锚区 + 测试台账 + 收口）|
| **assessment 簇 · design-prelude(2)** | `assessment-index` | 阶段评估编排器（measure-first 冻分母 + 调查面地图）|
| | `assessment-analysis` | 单调查面深评（借鉴矩阵 + 缺口台账 + 净新契约草案）|
| **truth/ 子簇 · truth-grounding(3)** | `truth/assessment-index` | 真值奠基 campaign 编排器（T1-T4 + 7 点 rubric + 反假绿 SSOT）|
| | `truth/per-domain-analysis` | 单域真相深勘（sub-agent 产物 · 7 点 rubric + reverse-water）|
| | `truth/per-cluster-value-proposition` | 簇级三态价值承诺（🟢能建/🟡围栏/🔴勿建 + FE readiness）|
| **review / closure(3)** | `code-review` | 评审制品 + verdict（单 reviewer）|
| | `code-review-findings-ledger` | 跨 reviewer 合并 + verified-findings + 三类归属 + 修复方案 |
| | `closure` | 收口 + 价值/负债台账 + handoff |
| **respond / 附加章节(2)** | `code-review-respond` | 实现者回应（append code-review §6）|
| | `code-execution-log` | 执行日志回填（append action-plan §9 厚版）|
| **report/ 专科(2) + README(1)** | `report/api-compliance` | API 合规审查（NACP 六维）|
| | `report/bug-analysis` | owner-test → bug 根因 + DAG 修复结构 |
| | `eval-README` | 对外交付物：项目顶层 README（onboarding/巡检/交接）|

---

## 2. 模板详解（功能价值 · 何时用 · 承重模块）

> 每份：**一句话功能/价值 · 何时用 / 何时不用 · 承重模块（★=灵魂）**。

### 2.1 eval 家族（6）—— 共有脊：本文是 eval，**冻结零决策**；需 owner 拍板者列 OPEN 或回 qna。状态：纯分析 `draft|reviewed|superseded`；锚型 `+frozen`。

- **`eval-general-purpose`** — charter/planning 前开放式提案"装什么、怎么拆相位"，也是不归其它 flavor 的**默认兜底**。★ §2 In/Out-Scope（提案边界）· §4 逐簇工作台账 · §6 Owner 决策门。**何时不用**：写验收→design；排序→action-plan；对照找缺口→gap-study。
- **`eval-gap-study`** — 以参考实现为标尺，研究我方某子系统缺什么、该建什么。★ §3 缺口/断点台账。**何时不用**：穷尽外部 CLI 本身（已退役 investigation）；提案整阶段→general-purpose；go/no-go→feasibility。
- **`eval-state-analysis`** — 里程碑后回溯已交付真实状态（交付了什么/债多少/声称 vs 真实），交接下一周期。★ §3 对账诚实（灵魂段，防文档剧场）· §2.2 Deferred 台账（带 reopen 触发器）。**何时不用**：给制品下收口结论→closure；复盘失误→retrospective。
- **`eval-reference-anchor`** — design 前把每个可借鉴点钉到 `path:line`/URL，给 verdict，并用 substrate-fit/TR 过滤**防"思路误抄成机制"**。★ §5 Substrate-fit/TR 过滤复核。图例：借鉴 verdict `✅借/🔶部分借/⛔反例/🆕净新`。可 frozen。
- **`eval-feasibility-study`** — charter/design 前对**单个关键决策**做 go/no-go 探针。★ §0 Verdict · §3 方法·试了什么（诚实段）· §5.2 残余风险硬前置。
- **`eval-retrospective`** — 把一次走错的弯路固化成"学习化石"。★ §2 根因表（追到机制/认知层）。**何时不用**：回看代码现状→state-analysis；评审制品→code-review。

### 2.2 planning 簇（3）★ —— 三态成熟链：`planning-initial → planning-proposed → planning-final`，逐级 supersede 不回改前序。取代旧 `eval-planning`。

> **承重梁（共有脊）**：① **§辨证审核 + 调整溯因**——每态裁定其前序，且每次 AP/DAG 调整绑定**驱动真相 Truth-ID**（§缺失=链断）；② **双门渐进冻结 + 真相台账**——owner-gate 在两端（foundational `pre-initial-planning-qna` / execution `pre-charter-qna`），真相逐态析出记入 §2 真相台账（CITE 不自冻，见 §4.2）；③ **planning 文档冻结零决策**——只 CITE 已在 qna/reference-anchor/HEAD 冻结的真相。

- **`planning-initial`**（站①）— 把原始 eval/owner 提案整合裁定成初步蓝图。★ §2 真相台账（foundational `T-O` + 暂定 `T-P`）· §3 整合裁定（无 Δ 表）· §11 下游链意图声明（省略/停链须预告）。
- **`planning-proposed`**（站②）— 拿 reference-anchor 回灌事实逐项重锚、记 `T-R`、据真相调 DAG/AP 并溯因。★ §2 真相台账(+T-R) · §3 Δ 表 + 驱动真相列（支持 N→1 合流 / 前序替换 / 外审横向 §3.C）· §6.1 DAG 调整溯因。
- **`planning-final`**（站③）— critique proposed、汇全态真相、execution-ready 定档、1:1 派生 action-plan。★★ **§2 真相台账·终态全集 `[锁死]`**（含 execution `T-O` + ≥1 HEAD-实测 `T-R`，吸收旧 §12/§13）· **§7 逐 AP 锁 4 台账 `[锁死]`**（A 工作清单 / B reference-anchor / C 测试用例 / D 收口评估，1:1 预填下游 AP）· §11.A 派生排序。

### 2.3 qna 簇（2）★ —— owner 决策唯一真源 register；**角色参数化**（中性槽，取代旧"身份反转特例"）。取代旧 `qna`。

> **共有脊**：单一真源 / Q 编号稳定 append / 冻结后只引 `Q 编号+业主回答`；**角色中性槽** `{ROLE_A}` 提问·`{ROLE_B}` second-opinion（字段名禁写死模型名）；**second-opinion 模式三态** `present|waived|retired`；**位点字段** `pre-initial-planning|pre-charter|deep-dive|spike-expansion`；**truth-gate 台账**产 owner-gated `T-O`（供 planning §2 CITE，§4.2）。

- **`qna-singular`** — 一批问题、逐题裁决、一次冻结（典型 pre-initial 定调门 / pre-charter 关 gate 门）。★ 逐 Q 字段骨架（影响范围/为什么/当前建议{ROLE_A}/Reasoning/{ROLE_B} 三槽/问题/业主回答）· §3 冻结后 Truth-Gate 终态台账。
- **`qna-progressive`** — 多轮渐进梳理真相（典型 deep-dive）：问一批 → owner 直答 → 记录真相 → agent 中场评估 → 由真相驱动下一批。★★ **锁死三件 `[锁死]`**：① §1 每轮 Truth-Gate 台账（累积 T-O）· ② 轮间「中场评估」段 · ③ 下一轮每题标"由哪条 T-O 驱动"。

### 2.4 design（1）+ action-plan（1）

- **`design`** — 功能簇设计：净新契约 + 跨功能一致性 + 深度 tradeoff + 验收。★ §3 架构稳定性/扩展策略 · §5/§6 In/Out + Tradeoff 价值判断 · §7 In-Scope 功能详列。**frozen 须 owner 裁决（指向 qna register），落 `docs/design/` 户口。**（注：refactor 版 design-neo/sketch 已退役，§5。）
- **`action-plan`** — 落地终点：消费已 frozen 的 design/qna/planning，排"怎么做/何序/怎么测/怎么收口"。**不开 Q/A**（只消费冻结结论）。★ §3 业务工作总表（不可约三元组：`涉及文件 file:line | 收口目标 | 测试映射→§8`）· **§7 内置 Reference-Anchor 锚区**（含 §7.3 安全项威胁模型，不得留空）· **§8 测试台账**（类型/层/来源 🆕新增·♻️沿用·🔱fork/四元组 PASS）· §10 收口（DoD=测试台账全 PASS 映射）。状态：`+executing|executed`。

### 2.5 assessment 簇 · design-prelude（2）—— **独立簇，非 eval 血缘**；进 planning 前的「前置研究评估」（关心"要建什么/能借什么/怎么落地"）。

- **`assessment-index`** — 一个多面相位评估开场：measure-first 冻结全阶段共享**分母**，画"调查面地图 + owner-gate 候选 + 勿重做表"，编排 N 份 analysis。★ §2 站① measure-first 预核查（冻分母）· §3 逐调查面登记。
- **`assessment-analysis`** — 对**一个调查面**做 measure-first 深评，喂下游规划/设计。★ §3 借鉴锚定矩阵 · §4 缺口台账 · §6 净新契约草案 · §7 substrate-fit 过滤 · §9 验收格栅草案 · §10.2 owner-gate 候选。
> **与 truth/ 区别**：本簇朝"**建新**"（借鉴/契约/验收）；truth/ 朝"**验真**"（已有系统真值层）。二者无血缘、勿混用。

### 2.6 truth/ 子簇 · truth-grounding（3）—— 系统真值奠基 campaign（关心"已有系统真相是什么、哪些真能用、哪些假绿"），发动 sub-agent 逐域勘察。

> **共有脊**：measure-first（HEAD 实测+file:line）· 反假绿（灵魂·reverse-water 留痕）· trust-code 亲验（禁据二手 closure）· degraded≠green（T1 live 不可由 T2 离线冒充）· read-only-first。**判据 SSOT**：T1-T4 真值分层 + 逐域 7 点 rubric 只在 index §2 定义一次（§4.4）。

- **`truth/assessment-index`**（站①）— campaign 编排器：立判据 + 切 N 域 + 派 read-only sub-agent + Living Tracker。★ §2 方法判据（T1-T4 + 7 点 rubric）· §3 红线 · §4 域路由 · §7 状态总表。
- **`truth/per-domain-analysis`**（站②）— 单域真相深勘（sub-agent 产物）：7 点 rubric + 假绿审计 + FE 可达性 + reverse-water。★ §9.1 逐能力 T 层热力图 · §9.2 reverse-water · §9.4 verdict（go/go-with-fence/blocked）。
- **`truth/per-cluster-value-proposition`**（站③）— 簇级上卷成给前端的承诺：🟢能建/🟡围栏建/🔴勿建。★ §3/§4/§5 三态价值台账 · §6 GAP(P0-P2) · §7 对前端意义 + 利用法。

### 2.7 review / closure（3）

- **`code-review`** — 评审 design/action-plan/code/docs/closure + verdict（单 reviewer）。★ §0 verdict + 等级 · §2 审查发现（R1..Rn）· §3 In-Scope 逐项对齐 · §4 防把 deferred 误判 blocker。状态：`reviewed|changes-requested|re-reviewed|closed`。
- **`code-review-findings-ledger`** — 收齐 **≥2 份** 独立 reviewer 后，实现者平铺/合并去重/逐条对真实代码亲验，成单一权威台账 + 修复方案。★ §3 verified-findings 台账 · **三类归属问责轴**（`[true-bug]`/`[partial-delivery]`/`[true-deferred]` + 反规避诚实闸）· §5 初步修复方案。状态：`triaged|fixing|resolved|closed`。
- **`closure`** — 阶段/子阶段收口。先选档（子阶段 §0-5 / 阶段 final §0-7 / grand §0-9）。★ §5 诚实收口声明（5 态）· §8 价值/负债台账（5 级证据）。纪律：close-type 4 类 + 四元组证据（commit+query/test+run-time）。

### 2.8 respond / 附加章节（2）—— **不是独立文档，append 到宿主**。强制 banner：宿主/挂载位/append-only/作者·时机/回链 item-ID/多轮。

- **`code-review-respond`** — 实现者修复后逐项回应（append code-review §6）。★ 6.2 逐项回应表（R-ID × `fixed|deferred|rejected`）· 6.5 验证结果 · 6.7 Ready-for-rereview gate。**append-only**，不改写 §0-§5。
- **`code-execution-log`** — action-plan `executed` 后回填执行日志（append §9 厚版）。★ 9.1 逐工作项状态（回链台账 ID）· 9.5 pre-existing 失败带 git 证据甩锅。纪律：计划 vs 实际逐条偏差；residual 交后继不回填本阶段。

### 2.9 report/ 专科（2）+ project-README（1）

- **`report/api-compliance`** — 对照 frozen contract / qna 审 API surface 合规（NACP）。★ §4 跨簇 NACP 合规（Authority 翻译 / Trace UUID / Error Code 字典 / Tenant 边界 / Envelope Drift Gate）。
- **`report/bug-analysis`** — owner-test 回来后、写 charter/action-plan **之前**的根因诊断。★ §6 架构判定(hot-fix vs 长治) · §7 完整 DAG 修复结构 · §8 测试体系归责 · §10 修复后测试方案 · 附录 Z 长期原则。
- **`eval-README`** — 给一个仓库产出/重写**对外**顶层 `README.md`（onboarding/巡检/交接）；借 eval 对账诚实但产出是交付物。档位 A/B/C（整库 / 子项目 / 单目录极简）。

---

## 3. 模块重组指南（跨模板组合）

### 3.1 原则
- **默认选一个模板**；只有一个分析同时需要多模板能力时才组合。
- 以一个模板作主骨架、从别处借模块嵌入，头部写 `结构来源(dogfood):…`；组合**不改变模块语义与纪律**。

### 3.2 真实先例（见 `propositions/`，可仿照）

| 产物 | 主骨架 | 借入模块 |
|------|--------|----------|
| `propositions/value-proposition-of-template-docs.md` | `eval-state-analysis` | + `design Tradeoff` + `design Value Verdict` + `eval-gap-study 缺口台账` |
| `propositions/nano-agent-vs-SDD.md` | `eval-gap-study` 对照 | + `design Tradeoff` + `design Verdict` |
| `propositions/CCMD-vs-SDD-by-opus.md` | `eval-general-purpose` 共有脊 | + `eval-retrospective §2 根因表` + `design Tradeoff/Verdict` |

### 3.3 高复用模块目录（最常被借出）

| 模块 | 出处 | 借来做什么 |
|------|------|------------|
| TL;DR / Verdict 结论先行 | 所有 eval / code-review §0 / closure §0 | 任何分析的开头一句话裁定 |
| Tradeoff 辩证（选 X 不选 Y / 代价 / 重评）| `design` | 任何有争议取舍 |
| 对账诚实（声称 vs 代码 / frozen≠done）| `eval-state-analysis §3` | 防文档剧场 |
| 根因表（追到机制/认知层）| `eval-retrospective §2` | 复盘失误为什么发生 |
| substrate-fit / TR 过滤 | `eval-reference-anchor §5` / `assessment-analysis §7` | 把外部机制按本仓技术路线降级 |
| 验收格栅（F→收口目标→Test-ID）| `design` / `assessment-analysis §9` / `action-plan §8` | 可验证完工标准 |
| 裁定动词 rubric（KEEP/REFRAME/…）| `planning §辨证 + 附录 B` | 裁定/对比前序版本 |
| T1-T4 真值分层 + reverse-water | `truth/assessment-index §2` / `truth/per-domain-analysis §9` | 系统真值层裁定 + 反假绿留痕 |
| 真相台账 + 驱动真相溯因 | `planning §2/§辨证` / `qna truth-gate` | 决策/事实冻结 + 调整可追溯 |
| 诚实收口 5 态 + 价值-负债台账 | `closure §5/§8` | 交付物分级证据 |
| DAG 修复结构 + 测试归责 | `report/bug-analysis §7/§8` | 多问题共因 + 分层归责 |

---

## 4. 统一约定（CANONICAL —— 唯一真源）

### 4.1 文档状态词汇
- **核心四态（共用）**：`draft → reviewed → frozen → superseded`。
- **家族扩展**：`action-plan` + `executing|executed`；`code-review/api-compliance/*-respond` 用 `reviewed|changes-requested|re-reviewed|closed`；`code-review-findings-ledger` 用 `triaged|fixing|resolved|closed`。
- **eval 纯分析型**（general-purpose/gap-study/state-analysis/feasibility/retrospective）：`draft|reviewed|superseded`（快照不 freeze）；锚型（reference-anchor / planning-final）：`+frozen`。
- **truth/ 子簇**：per-domain `draft|cross-reviewed|attested|superseded`；index `active campaign|closed`；per-cluster `draft rollup|reviewed|frozen`。
- **澄清**：`frozen`（文档定稿锁定）≠ planning/eval 的"冻结零决策"（指不替 owner 拍板）。

### 4.2 ★ 真相 ID 命名空间（qna ↔ planning 互锁，唯一真源）
- **`T-O` owner-gated 真相**——由 **qna truth-gate 冻结**（qna-singular §3 / qna-progressive §1）；子类型 `foundational`（pre-initial-planning 位点）/ `execution`（pre-charter 位点）。**planning §2 真相台账 CITE 这些 T-O，不自冻。**
- **`T-R` reference-checked 真相**——来自 reference-anchor 回灌 + HEAD 实测；子类型含 `HEAD-实测`（planning-final §2.2 锁死 ≥1 条）。**不进 qna**（qna 只产 T-O）。
- **`T-P` provisional 暂定前提**——planning-initial 态未冻结的 conjecture，待 proposed 用 T-R 证实/证伪。
- **stage 轴（planning 簇）**：`initial|proposed|final` = 成熟度轴，独立于 status，= 文件名（planning-initial/proposed/final），勿塞进 status。

### 4.3 符号图例（三套，语义不同，**勿混用**）
- **复用判定**（我方代码处置；planning / design / action-plan）：`✅ 复用` / `♻️ 重 substrate` / `🆕 净新`。
- **借鉴 verdict**（外部参考裁定；eval-reference-anchor / assessment-analysis §3）：`✅ 借` / `🔶 部分借` / `⛔ 反例` / `🆕 净新`。
- **真值分层 T1-T4**（仅 truth/ 子簇）：`🟢 T1 live-proven` / `🟡 T2 离线 gate-green` / `🟠 T3 诚实降级/deferred` / `🔴 T4 被抓假绿`。
> 注：truth/ 的三态价值台账（per-cluster §3/§4/§5）用 `🟢能承诺/🟡部分/🔴不能`，是 T 层的**消费者上卷视图**，与 T1-T4 同源不同表。

### 4.4 truth-grounding 判据（仅 truth/ 子簇 · SSOT 在 `truth/assessment-index §2`）
- **7 点 rubric**（每份 per-domain-analysis 必答）：① 构成 ② 数据真相 ③ 真值层裁定(T1-4) ④ 假绿审计 ⑤ FE 可达性 ⑥ 缺口/deferred/blocker ⑦ verdict(go/go-with-fence/blocked)。
- **反假绿红线**：假绿必点名 + reverse-water 留痕；degraded≠green；trust-code 亲验禁据二手。

### 4.5 裁定动词 rubric（planning §辨证 / `propositions/better-planning.md`，可按 lineage 覆盖）
- proposed（vs initial）：`KEEP / REFRAME / CLOSED / NEW`。
- final（vs proposed）：`CONFIRM / CORRECT / REFINE / RESIZE / GAP / SCOPE↕`。

### 4.6 qna 角色与模式（仅 qna 簇 · SSOT 在 qna 簇共有脊）
- **角色中性槽**：`{ROLE_A}` 提问/架构（Opus/Fable/…）+ `{ROLE_B}` second-opinion（GPT/none）+ `owner` 裁决；**文首一次性自填，不再每次声明"反转"**；字段名中性化 `{ROLE_B}对{ROLE_A}推荐线路的分析`（禁写死模型名）。
- **second-opinion 模式**：`present`（走完三槽）/ `waived`（owner 直答、留空、不阻塞冻结）/ `retired`（不设 second-opinion 栏；progressive 可自第 N 轮起退役）。
- **位点字段**：`pre-initial-planning | pre-charter | deep-dive | spike-expansion`。

### 4.7 核心名词表（统一中英）

| 名词 | 含义 |
|------|------|
| `净新`(net-new) | 从零定义的对外契约 / 架构接缝 |
| `扩展既有`(additive) | 在已建 substrate 上加列/加端点 |
| `grounding` | 架构边界 + 仓内 file:line 锚的落地依据（保留英文）|
| `substrate` | 仓库现实代码基底（保留英文）|
| `收口目标` | 一句话可验证完工标准 |
| `验收格栅` | `功能 F → 收口目标 → Test-ID` 三联 |
| `reverse-water` | 用代码证伪母体/前序的过度声称并订正留痕（truth/）|
| `truth-gate` | qna 冻结 owner-gated 真相（T-O）的台账 |
| `qna register` | owner 决策唯一真源 |

### 4.8 交叉引用与占位符
- **引用模板**用文件名根（`eval-reference-anchor` / `planning-final` / `qna-singular` / `truth/per-domain-analysis`），不裸缩写。
- **`qna` 大小写**：文件/register 一律小写；决策只活在 register，内嵌 QNA 须指向 register。
- **占位符**：统一 `{UPPER_SNAKE}`，backtick 包裹。
- **簇共有脊**：eval / planning / qna / truth/ 四簇各有头部「共有脊」块（同簇结构一致）；respond 家族用 banner。
- **wiki-链**：同簇互引用 `[[name]]`（如 `[[planning-proposed]]`、`[[truth/per-domain-analysis]]`）。

---

## 5. retired/ 说明

`docs/templates/retired/` 存放已被 active 集取代的历史模板，**不用于新工作**：
- **`charter` / `charter-lite`** → 定边界/冻决策角色由 **planning 三态 + qna 双门** 吸收（§1.2）。
- **`eval-planning`**（一文件三态开关）→ 拆为 **planning-initial/proposed/final** 三独立文件（+ 真相台账 + 双门）。
- **`qna`**（身份写死 GPT问Opus答）→ 拆为 **qna-singular / qna-progressive**（角色解耦 + truth-gate）。
- **`design-neo` / `design-sketch`** → design 家族现仅保留 `design`。
- **`respond-post-freeze` / `respond-verification`** → 退役（碰撞核实/冻结后补强按需并入 review/respond 流程）。
- **`investigation` / `code-review-eval` / `code-megafile-header` / `_TEMPLATE-spike-finding` / `issue-closure-fax9-and-beyond` / `composition-factory.ts` / `wrangler-worker.toml`** → 专项/陈旧，被现 active 集覆盖。

> 注：部分 active 模板的「何时不用」仍含指向 `charter` 的历史措辞（如 eval 家族）——读作"定阶段边界/冻结"语义，落点改为 planning 三态 + qna；待逐份模板下次保养时订正。

---

## 附录 · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.2 | 2026-05-31 | Opus 4.8 | 完整重写为可操作索引（§0 指南 + §1 决策树 + §2 模块分解 + §3 重组指南 + §4 canonical）|
| v0.3-0.5 | 2026-06-11 | Opus 4.8 | 同步 action-plan v2 / 新增 review-findings-ledger + 三类归属问责轴 |
| **v0.6** | **2026-06-24** | **Opus 4.8** | **完整重写以反映模板体系重构**：① charter 家族退役、`eval-planning→planning 簇(3)`、`qna→qna 簇(2)`；② 新增 `assessment 簇·design-prelude(2)` 与 `truth/ 子簇·truth-grounding(3)`、`report/ 专科(2)`、`eval-README`；③ design 家族收敛为 `design`、`review-findings-ledger→code-review-findings-ledger`、`respond-execution-log→code-execution-log`、respond-post-freeze/verification 退役；④ 新增 §4.2 真相 ID 命名空间（qna `T-O` ↔ planning §2 互锁）、§4.4 truth-grounding 判据、§4.6 qna 角色/模式；⑤ §1.2 主流水线据 grounding-truth 实践重写、§5 legacy→retired。active 23→26 |
