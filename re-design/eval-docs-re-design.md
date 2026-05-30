# Eval 文档分型与模板再设计建议

> 文档对象：`docs/eval/**` 全量 eval 文档的分型与模板化建议
> 作者：Claude Opus 4.8（独立 reasoning + 6 路并行子代理采样）
> 日期：2026-05-30
> 文档性质：**re-design 建议 / 向 owner 的汇报**（不是 charter、不是 design、不冻结任何决策）
> 文档状态：`draft — 待 owner 审阅`
> 调查输入：
> - 全量清单：`docs/eval/**`（397 份）、`docs/design/**`（175 份）、`docs/action-plan/**`（204 份）
> - 现有模板：`design.md` / `action-plan.md` / `qna.md` / `charter.md` / `charter-lite.md` / `investigation.md` / `closure.md` / `code-review*.md` / `api-compliance.md` / `bug-analysis-report.md`
> - 深读采样：约 50 份 eval（6 个家族各 8–9 份，偏重近期 more-capabilities / more-intelligence / product-enhancement / web-v60 / pro-to-product）

---

## 0. 一句话结论（TL;DR）

**eval 不是"工作流第 1 步的一份文档"，而是整个 charter 之前的发散调查带 + 收尾上一周期的回溯带**——它天然多型，所以"没有固定格式"是对的，但其中有几个**高频、形状稳定、漂移代价高**的子型值得固化成模板。

对 owner 的核心建议：**做 6 个 eval 模板**，而不是 3 个。

- ✅ **采纳 owner 提的 3 个**：`general-purpose`、`feasibility-study`、`state-analysis`——三个都成立，但定义需要收紧（见 §4.2）。
- ➕ **我额外推荐 3 个**：`gap-study`（缺口研究，**语料里最大的无模板家族，约 42 份**）、`reference-anchor`（参考锚定台账）、`retrospective`（复盘）。
- 🔀 **明确"归并不另立"清单**：review→`code-review.md`（已有，约 108 份）、pre-charter-qna→`qna.md`（已有）、外部 CLI 深析→`investigation.md`（已有）、spike-design→`design.md`、evidence-pack→`closure.md`、debt-ledger→作为 `state-analysis` 的一个 profile。

并且：**顺带回答 owner 对 design / action-plan 角色的疑虑**——这两份文档的分工其实是清晰的，模糊感来自"STEP1 的 planning 类 eval 已经在做相位拆分和 DAG"，看起来像 action-plan，但它**不冻结任何东西**。判别标准是**模态（modality）而非内容**（见 §2.2）。

---

## 1. 调查方法与采样

### 1.1 两层采样

| 层 | 方法 | 规模 | 目的 |
|----|------|------|------|
| 全量 | 文件名模式统计 | 397 份 eval | 摸清各家族的**相对体量**，让推荐基于真实分布而非样本偏差 |
| 深读 | 6 路并行子代理，每路读 8–9 份 | ≈50 份 | 摸清每个家族的**真实骨架**（章节、受众、作者、产出形态、触发点） |

### 1.2 全量文件名分布（一份文件可命中多个模式，下表为近似量级）

| 家族（按体量降序） | 近似份数 | 占比 | 当前是否已有模板 |
|--------------------|---------|------|------------------|
| **review**（`*-reviewed-by-*` / `review-ledger` / `full-scan`） | ≈108 | 27% | ✅ `code-review.md` + `code-review-eval.md` + `code-review-respond.md` |
| **study / gap / compared**（`*-study` / `*gap*` / `*compared*`） | ≈42 | 11% | ❌ **无** |
| **planning / scope / thoughts**（`*planning*` / `*thoughts*` / `scope-analysis` / `inclusions`） | ≈33 | 8% | ❌ **无** |
| **state-analysis / water-level**（`state-analysis` / `water-level` / `analysis-after`） | ≈23 | 6% | ❌ **无** |
| **evidence**（`*evidence*` / `realized-code` / `external-contract-surface` / `nacp-compliance`） | ≈18 | 5% | 🔶 部分可用 `closure.md` |
| **investigation**（外部 CLI 深析，`mc-investigation` / `investigation`） | ≈17 | 4% | ✅ `investigation.md` |
| **qna**（`*qna*`） | ≈12 | 3% | ✅ `qna.md` |
| **spike-design**（`*spikes-design*` / `new-spikes` / `spike-expansion`） | ≈9 | 2% | 🔶 实为 `design.md` 形态 |
| **retrospective / debt / misstep** | ≈3 | <1% | ❌ **无** |
| **feasibility / prototype** | ≈2 | <1% | ❌ **无** |
| **reference-anchor** | ≈2 | <1% | ❌ **无** |

### 1.3 作者署名分布（跨家族横切）

| 署名 | 份数 |
|------|------|
| `-by-opus` | 113 |
| `-by-GPT` | 89 |
| `-by-deepseek` | 48 |
| `-by-kimi` | 38 |
| `-by-GLM` / `-by-sonnet` | 17 |
| **无 `-by-` 标记** | 86（22%） |

**结论性观察**：约 78% 的 eval 把作者烤进文件名，因为它们是在**多模型并行扇出（panel fan-out）**中产出的；并且不少 review/qna 会被**回填成多方制品**（追加"实现者回应"段、追加"对审查的评价"段、追加跨源合并 ledger）。

> 这一条直接构成模板设计约束：**每个 eval 模板都要预留 (a) 审查者/作者身份槽（含 panel 位）与 (b) 可选的回应/round-trip 段**——否则模板会和真实用法打架。

---

## 2. 工作流全景：eval 在生命周期中的真实位置

> 本节直接回应 owner 对 "design 文件和 action-plan 文件在工作流程中的作用" 的长期疑虑。

### 2.1 实测到的生命周期，比"4 步"更丰富

owner 描述的工作流是：`STEP1 eval → STEP2 full-charter → STEP3 design+faq → STEP4 action-plan`。采样后我看到的**真实形态**是：STEP1 的 "eval" 不是一份文档，而是一整条**发散调查带**，它内部还有子阶段；而上一周期的 **review + state-analysis** 同时承担了"收尾旧周期 / 开启新周期"的双重职责。完整环：

```text
─── 上一周期收尾 ───────────────────────────────────────
   implementation → review(评审 eval) → closure → state-analysis(回溯快照)
                                                       │  ← 既收尾旧周期，又开启新周期
                                                       ▼
─── STEP 1 · EVAL（charter 前的发散调查带，多型并存）─────
   1a investigation / study / gap   读参考、画缺口          [gap-study / investigation]
   1b reference-anchor              钉住"借哪些、怎么借"     [reference-anchor]
   1c initial→proposed→re-planning  提相位拆分与 DAG（提案） [general-purpose / planning]
   1d feasibility                   对单个决策做 go/no-go    [feasibility-study]
   1e debt-analysis                 盘点要还的债              [state-analysis(debt profile)]
   1f state-analysis                上一里程碑的交付快照      [state-analysis]
   1g pre-charter-qna               把业主决策冻结            [qna ← 已有模板]
                                                       │
                                                       ▼
─── STEP 2 · FULL-CHARTER ──────────────────────────────
   冻结：为什么现在做 / 本阶段做与不做 / 各 Phase 边界 / 退出与失败判据
                                                       │
                                                       ▼
─── STEP 3 · DESIGN + FAQ ──────────────────────────────
   把已冻结决策展开成"可验证的验收条件"；owner/architect 级问题继续在 qna register 冻结
                                                       │
                                                       ▼
─── STEP 4 · ACTION-PLAN ───────────────────────────────
   把已冻结的 design 结论排成执行序列：Phase 表 / 工作项 / 测试方式 / 收口
                                                       │
                                                       ▼
   implementation → review → closure → state-analysis …（环闭合）
```

**关键洞察**：eval 之所以"没有固定格式"，正因为它覆盖了从 1a 到 1g 七种认知任务 + 上一周期的 review/state-analysis。把它们硬塞进一个模板是错的；但放任全部无模板，也让高频子型反复漂移。正确解是**分型固化少数几个，长尾留给 general-purpose**。

### 2.2 design vs action-plan 的真实分工（直接回应疑虑）

读完两份模板的"纪律"段后，分工其实**写得很清楚**，且彼此咬合：

| 维度 | **design.md**（STEP3） | **action-plan.md**（STEP4） |
|------|------------------------|------------------------------|
| 回答的问题 | **WHAT + WHY**：是什么、为什么、边界在哪 | **HOW + WHEN + 顺序**：怎么落、先后、谁先谁后 |
| 对决策的姿态 | **冻结**：contract/boundary/scope/runtime-posture/security 必须在此或 qna 冻结（§0 纪律） | **只消费**：不开 Q/A，只读引用已冻结结论（§0/§6 纪律） |
| 产出形态 | **可验证的验收条件**（§7 明确写"不是任务列表，不写 `[ ] 创建文件 X`"） | **执行任务表**（§4：工作项 / 涉及文件 / 测试方式 / 收口标准） |
| 不做什么 | 不排执行序列 | 不重开设计问题 |
| 共同支点 | ←──── **冻结的 QNA register** 是二者之间的唯一接缝 ────→ | |

**为什么会让人觉得模糊**：因为 STEP1 的 planning / proposed-execution-plan 类 **eval** 已经在画 Phase 拆分、DAG、甚至 owner gates——形态上**长得像 action-plan**。但它们在文首都显式声明"**不冻结任何决策 / 不是 charter / 不是 action-plan**"（采样到的 planning 文件无一例外）。真正的判别器是：

> **模态（modality），不是内容（content）。**
> - **eval（含 planning）= 提案**：说 "proposed / 倾向 / 待 owner 决断 / OPEN"，**冻结零个东西**。
> - **charter = 冻边界**：冻结"做/不做、Phase 职责、退出判据"。
> - **design = 冻决策 + 写验收**：冻结 contract/scope，给出可验证收口目标。
> - **action-plan = 排序 + 执行**：把冻结结论排成 Phase 工作表。

同一组"Phase 列表 + DAG"在 eval 里叫"建议"，在 charter 里叫"冻结边界"，在 action-plan 里叫"执行序列"——**内容相似、模态不同**。这就是疑虑的根源，也是它的解。

### 2.3 推论：eval 是唯一仍缺模板治理的大类

charter / design / action-plan / qna / closure / code-review / investigation / api-compliance / bug-analysis 都已有固定模板。**eval 是唯一一个体量巨大（397 份）却整体无模板的文档大类**。因此 owner 的方向是对的：不是给 eval 套一个模板，而是**把 eval 拆成几种类型、各配模板**。

---

## 3. Eval 类型学：从语料中浮现的家族

把六路采样合并，按**认知任务 + 时间姿态**两个轴归纳，eval 真实存在 9 个家族（review/investigation/qna 已有模板，列出以正其位）：

| # | 家族 | 认知任务（回答什么问题） | 时间姿态 | 典型样本 | 现归宿 |
|---|------|--------------------------|----------|----------|--------|
| F1 | **review（评审）** | "这份上游制品忠于真相吗？能冻结/收口吗？" | 对既有制品回看 | `*-reviewed-by-*`、`GPT-review-ledger` | ✅ code-review.md |
| F2 | **gap-study（缺口研究）** | "对照参考，我们缺什么？接下来该建什么？" | 横向/前瞻 | `api-gap-study`、`llm-wrapper-study`、`mc-investigation-0x`、`claude-code-compared` | ❌ 无 |
| F3 | **general-purpose / planning（规划/范围）** | "这个阶段应该装什么？怎么拆相位？" | 前瞻提案 | `initial-planning`、`proposed-planning`、`scope-analysis`、`re-planning`、`work-inclusions` | ❌ 无 |
| F4 | **state-analysis（状态分析/水位）** | "上一里程碑真实交付了什么？债务多少？下一步？" | **回看交付 → 前瞻开新周期** | `state-analysis-after-*`、`water-level-after-*` | ❌ 无 |
| F5 | **feasibility（可行性/原型）** | "这条路走得通吗？go/no-go？" | 前瞻、gate 单个决策 | `wrangler-dev-feasibility`、`mjs-to-ts-prototype` | ❌ 无 |
| F6 | **evidence（证据包）** | "现在代码/运行时**实际**是什么样？（可复现引证）" | 回看本仓真相 | `realized-code-evidence`、`first-real-run-evidence`、`external-contract-surface` | 🔶 closure.md |
| F7 | **investigation（外部 CLI 深析）** | "外部参考 X **整体**长什么样？" | 横向、研究对象=外部 | `investigation.md` 实例 | ✅ investigation.md |
| F8 | **reference-anchor（参考锚定）** | "每个可借鉴点钉在哪、借不借、substrate 适配吗？" | 横向 → 喂 design | `*-reference-anchor-by-opus` | ❌ 无 |
| F9 | **retrospective / debt（复盘/债务）** | 复盘："哪步走错了、教训是什么？" / 债务："要还哪些债、什么顺序？" | 回看决策/债务 | `seam-misstep-retrospective`、`debt-repayment-analysis`、`MCS1-MCS2-introspect` | ❌ 无 |

**注意 F2 vs F7 的关键区别**（最容易混）：`investigation.md` 的研究**对象是外部 CLI 本身**（产出"一个外部工具的能力清单+评分"）；F2 gap-study 的研究**对象是 nano-agent**，参考只是"标尺/借鉴源"（产出"我方缺口台账 + 优先级建造建议，喂 charter"）。二者方向相反，不能互相替代。

---

## 4. 模板推荐（核心）

### 4.1 判定原则：什么样的 eval 子型值得一个模板？

不是所有家族都该有模板。模板的收益是"防漂移、提速、便于 review/handoff 引用"；成本是"增加心智负担、可能没人用、扼杀 eval 本该有的灵活"。判据：

> **同时满足"高频 或 漂移代价高"× "形状稳定且与现有模板不重叠"→ 固化；否则留给 general-purpose 兜底。**

按这把尺子过一遍 9 个家族：

| 家族 | 高频? | 形状稳定且独特? | 已有模板覆盖? | 判定 |
|------|-------|-----------------|---------------|------|
| F1 review | ✅108 | ✅ | ✅ code-review | **归并**（已覆盖） |
| F2 gap-study | ✅42 | ✅（verdict-first → 证据基线 → 编码缺口台账 → 优先级建造 → charter 交接） | ❌ | **新建**（我加） |
| F3 planning | ✅33 | ✅（=最常见的开放式 eval 骨架） | ❌ | **新建 = general-purpose**（owner 提） |
| F4 state-analysis | ✅23 | ✅（回看快照 + 对账诚实 + 前瞻交接） | ❌ | **新建**（owner 提） |
| F5 feasibility | ❌2 | ✅（假设 → 试了什么 → 结果 → verdict token → 残余风险） | ❌ | **新建**（owner 提；低频但形状极清晰、决策 gate 价值高） |
| F6 evidence | 🔶18 | 🔶（与 closure 的证据段重叠） | 🔶 closure | **归并 → closure**（或薄 code-evidence，见 §4.4） |
| F7 investigation | 🔶17 | ✅ | ✅ investigation | **归并**（已覆盖） |
| F8 reference-anchor | ❌2 | ✅✅（axes×sources verdict 矩阵 + substrate-fit/TR 过滤，极独特） | ❌ | **新建**（我加；低频但形状无可替代） |
| F9-retro retrospective | ❌2 | ✅（时间线 + 根因表 + 教训 + 正确形态） | ❌ | **新建**（我加；便宜、recall 价值高） |
| F9-debt debt-ledger | ❌1 | 🔶（评分债务台账，近似 state-analysis） | ❌ | **归并 → state-analysis 的 debt profile** |
| qna（pre-charter） | ✅12 | ✅ | ✅ qna | **归并**（已覆盖，两种朝向都已支持） |
| spike-design | 🔶9 | ❌（就是 design 骨架，spike 是载荷） | ✅ design | **归并 → design** |

### 4.2 采纳 owner 的 3 个（定义收紧版）

#### ① `general-purpose`（= planning / scope 骨架，作默认兜底）

owner 提的"general-purpose"应该**就是 planning/scope 这个最常见的开放式形态**，而不是另造一个空泛兜底壳。采样证据：33 份 planning 文件横跨 5 个阶段、4 位作者、2 个模型版本，在**没有共享脚手架**的情况下收敛到同一套 ~10 段骨架——这正是"默认文档形状"的标志。

- **必备段**：头部 + **性质免责声明**（"本文是 eval/提案，冻结零决策，不是 charter/action-plan"）→ TL;DR → 上游输入锚定 → in/out scope → 命名的相位/工作簇列表 → 逐簇工作台账（id/项/来源/复用-vs-净新/规模/风险）→ DAG（关键路径+并行窗）→ owner 决策门/开放问题 → 风险册 → 建议 + 收尾一句话 + 修订历史。
- **可插拔模块**：测试矩阵、参考蓝图附录、options-with-tradeoffs 表。
- **设计取向**：骨架要**轻且模块化**——默认实例化成 planning 形态，但允许删模块以兜住长尾 eval。这样"catch-all"与"最常见形态"两个诉求同时满足。

#### ② `feasibility-study`（go/no-go 探针）

名字贴切，直接采纳。低频（仅 2 份）但形状极清晰、且每份都精确 gate 一个 charter 决策（`Decision affected: QNN`）。

- **必须强制作者写明**：(1) 假设/问题 + 它 gate 的 charter 决策；(2) **试了什么**——若**未真跑要显式声明**（采样里 deferred-measurement 表 / "static analysis" 框定是反复出现的诚实模式）；(3) 结果——**既允许"原型数字"也允许"分类/缺口矩阵"**两种形态；(4) **verdict token**（如 `conditional-ready` / `ready-for-PPX10`）；(5) 残余风险 / 硬前置条件（每份都把一条约束带进下一相位）。

#### ③ `state-analysis`（里程碑后回溯快照）

直接采纳，且它与 general-purpose 有**本质区别**，必须独立：

- **独特之处**：(a) **时间姿态**——回看*已交付*状态（真实代码里成立了什么、水位到哪），再回身喂下一周期；(b) **绑定里程碑边界**（after-MCX4/MC8/MIX3…），是周期之间的铰链；(c) **对账诚实纪律**——把*声称*的价值与*真实*代码对账（over/under-claim 审计、"frozen≠done"、占位/假零猎杀），并把每条 deferred 项带 reopen 触发器前结；(d) **反镀金纪律**——多份显式警告"别为水位而造水位、别硬开不必要的下一相位"。
- **必备段**：头部（含"本文是 state-analysis，不是 closure/verdict/charter"声明 + 权威输入）→ 水位/健康 一句话 → **回看清单**（交付价值台账 / deferred 台账 / 逐单元评级矩阵）→ 归因/缺口分析（根因缝、覆盖缺口、over/under-claim）→ verdict（价值-vs-债务 / 达成度 / 健康评级）→ **前瞻交接**（deferred + reopen 触发 + 下一周期建议）→（可选）复现命令、修订历史。
- **内置 profile（不另立模板）**：
  - *spike/test water-level profile*：按 D/W/E（+ runtime）桶给 spike 套件评级、对比上一基线。
  - *debt-ledger profile*（吸收 F9-debt）：评分债务台账（内聚/紧急/复杂/风险/价值）+ closure 判据 + DAG。

### 4.3 我额外推荐的 3 个（含辩证）

#### ➕④ `gap-study`（缺口研究）——**我最强的追加建议**

- **为什么要**：这是**语料里最大的无模板家族（≈42 份，仅次于已有模板的 review）**。它的认知任务高度一致："对照参考画出 nano-agent 的缺口 → 编码缺口台账 → 优先级建造建议 → 喂 charter/design"。形状稳定：`verdict-first → 证据基线 → 编码盲点/断点台账(带 file:line) → 优先级建造(带工作量/工作块) → charter 交接`。
- **反方**：它会不会和 general-purpose、investigation 重叠？
- **我的回应（三方划界，很干净）**：
  - `investigation.md` = **穷尽分析一个外部 CLI**（对象=参考，14 段固定，产出能力评分卡）；
  - `gap-study` = **分析我方子系统/接口面、以参考为标尺找缺口**（对象=nano-agent，轴由作者选：subsystem / API-category / 调查问题 / 单参考标尺）；
  - `general-purpose` = **提案一个阶段该装什么**（前瞻、冻结零决策）。
  三者对象与模态都不同，不可互替。gap-study 的 body 轴**应允许作者自选、不写死**，但"编码盲点台账 + 优先级建造 + charter 交接"的脊梁要固定。

#### ➕⑤ `reference-anchor`（参考锚定台账）

- **为什么要**：形状**无可替代地独特**——`主题轴 × 来源引擎`的锚定矩阵 + 4 符号 verdict 图例（✅借/🔶部分/⛔反例/🆕净新）+ 置信分层（context-line/HEAD/web）+ 反例坑表 + 净新表 + web 来源台账 + 核验记录 + **substrate-fit / 技术路线(TR-1..10) 过滤**（把借来的机制降级/重映射）。general-purpose 无法在不丢脊梁的情况下托住它。
- **反方**：只有 2 份，太低频，值得一个模板吗？
- **我的回应**：它是**新近确立的实践**（MCCM/MCX 才出现），且是"设计三件套"（initial-planning → **reference-anchor** → pre-charter-qna）的承重件。正因为它新、且形状高度特化，**才更需要模板防止下一份漂移**。这是一个"前瞻性下注"。**建议**：建模板，但标注"待三件套实践确认延续后再正式推广"。

#### ➕⑥ `retrospective`（复盘）

- **为什么要**：形态与其它家族**完全正交**——`一句话 → 时间线 → 根因表(R1..Rn) → 教训 → 现在的正确形态`。它在每次走错路时复发（seam-misstep、action-plan-rewrite-required 等），是**团队的学习化石**。模板极便宜，recall 价值高。
- **覆盖范围**：一个骨架同时覆盖"短的失误化石"（BNX7）与"长的、对 owner 指令的内省式复盘+重设计"（MCS1-MCS2-introspect）。

### 4.4 明确"归并不另立"清单（同样重要）

| 候选 | 归宿 | 理由 |
|------|------|------|
| **review**（≈108） | `code-review.md` + `code-review-eval.md` + `code-review-respond.md` | 已有模板；采样里 design/action-plan/charter 评审已 1:1 复用 code-review 骨架（0–5 段脊 + severity/type/blocker finding schema + done/partial/missing 对齐表 + 回应回路）。**无需新 eval 模板**。 |
| **pre-charter-qna**（≈12） | `qna.md` | 逐字实例化 qna.md（标准朝向"GPT 提案+Opus second-opinion"与身份反转朝向"Opus 提案+GPT second-opinion"两版都用到了）。**唯一增量**：冻结后会长出"§业主裁决摘要·一致性审查·冻结声明"尾段——建议给 qna.md 加一个**可选的 freeze-declaration 尾块**即可。 |
| **investigation（外部 CLI）**（≈17） | `investigation.md` | 已有；研究对象=外部参考，与 gap-study 方向相反。 |
| **spike-design**（≈9） | `design.md` | 结构上就是通用 design-sketch（讨论对象/定位/架构稳定性/tradeoff/in-scope/QNA/verdict）+ 内嵌 QNA freeze；"spike"是载荷不是文档类型。 |
| **evidence-pack**（≈18） | `closure.md`（默认）或薄 `code-evidence` 模板 | 承重特征是"可引证、可复现的本仓真相"（file:line / 命令→结果 / UUID/commit 锚），与 closure 的证据段高度重叠。**建议默认折进 closure**；若 owner 觉得"非收口时刻也常写证据包"，再单立一个薄 `code-evidence`。 |
| **debt-ledger**（≈1–3） | `state-analysis` 的 **debt profile** | 评分债务台账近似 state-analysis 的回看清单；做成 profile 而非独立模板，**控制模板数量膨胀**。owner 若认为债务盘点足够独立，可提升为单独模板。 |

### 4.5 数量抉择：给 owner 一个三档光谱

| 档位 | 模板集 | 优点 | 缺点 |
|------|--------|------|------|
| **最小（owner 原案，3 个）** | general-purpose / feasibility-study / state-analysis | 心智负担最低 | **最大的无模板家族 gap-study(42)** 仍漂移；reference-anchor/retrospective 无家可归 |
| **推荐（6 个）★ 我的选择** | 上述 3 + **gap-study** + **reference-anchor** + **retrospective** | 覆盖到所有"高频或形状独特"的家族；长尾仍由 general-purpose 兜底 | 比 3 个多 3 份模板维护 |
| **最大（8–9 个）** | 上述 6 + 独立 `code-evidence` + 独立 `debt-ledger`（+ 可能 panel-review 变体） | 每个家族都有家 | 模板增殖、低频模板可能没人用、侵蚀 eval 的灵活性 |

**我推荐"6 个"**：它正好卡在"治理高频/高独特家族"与"不让模板增殖扼杀灵活"之间。`code-evidence` 与 `debt-ledger` 先做成既有模板的 profile，等体量长起来再提升。

---

## 5. 每个推荐模板的骨架草案（让推荐可落地）

> 仅列**必备段**，供 owner 评估"每个模板会长什么样"。细节待 owner 拍板模板数量后再填。

**通用头部（所有 eval 模板共享）**：对象 / 日期 / 作者（+panel 位）/ **文档性质标签（含"本文不是 X"声明）** / 输入权威源 / 文档状态。  *（落实 §1.3 的 panel 约束：作者身份 + 可选 second-opinion/round-trip 槽。）*

| 模板 | 必备段（脊梁） |
|------|----------------|
| **general-purpose** | 头部+性质声明 → TL;DR → 上游输入锚定 → in/out scope → 命名相位/工作簇 → 逐簇工作台账 → DAG(关键路径) → owner 决策门 → 风险册 → 建议+一句话+修订史 |
| **feasibility-study** | 头部(+`Decision affected: Q__`) → 假设/问题 → 现状/锚点表 → **试了什么（未跑要声明）** → 结果（数字 *或* 分类矩阵）→ 风险×缓解 → **verdict token** → 残余风险/硬前置 |
| **state-analysis** | 头部(+"非 closure/verdict")→ 水位一句话 → 回看清单(价值/deferred/逐项评级) → 归因/缺口(根因缝/覆盖/over-under-claim) → verdict(价值-债务/达成度) → 前瞻交接(reopen 触发+下一周期) →(可选)复现命令 + 修订史。**profiles**：water-level / debt-ledger |
| **gap-study** | 头部(+investigation-type/scope-fence)→ verdict-first → 方法与可采信证据基线 → **body（轴自选：subsystem/API/问题/单参考标尺）** → 编码盲点台账{id,severity,file:line,impact} →(可选)参考对比矩阵 → 优先级建造{优先级,项,工作量/工作块,依赖} → 收尾 verdict + charter 交接 |
| **reference-anchor** | 头部 → 读法/图例(✅🔶⛔🆕)+置信分层 → 逐主题轴锚定矩阵(path:line/URL + verdict) → 反例坑表 → 净新表 →(web 来源台账)→ 核验记录 → **substrate-fit / 技术路线(TR) 过滤复核** → 修订史 |
| **retrospective** | 一句话 → 时间线 → 根因表(R1..Rn) → 教训 → 现在的正确形态 →(长版加：接受批评 / 失败模式定位 / 重设计 / 对比矩阵) |

---

## 6. 边界与易混淆点（模板说明里必须写清）

1. **investigation vs gap-study vs general-purpose**（最易混的三方）：
   - investigation = 研究**外部 CLI 本身**（对象=参考）；
   - gap-study = 以参考为标尺研究**我方缺口**（对象=nano-agent）；
   - general-purpose = **提案阶段范围**（前瞻、冻结零决策）。
2. **state-analysis vs retrospective vs debt-ledger**：
   - state-analysis = 回看**交付的代码/水位现状**；
   - retrospective = 回看**一次决策失误**（时间线+根因，不是代码现状）；
   - debt-ledger = 盘点**要还的债 + 评分排序**（state-analysis 的 profile）。
3. **reference-anchor vs design**：reference-anchor 只产出"借鉴台账 + substrate 过滤"，**不做设计决策**；它喂 design，不替代 design。
4. **任何 planning eval vs charter/action-plan**：见 §2.2——**模态判别**：eval 提案/冻结零、charter 冻边界、design 冻决策+写验收、action-plan 排序+执行。

---

## 7. 风险与落地建议

### 7.1 风险

| 风险 | 判断 | 缓解 |
|------|------|------|
| 模板增殖、低频模板没人用 | medium | 用 §4.1 的判据守门；evidence/debt 先做 profile 不独立；reference-anchor 标"待实践确认" |
| 模板压死 eval 的灵活性 | medium | general-purpose 设计成**轻+模块可删**；gap-study 的 body 轴**作者自选不写死** |
| panel/round-trip 用法与模板打架 | high（78% 有 -by- 标记） | 每个模板预留**作者/panel 身份槽 + 可选回应段**；把 qna 的逐 Q 块抽成**可内嵌子组件**（design/spike 已在内嵌它） |
| 与既有模板边界不清，被误用 | medium | 每个模板头部强制"**本文不是 X**"声明 + §6 的划界表写进模板说明 |

### 7.2 落地建议（若 owner 批准"6 个"）

1. 先落 **gap-study + state-analysis + general-purpose**（覆盖 ≈98 份无模板存量，性价比最高）。
2. 再落 **feasibility-study + retrospective**（形状清晰、便宜）。
3. **reference-anchor** 最后落，并标注"待设计三件套实践确认延续"。
4. 给 `qna.md` 加可选 **freeze-declaration 尾块**；把 qna 逐 Q 块标注为**可内嵌组件**。
5. evidence → 暂折进 `closure.md`；debt → 暂作 `state-analysis` 的 profile；二者体量长起来再提升为独立模板。

---

## 8. 一句话结论与给 owner 的决策问题

**一句话**：eval 天然多型是对的，但"全无模板"让最大的几个家族在反复漂移；我建议做 **6 个 eval 模板**（owner 的 general-purpose / feasibility-study / state-analysis + 我加的 gap-study / reference-anchor / retrospective），其余（review/qna/investigation/spike-design/evidence/debt）**归并进既有模板或作 profile**，并把 §2.2 的"模态判别"写进所有模板说明，顺带消解 design/action-plan 的角色疑虑。

**给 owner 的 3 个决策问题**：

1. **数量档位**：采纳"推荐 6 个"，还是回到"最小 3 个"或"最大 8–9 个"？（我推荐 6）
2. **gap-study 是否新建**：这是最大的无模板家族（≈42），我强烈建议单立；owner 是否同意它与 investigation/general-purpose 三方分立？
3. **evidence 与 debt 的处置**：同意先作 closure / state-analysis 的 profile（不独立），等体量长起来再提升——还是现在就独立成模板？

---

## 附录 A · 调查覆盖

- 全量统计：397 eval / 175 design / 204 action-plan 文件名模式 + 署名分布。
- 深读采样（6 路并行子代理，≈50 份）：
  - review：web-v60 design/charter/action-plan-reviewed-by-opus、PE design/action-plan-reviewed、PP full-scan、MC review-ledger、context-structure-reviewed-by-GPT、Z0-ZX design-reviewed。
  - state-analysis：MCX4 / MC8 / MIX3 / water-level(MIX3/PEX5/BSSB6) / BNX5 / PPX11 / what-to-do-after-MCS2。
  - gap-study：api-gap-study / llm-wrapper-study / agentic-loop-api-study / mc-investigation-01·02 / agent-core-analysis / api-enhance / audit-and-reporting-study / claude-code-compared。
  - planning：MCCM initial·proposed / MCX initial·proposed / BN-work-inclusions / PP initial·re-planning / MI-initial-thoughts / MIX scope-analysis。
  - feasibility+evidence：wrangler-dev-feasibility / mjs-to-ts-prototype / llm-contract-extraction / web-sdk-gap / realized-code-evidence / external-contract-surface / cf-agent DO 对比 / cf-agents-session-memory / first-real-run-evidence。
  - qna/spike/debt/anchor：MCX/MCCM/web-v60 pre-charter-qna / BNX7-retrospective / debt-repayment-analysis / MI-S2-new-spikes-design / MCS1-MCS2-introspect / MCX3-MCX4-reference-anchor。

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：397-eval 全量分型 + 6-模板推荐 + design/action-plan 角色澄清 |
| v0.2 | 2026-05-30 | Opus 4.8 | 增补：内容台账（共有/独有矩阵）+ 逐项价值分析 + wave 化执行方案（§9–§11 + 附录 C） |
| v0.3 | 2026-05-30 | Opus 4.8 | 增补：eval↔design 边界发现——"design 寄生在 eval/"的检测方法、量化、三形态、治理判断与对策（§12–§18 + 附录 D 检测脚本）；催生 `design-sketch.md` |

---

# 增补（v0.2）：内容台账 · 价值分析 · 执行方案

> 本增补回应 owner 追加要求：把 **owner 的 3 个 + 我加的 3 个** 共 6 个 eval 模板，拆到**内容（章节/组件）粒度**，做一张台账说明哪些内容是**共有**、哪些是**独有**，逐项 reasoning 其价值，并给出**更具体的执行方案**。
>
> 列含义：**GP**=general-purpose（owner）· **FS**=feasibility-study（owner）· **SA**=state-analysis（owner）· **GS**=gap-study（我加）· **RA**=reference-anchor（我加）· **RE**=retrospective（我加）。
> 单元格：**●**=必备段 · **○**=可选段 / profile · **—**=不含。

## 9. 共有 / 独有 内容台账

> 一个根本性的设计判断先写在前面：**6 个模板不是 6 套独立结构，而是「1 条共有脊 + 6 个独有差异块」的装配模型。** owner 的 3 个与我加的 3 个**共用同一条脊（A 组）**，只在各自的独有块上分叉。这意味着我追加的 3 个模板，**增量成本只有它们的独有块，不是 3 套完整模板**。

| 组 | 内容组件 | GP | FS | SA | GS | RA | RE | 归属 | 价值 |
|----|----------|----|----|----|----|----|----|------|------|
| **A 共有脊** | A1 通用头部（对象/日期/作者+panel/状态/权威输入） | ● | ● | ● | ● | ● | ● | **共有 6/6** | 高 |
| | A2 性质免责声明（"本文不是 charter/closure/design/action-plan"） | ● | ● | ● | ● | ● | ● | **共有 6/6** | 高 |
| | A3 TL;DR / verdict-first / 一句话结论 | ● | ● | ● | ● | ○ | ● | **共有 5–6** | 高 |
| | A4 上游输入锚定（file:line / 文档链接） | ● | ● | ● | ● | ● | ● | **共有 6/6** | 中 |
| | A5 修订历史 | ● | ○ | ● | ○ | ● | ○ | **共有（建议全收）** | 中 |
| **B 规划模块** | B1 in/out scope（含 scope-fence） | ● | — | ○ | ○ | — | — | **GP 主 / 半共有** | 高 |
| | B2 命名相位 / 工作簇列表 | ● | — | — | — | — | — | **GP 近独有** | 高 |
| | B3 逐簇工作台账（id/项/来源/复用-净新/规模/风险） | ● | — | ○ | — | — | — | **GP 主** | 高 |
| | B4 DAG（关键路径 + 并行窗） | ● | — | ○ | — | — | — | **GP 主** | 中 |
| | B5 owner 决策门 / 开放问题 | ● | ● | ○ | — | — | — | **半共有（GP+FS）** | 高 |
| | B6 风险册 | ● | ● | ● | ○ | — | ○ | **半共有** | 中 |
| | B7 建议 / 下一步 | ● | ● | ● | ● | ○ | ● | **半共有** | 中 |
| **C SA 独有** | C1 回看清单（价值 / deferred / 逐项评级矩阵） | — | — | **●** | — | — | — | **独有 @SA** | 高 |
| | C2 对账诚实（over/under-claim · frozen≠done · 假零猎杀） | — | — | **●** | — | — | — | **独有 @SA** | **极高** |
| | C3 前瞻交接（deferred + reopen 触发器 + 下一周期） | — | — | **●** | — | — | — | **独有 @SA** | 高 |
| | C4 [profile] 水位 / 桶评级（D/W/E + runtime） | — | — | ○ | — | — | — | **独有 @SA(profile)** | 中 |
| | C5 [profile] 债务评分台账（内聚/紧急/复杂/风险/价值，吸收 debt） | — | — | ○ | — | — | — | **独有 @SA(profile)** | 中 |
| **D FS 独有** | D1 `Decision affected: Q__` + verdict token | — | **●** | — | — | — | — | **独有 @FS** | 高 |
| | D2 "试了什么 / 未跑要显式声明"诚实段 | — | **●** | — | — | — | — | **独有 @FS** | 高 |
| | D3 结果（原型数字 **或** 分类/缺口矩阵） | — | **●** | — | — | — | — | **独有 @FS** | 中 |
| | D4 残余风险 / 硬前置条件 | — | ● | ○ | — | — | — | **FS 主 / 半共有** | 中 |
| **E GS 独有** | E1 编码盲点/断点台账 {id, severity, file:line, impact} | — | — | — | **●** | — | — | **独有 @GS** | 高 |
| | E2 body 轴自选（subsystem / API / 调查问题 / 单参考标尺） | — | — | — | **●** | — | — | **独有 @GS** | 高 |
| | E3 优先级建造 {优先级, 项, 工作量/工作块, 依赖} | — | — | ○ | **●** | — | — | **GS 主** | 高 |
| | E4 参考对比矩阵（vs claude-code/codex/gemini-cli/cf-agents） | — | — | — | ○ | ○ | — | **GS/RA 共享** | 中 |
| **F RA 独有** | F1 axes×sources 锚定矩阵 + verdict 图例（✅借/🔶部分/⛔反例/🆕净新） | — | — | — | — | **●** | — | **独有 @RA** | 高 |
| | F2 置信分层（context-line / HEAD / web-high/low） | — | — | — | — | **●** | — | **独有 @RA** | 中 |
| | F3 反例坑表 + 净新表 | — | — | — | — | **●** | — | **独有 @RA** | 中 |
| | F4 substrate-fit / 技术路线（TR-1..10）过滤复核 | — | — | — | — | **●** | — | **独有 @RA** | **高** |
| | F5 核验记录（path:line / URL 逐条可核） | — | — | — | — | ● | — | **RA 主** | 中 |
| **G RE 独有** | G1 时间线（误判→纠偏） | — | — | — | — | — | **●** | **独有 @RE** | 中 |
| | G2 根因表（R1..Rn） | — | — | — | — | — | **●** | **独有 @RE** | 高 |
| | G3 教训 / 现在的正确形态 | — | — | — | — | — | **●** | **独有 @RE** | 高 |
| | G4 [长版] 接受批评 / 失败模式定位 / 重设计 | — | — | — | — | — | ○ | **独有 @RE(长版)** | 中 |

**台账读出的三条结论**：

1. **共有脊（A 组）= 5 个组件 × 6 模板**：这是写一次、所有模板复用的部分。**把它抽成单一来源，是整个再设计里性价比最高的一步**（一次投入，消除 397 份 eval 头部的长期漂移，并通过 A2 的"本文不是 X"声明直接根治 §2.2 的模态混淆）。
2. **GP 几乎只由 A 组 + B 组装配而成**——它本身没有多少"独有"组件（只有 B2 接近独有）。这印证 §4.2 的判断：**general-purpose 应当 = 共有脊 + 规划模块的默认装配，不是另造结构**。
3. **每个"该独立"的模板都通过了"独有充要条件"检验**：SA 有 C 组、FS 有 D 组、GS 有 E 组、RA 有 F 组、RE 有 G 组，且这些独有块都是 GP 无法在不丢脊梁的情况下托管的。**反向验证了归并决策**——evidence / debt / spike-design / pre-charter-qna 对照 closure/SA/design/qna **拿不出非空的独有块**，所以正确地被归并而非独立（见 §9 末"充要条件"框）。

> **模板存在的充要条件（治理规则，建议写进模板说明）**：
> **一个内容集合只有在拥有 ≥1 个「非空、且无法被 general-purpose/既有模板托管」的独有必备段时，才配独立成模板；否则降级为某既有模板的 profile。**
> 这条规则同时解释了"为什么加 GS/RA/RE"（各有独有块）与"为什么不加 evidence/debt/spike-design"（独有块被 closure/SA/design 吸收）。

## 10. 每项内容的价值分析与 reasoning

> 价值 = **频率（写多少次）× 防漂移（标准化能挡掉多少复发错误）× 不可替代性（GP 能否托管）**。下面按组给出 reasoning 与"缺失会怎样"。

### A 组 · 共有脊 —— 价值：高（杠杆最大）

- **频率**：每份 eval 都写（×397），是出现频次最高的内容。
- **防漂移**：A2「性质免责声明」是**唯一能从源头根治模态混淆的组件**——它强制每份 eval 在文首声明"冻结零决策、不是 charter/design/action-plan"，正是 §2.2 里 owner 疑虑的解药。A1/A4 标准化输入锚定，让 review/handoff 能稳定引用。
- **不可替代性**：本就是所有模板共用，抽出来零损失。
- **缺失会怎样**：eval 继续被误当 charter/closure 用（历史上已发生，多份文件不得不手写"本文不是 X"自我澄清）；引用关系漂移。
- **reasoning 结论**：**第一优先级实现**。一次投入，全局收益。

### B 组 · 规划模块 —— 价值：高（GP 的本体）

- **频率**：planning 类 eval ≈33 份，且是 charter 前的常规动作。
- **防漂移**：B2/B3/B5（命名相位 + 工作台账 + owner 决策门）标准化后，"提案"与"charter/action-plan"的模态边界更清晰；B5 把 owner 决策**显式列为 OPEN**，避免 eval 偷偷冻结决策。
- **不可替代性**：B 组就是 GP 的承重结构，无法外移。
- **缺失会怎样**：每份 planning eval 重新发明相位/DAG/决策门的表达，owner 每次都要重新适应不同结构。
- **reasoning 结论**：**与共有脊一起进 Wave 1**，构成 GP。

### C 组 · SA 独有 —— 价值：极高（C2 是全文最值钱的纪律）

- **C2 对账诚实** 是整个 state-analysis 存在的理由：**它专挡"声称价值 vs 真实代码"的偏差**（over/under-claim、frozen≠done、占位/假零）。这正是采样中 MC8/MIX3 状态分析反复抓出的 bug 类。**没有 C2，SA 就退化成一份普通回顾，失去它最独特的价值。**
- **C1/C3**：回看清单给"交付了什么"一个稳定快照；前瞻交接（含 reopen 触发器）保证 deferred 项不被静默吞掉——这是周期之间不丢账的关键。
- **C4/C5 profile**：把 water-level 与 debt-ledger 做成 SA 的 profile，**用一个模板吸收两个低频家族**，是控制模板数量的关键手筋。
- **缺失会怎样**：里程碑之间债务静默累积、价值被夸大、下一周期基于错误的"已完成"假设开工。
- **reasoning 结论**：SA 进 Wave 1；C2 是其灵魂必备段。

### D 组 · FS 独有 —— 价值：高（低频但高风险 gate）

- **频率低（2 份）但每份都 gate 一个 charter 决策**——决策一旦走错，下游一整条 design/action-plan 跟着错。
- **D1 verdict token + D2 诚实段** 是核心：D2「未真跑要显式声明」**专防"可行性表演"**（没跑就宣称可行）。采样中 deferred-measurement 表/"static analysis"框定是反复出现的诚实模式，值得固化。
- **不可替代性**：go/no-go 的 token 化结论 + 决策绑定，GP 的"建议"段无法替代（GP 不 gate 单个决策）。
- **缺失会怎样**：feasibility 沦为乐观叙事，charter 基于未验证假设拍板。
- **reasoning 结论**：Wave 2；模板很薄但必须强制 D1/D2。

### E 组 · GS 独有 —— 价值：高（最大存量的承重件）

- **频率最高的无模板家族（≈42）**，单这一点就让 GS 的标准化收益最大。
- **E1 编码盲点台账（带 file:line）** 是 gap-study 的产出本体——它是喂给 charter 的"我方缺什么"清单；**E2 body 轴自选** 保留了 gap-study 必须的灵活（不同调查按 subsystem/API/问题/单参考 切片），同时锁住脊梁。
- **不可替代性**：方向与 investigation（研究外部）、GP（提案范围）都不同，三方不可互替（§6）。
- **缺失会怎样**：最大的一类 eval 继续各写各的，缺口清单格式不一，charter 难以稳定消费。
- **reasoning 结论**：Wave 1；优先级与 GP/SA 并列。

### F 组 · RA 独有 —— 价值：中（低频但 F4 不可替代）

- **频率低（2 份，且是新近实践）**，所以整体价值定"中"。
- **F4 substrate-fit / 技术路线过滤** 是真正的价值点：**它是阻止"盲目照抄参考"的闸门**——把借来的机制按 nano-agent 技术路线（TR-1..10）降级/重映射（与既有记忆"reference-anchor 必须用技术路线过滤 reference，机制≠思路"一致）。F1 的 verdict 图例让"借/部分/反例/净新"判断可核。
- **不可替代性**：axes×sources 矩阵 + TR 过滤的形状极特化，GP 托不住。
- **缺失会怎样**：参考借鉴退回口头判断，容易把"思路"误抄成"机制"。
- **reasoning 结论**：Wave 3，**标 provisional**——待"设计三件套"（initial-planning→reference-anchor→pre-charter-qna）确认为稳定实践后再正式推广。

### G 组 · RE 独有 —— 价值：中（便宜 + 高 recall）

- **频率最低（≈2–3）**，但模板**极便宜**（4 个短段）。
- **G2 根因表 + G3 教训** 把每次走错路**固化成可检索的学习化石**——recall 价值随时间复利。
- **不可替代性**：它分析"一次决策失误"而非代码现状（≠SA）也非制品评审（≠review），无处可归。
- **缺失会怎样**：教训散落在长文里，下次同类失误重犯。
- **reasoning 结论**：Wave 2，和 FS 一起做（都便宜、形状清晰）。

### 价值排序速览（用于排执行优先级）

| 价值档 | 组件 | 落点 |
|--------|------|------|
| **极高** | A2 性质声明、C2 对账诚实 | 必做，越早越好 |
| **高** | A1/A3 头部+TL;DR、B1/B2/B3/B5 规划核心、C1/C3、D1/D2、E1/E2/E3、F4、G2/G3 | Wave 1–2 主体 |
| **中** | A4/A5、B4/B6/B7、C4/C5、D3/D4、E4、F1/F2/F3/F5、G1/G4 | 随模板顺带，或 profile/可选 |

## 11. 更具体的执行方案分析

### 11.1 总策略：先脊后块，存量优先

由台账得到的装配模型直接决定执行顺序：

> **先把共有脊（A 组）抽成单一来源 → 再按"存量大小 × 价值"顺序补各模板的独有块。** 每个模板 = 脊 + 它的独有块；不重复造脊。

### 11.2 Wave 化路线图

| Wave | 动作 / 模板 | 内容构成（脊 + 独有块） | 工作量 | 依赖 | 覆盖存量 | 验收 |
|------|-------------|--------------------------|--------|------|----------|------|
| **0 · 前置** | 抽共有脊 + 写模态判别 | A1–A5 抽成 `_eval-common-header`（约定/snippet）；§2.2 模态判别 + §6 划界写进"模板说明" | **S** | 无（全局前置） | 影响全部 397 | 脊可被任一模板引用；A2 声明就位 |
| **1 · 存量优先** | **GP** | 脊 + B1–B7 装配 | **M** | Wave 0 | ≈33 planning | 能直接重写 1 份历史 planning（dogfood） |
| | **SA** | 脊 + C1–C3（必备）+ C4/C5 两个 profile | **M–L** | Wave 0 | ≈23 state/water-level（+吸收 debt） | C2 对账诚实段非空；water-level profile 能套 1 份历史 |
| | **GS** | 脊 + E1–E3（必备）+ E4 可选 | **M** | Wave 0 | ≈42 study/gap（最大） | E1 台账带 file:line；body 轴可三选一 |
| **2 · 便宜清晰** | **FS** | 脊 + D1–D4 | **S** | Wave 0 | ≈2（高风险 gate） | 强制 D1 token + D2 诚实段 |
| | **RE** | 脊 + G1–G3（+G4 长版可选） | **S** | Wave 0 | ≈2–3 | 短/长两版各套 1 份历史（BNX7 / MCS1-MCS2-introspect） |
| **3 · 前瞻** | **RA**（标 provisional） | 脊 + F1–F5 | **M** | Wave 0；三件套实践确认 | ≈2（新实践） | F4 substrate/TR 过滤段非空 |
| **配套** | qna.md 增强 | 加可选 freeze-declaration 尾块；逐 Q 块标为**可内嵌组件** | **S** | 无 | 12 qna + 被 design/spike 内嵌 | design/spike 能 `引用` Q 块而非复制 |

工作量粗估：**Wave 0 ≈ S；Wave 1 ≈ M+M+ML（主体投入）；Wave 2 ≈ S+S；Wave 3 ≈ M；配套 ≈ S。** 即"一个 S 起步 + 三个中量模板（GP/SA/GS）+ 三个轻量收尾（FS/RE/RA）+ 一个 S 配套"。

### 11.3 关键依赖与排序理由

- **Wave 0 是硬前置**：所有模板都引用共有脊；先抽脊避免在 6 个模板里把头部抄 6 遍（否则脊本身就漂移，自我打脸）。
- **Wave 1 选 GP/SA/GS 而非别的**：纯按存量——三者合计覆盖 ≈98 份无模板 eval（占无模板存量的绝大多数），ROI 最高；且 GP 是长尾兜底，必须先于"把长尾往 GP 塞"的预期落地。
- **RA 放 Wave 3 且 provisional**：它低频且依赖一个尚未确认会延续的实践（设计三件套）。**过早固化低频模板是 §7.1 的明确风险**——先观察，确认延续再推广。
- **FS/RE 放 Wave 2**：形状清晰、模板薄、便宜，但不抢 Wave 1 的存量优先级。

### 11.4 每个模板的统一验收门（dogfood 强制）

每个模板**冻结前必须满足**：

1. **独有块非空**：至少有 1 个独有必备段被实际填写，且与 GP 明显区分（否则按充要条件降级为 profile）。
2. **头部含 A2 性质声明**：显式写"本文不是 charter/design/action-plan/closure"。
3. **划界入说明**：§6 的易混淆边界写进该模板的使用说明（如 GS 必须写清 vs investigation/GP 的三方区别）。
4. **历史回填验证（dogfood）**：用 ≥1 份既有 eval 套该模板跑通，证明模板能容纳真实内容而非空想结构。
   - GP→某份 `initial-planning`；SA→`state-analysis-after-MCX4`；GS→`api-gap-study`；FS→`wrangler-dev-feasibility`；RA→`MCX3-MCX4-reference-anchor`；RE→`BNX7-seam-misstep-retrospective`。

### 11.5 落地后的度量与回收机制

- **挂标签**：新写的 eval 必须在头部声明所属模板类型（含 `general-purpose`）。
- **长尾健康度**：3 个月后统计"无模板可挂、只能进 general-purpose"的 eval 比例——比例过高说明分型不足，过低说明 GP 过度兜底。
- **低频回收**：6 个月内实例 <2 的模板（重点盯 RA/FS/RE），降级为 GP 或既有模板的 profile，**防止模板坟场**。

### 11.6 给 owner 的执行决策点（在 §8 三问之外）

1. **是否采用"先脊后块"装配模型**（共有脊抽成单一来源）——这是把 6 个模板成本降到"1 脊 + 6 差异块"的关键，我强烈建议采用。
2. **Wave 1 是否锁定 GP/SA/GS**（按存量 ≈98 份优先），把 FS/RE/RA 放后面？
3. **RA 是否接受 provisional 标记**（待设计三件套确认延续再正式推广），还是现在就正式化？

---

## 附录 C · 台账方法说明

- **组件来源**：§5 的 6 份骨架草案 + 6 路子代理回报的"ALWAYS/SOMETIMES present"段位判定。
- **●/○/— 判定依据**："该段在该家族采样中是否普遍出现"——普遍=●，偶现/profile=○，不出现=—。
- **价值评级依据**：频率（§1.2 体量）× 防漂移（该段标准化挡掉的复发错误类）× 不可替代性（GP 能否托管）。
- **充要条件检验**：对 evidence/debt/spike-design/pre-charter-qna 逐一验证"是否存在无法被 closure/SA/design/qna 托管的独有必备段"，结论为否 → 归并（与 §4.4 一致）。

---

# 增补（v0.3）：eval↔design 边界 —— "design 寄生在 eval/"的检测、发现与对策

> 本增补回应 owner 的观察："有时一份 eval 文件会在本体内直接演化成 design 文件，这在过去发生了很多次。" 我设计了一种可复现的检测方法，扫了全部 397 份 eval，确认了现象、量化了频率、并把"演化"拆成三种真实形态。结论催生了一个新模板 `docs/templates/design-sketch.md`。
>
> **为什么持久化进本文**：这是 eval↔design 边界治理的事实基线 + 可复跑方法，属于 §2.2（模态判别）与 §4.4（spike-design 归并）的实证补全；未来任何关于"eval/design 是否该合并/分流"的讨论都应以本节为锚。

## 12. 触发问题

design 文档与 eval 文档的用途有时重叠：一份 eval 会在本体内（或沿其谱系）长成 design。需要一种**可复现的方法**把这些文件找出来，判断是良性短路还是治理漂移。

## 13. 检测方法（可复现，三步指纹法）

design 有一套 `design.md` 独有的**结构指纹**，正常 eval 不该携带。检测：

1. **结构指纹打分**：对 `docs/eval/**` 每个文件，统计 15 个 design 专属标记命中数——`架构稳定性与未来扩展` / `In-Scope 功能详细列表` / `可验证的验收条件` / `一句话收口目标` / `核心取舍·Tradeoff` / `Value Verdict` / `接口保留点·完全解耦点·聚合点` / `本设计` / `功能簇定义` / `一句话定位陈述` / `在 nano-agent 中的定位` / `关键术语对齐`。命中 **≥7** ≈ 携带完整 design。
2. **模态判别器**：加 `本设计` 自指、`文档状态: frozen`（eval 本应"冻结零"）、标题含 `设计/design`；用名字含 `reviewed-by` 剔除"评审 design 的 eval"这类 false positive。
3. **`docs/design/` 交叉比对**：候选在 `docs/design/` 是否有同簇对应文件——无 → 是"困在 eval/ 的事实 design"（治理漂移）。

> 完整脚本见**附录 D**，可直接接入 `docs:check`。

## 14. 量化：发生频率

| 信号 | 数量（/397） | 解读 |
|------|--------------|------|
| eval 标题含 `设计/design` | 43 | 含 review/analysis，需筛 |
| eval 正文 `本设计` 自指 | **16** | 较干净 |
| eval 标 `文档状态: frozen` | **34** | frozen 是 design/charter 模态；含部分合法 qna register |
| eval 指认 `母本` | 3 | 显式"从某 eval 演化而来" |
| 指纹 ≥10（近乎完整 design） | **8** | 见 §15 名单 |
| 手工确认的事实 design | **~10–12** | 见 §15 |

> 校准：34 个 frozen 里含合法的 pre-charter-qna（冻结 Q 是正当的）；最干净的"design 寄生"信号是 `本设计`(16) + 标题自称设计且非 review 的那批(~12)。

## 15. 名单：困在 eval/ 的事实 design（`docs/design/` 查无此人）

| 文件（`docs/eval/` 下） | 状态 | 性质 |
|------|------|------|
| `more-intelligence/spikes/MI-S2-new-spikes-design.md` | frozen + owner QNA §12 | spike 测试设计 |
| `more-intelligence/spikes/MI-S3-more-spikes-design.md` | — | spike 设计 |
| `more-intelligence/MIX7-design-clean-value-cutoff.md` | frozen + owner | 收束阶段设计 |
| `more-intelligence/MIX-wave-2/MIX4—MIX6-flexible-and-resilient-cores.md` | frozen | **运行时协议核设计**（非测试） |
| `more-intelligence/MIS2-bash-fake-further.md` | frozen，标题=`设计 + Eval` | 能力设计（自承双重身份） |
| `more-capabilities/spike-analysis/revised-v2-spike-expansion-design-by-opus.md` | frozen v0.4 + 外置 QNA register | 双层测试架构设计 |
| `more-capabilities/spike-analysis/after-MCX2-spike-expansion.md` | **draft，QNA 自答，已被 reject** | 测试设计（被上一行取代） |
| `more-capabilities/context-defending/MCX5-context-resiliance-design.md` | draft，母本=rotting-prevention | 韧性设计 |
| `product-enhancement/spike/P0-P1-high-value-fixes-analysis-by-opus.md` | — | "PEX5 阶段设计提案" |
| `pro-to-product/before-launch/analysis-after-PPX7-by-opus.md` | — | "Test Taxonomy Redesign + 新阶段规划" |
| （母本）`more-capabilities/context-defending/rotting-prevention-by-opus.md` | research，§10 长出 design 尾巴 | **最接近"本体内演化"的标本** |

**关键事实**：上述无一在 `docs/design/` 有对应文件（`docs/design/more-intelligence/` 只有 MID1–7，`more-capabilities/` 只有 MCD1–7）——它们是**永久停在 eval/ 的事实 design**。其中 **MIX4-6 是运行时协议核设计**，躺在 eval/ 最危险。

## 16. 三种真实形态（对 owner 直觉的诚实修正）

owner 的直觉"eval 在本体内演化成 design"是对的——design 内容确实大量寄生在 eval/。但深读后要说得更准：**纯粹"单文件内从 eval 渐变为 design"是少数**，真实分三种：

- **形态 A — 天生就是 design，只是错放在 eval/（最主流）**：MI-S2 / MIX7 / MIX4-6 / revised-v2。从标题（"功能簇设计"）到结尾全程 design 模态，套满 `design.md` 模板，frozen + owner QNA；把 water-level/state-analysis 当**上游输入**引用，自身不是 eval。eval/ 只是存放位置。
- **形态 B — 研究型 eval 长出 design 尾巴，再裂变出子 design（真正的"演化"，跨两文件）**：`rotting-prevention-by-opus.md`（自称"开发性研究，不是 charter/design"）§0–§9 纯 eval，**追加的 §10（owner 裁决触发）突然结晶**成 `CREATE TABLE nano_context_observations` schema + 5 条冻结判据 C1–C5 + emit 点 file:line；这块 §10 随后被抽出另立 `MCX5-...-design.md`，后者明写前者是"**直接母本**、v0.1 基于母本 §10 成稿"。**最接近 owner 所说的"本体内演化"**，演化点（§10）就在那份研究 eval 体内。
- **形态 C — 自承"设计 + Eval"双重身份（诚实混血）**：`MIS2-bash-fake-further.md` 标题直写"设计 + Eval"，design 骨架里 §0.3/§6.4 嵌入 **live 真实语料实测的"桶水位"岛**（8.7%→40.8%→69.9% + 复现命令）。
- **反向小料**：MIX4-6 frozen 之后因 owner 否决又追加 **eval 复盘 §11**——design 长出 eval 尾巴，方向相反。

## 17. 治理判断（最该被看见）

**在 eval/ 文件夹里，"eval 草稿"与"权威 design"的分界线，不是正文结构，而是「embedded QNA 是否走了 owner 裁决」。**

- 铁证：`after-MCX2-spike-expansion.md` 把 QNA **自答**（`答复来源=本设计`，无 `业主回答`）→ 永停 `draft` → 被 reject；`revised-v2` 把 QNA **外置到正规 register + owner 裁决** → `frozen`。后者 §9.1 明确点名"自答 QNA 违反治理本意"才触发重写。这正是 `qna.md` 纪律的真实代价案例，也与 §5「state-analysis 灵魂=对账诚实」同源。

**真正的 drift**：这些 design-grade 文档**有内容、有 owner 冻结，却没有 `docs/design/` 户口**——规范的 design 真相面被劈成两个文件夹，谁去 `docs/design/` 找 MCX5/spike 治理/MIX4-6 协议核设计都会扑空。

**但要公平**：co-location 是**理性**的，不是手滑——这些 design 的全部工作就是裁决隔壁那份 eval 抛出的 backlog，紧贴证据落笔很自然。问题不在"写在哪"，在"写完没回正规户口、没建索引、没守冻结门槛"。

## 18. 触发模式与对策

### 18.1 什么样的工作会被"在 eval 里做设计"

两类高度集中：① **测试治理 / 水位工作**（MI-S2、MI-S3、revised-v2、after-MCX2、PEX5、PPX7）；② **插曲 / 韧性"X-cluster"核**（MIX7、MIX4-6、MCX5、MIS2-bash）。共同点：**从主线编号设计流水线（MID/MCD…）分叉、紧贴某份分析 eval 的"支线设计"，倾向就地在 eval/ 成文。**

### 18.2 对策（三条，可叠加）

1. **承认 eval/ 是合法"design 孵化区"，但加出区规则（推荐）**：一份 eval 一旦越过 design 阈值——**= owner 裁决过的 embedded QNA + 可验证收口目标**——必须**要么迁去 `docs/design/`，要么在 `docs/design/` 建交叉索引**。阈值用"owner-adjudicated QNA"判定，与 §17 天然分界线一致。
2. **新增 `design-sketch.md` 轻量"支线设计"模板**（吸收 spike/插曲设计）：给支线设计正规模板 + 正规户口字段 + 冻结门槛。**已起草，见 `docs/templates/design-sketch.md`**（本增补的直接产物）。
3. **把检测做成 `docs:check` 的一条 lint**：扫 `docs/eval/**` 里 `本设计` + `文档状态: frozen` 且 `docs/design/` 无对应文件者，告警"design 寄生在 eval"。脚本见附录 D。

### 18.3 与既有结论的关系

- **强化 §4.4**：当时只把 spike-design 归并进 `design.md`；本节证明它不止 spike，而是一整类"支线设计"，故升级为独立的轻量模板 `design-sketch.md`（介于 `eval-general-purpose` 提案 与 完整 `design.md` 之间）。
- **印证 §2.2 模态判别**：这些文件之所以能被 owner 冻结，正因为它们已切换到 design 模态（冻决策+写验收）——它们不是"提案"，所以本就不该停在 eval。

---

## 附录 D · "design 寄生在 eval" 检测脚本（可接入 docs:check）

```bash
#!/usr/bin/env bash
# 扫 docs/eval/** 找出携带 design 结构指纹的文件，并标出在 docs/design/ 无对应户口者。
cd "$(git rev-parse --show-toplevel)"
patterns=(
"架构稳定性与未来扩展" "In-Scope 功能详细列表" "可借鉴的代码位置" "一句话收口目标"
"可验证的验收条件" "在 nano-agent 中的定位" "关键术语对齐" "Value Verdict"
"接口保留点" "完全解耦点" "聚合点" "本设计" "功能簇定义" "一句话定位陈述" "核心取舍"
)
while IFS= read -r f; do
  # 跳过"评审 design 的 eval"（false positive）
  case "$f" in *reviewed-by*|*review*) continue;; esac
  score=0
  for p in "${patterns[@]}"; do grep -qF "$p" "$f" && score=$((score+1)); done
  if [ "$score" -ge 7 ]; then
    frozen=$(grep -ciE '文档状态.*frozen|状态.*frozen' "$f")
    selfid=$(grep -cF '本设计' "$f")
    echo "DESIGN-IN-EVAL(score=$score frozen=$frozen 本设计=$selfid): $f"
  fi
done < <(find docs/eval -name '*.md')
# 阈值 ≥7；frozen>0 且 本设计>0 = 高置信"事实 design"，应有 docs/design/ 户口或交叉索引。
```
