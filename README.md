# Nano-Agent 文档模板体系 —— 索引 · 模块分解 · 统一约定（canonical）

> 本文件是 `docs/templates/` 的**单一权威入口**,有三个用途:
> 1. **模板选择**:按目标快速选中正确的模板或工作流轨道(§1)。
> 2. **模块分解目录**:对每个 active 模板,列出它由哪些模块构成、每个模块**承担什么责任 / 何时填**,以及该模板**何时用 / 何时不用**(§2)。**owner 可据此指令 agent 自行选模板,或跨模板抽取/组合模块。**
> 3. **统一约定(canonical conventions)**:状态词汇、轨道命名、符号图例、核心名词、交叉引用风格的唯一真源(§4)。任何模板与本表冲突,**以本表为准**。
>
> 设计/裁定背景见 `docs/templates/re-design/`(8 份再设计分析)。历史/停用模板见 `docs/templates/legacy/`(§5)。

---

## 0. 怎么用这份 README(给 owner 与 agent)

- **要 agent 自选模板**:让它读 §1 的选择决策树 + §2 各模板的「何时用/何时不用」,自行命中一个模板,并在产物头部声明 `文档性质`。
- **要 agent 组合模块**(分析需求跨越单一模板时):让它读 §2 的模块分解表 + §3 的「模块重组指南」,从不同模板抽取模块拼成骨架,并在产物头部写一行 **`结构来源(dogfood):<模板A 的模块> + <模板B 的模块>`**(已有 3 个真实先例,见 §3.2)。
- **模板是默认骨架,模块是可拆装的零件**。绝大多数工作直接选一个模板即可;只有当一个分析同时要"对照参考 + 深度取舍 + 价值评分"这类跨模板能力时,才组合模块。

---

## 1. 快速选择

### 1.1 选择决策树(先问目标)

```text
你要产出什么?
├─ 还在"想做什么/怎么拆" ─────────────▶ eval 家族(§2.1);选 flavor 看 1.3
├─ 要冻结"阶段边界/退出条件" ─────────▶ charter(重) / charter-lite(轻)
├─ 要冻结"owner 决策" ───────────────▶ qna(唯一真源)
├─ 要写"完工长什么样 + 接缝在哪"(净新/争议)─▶ design-neo(重轨) / design-sketch(combo 内单簇)
├─ 要排"怎么做/何序/怎么测" ──────────▶ action-plan
├─ 要"评审 / 收口 / 回填 / 自检" ─────▶ review·closure·respond 家族(§2.6/2.7)
└─ 要"API 合规 / bug 根因"专科调查 ───▶ api-compliance / bug-analysis-report
```

### 1.2 四轨工作流(详见 `re-design/workflow-tracks.md`)

| 轨 | 进 action-plan 前的文档组合 | 适配 |
|----|------------------------------|------|
| **A 单遍** | `eval-general-purpose` → action-plan | trivial、无契约 |
| **B charter-lite** | `eval`(+ 可选 `eval-reference-anchor`)→ `charter-lite` → action-plan | 小·低模糊·扩展既有·无净新 |
| **C combo ★** | `eval-planning`(三态)+ `eval-reference-anchor` + `qna`(+ `design-sketch` 若一处净新)→ action-plan | sub-phase·≥2 AP·需 grounding |
| **D 重轨** | `eval-gap-study`/`eval-state-analysis` → `charter` + `design-neo`(×N)+ `eval-reference-anchor` + `qna` → action-plan | foundation·净新多·争议架构 |
| **闭环(全轨)** | action-plan→`respond-execution-log`;impl→`code-review`→`code-review-respond`;阶段末→`closure`→`eval-state-analysis`(开下周期) |

**轨道/design 选择**:见 `re-design/workflow-tracks.md` §4 决策树 + 本文 §4.6 的 design-necessity 6 条。

### 1.3 家族索引(active 22)

| 家族 | 模板 | 一句话角色 |
|------|------|------------|
| **eval(7)** | `eval-general-purpose` | 提案"做什么"(兜底骨架)|
| | `eval-planning` | 三态规划(initial→proposed→final)→ 派生多 action-plan |
| | `eval-reference-anchor` | grounding 锚台账(借鉴 verdict + substrate-fit/TR 过滤)|
| | `eval-gap-study` | 我方缺口台账(对照参考找缺什么)|
| | `eval-state-analysis` | 交付快照 + 对账诚实 + 前瞻交接(周期铰链)|
| | `eval-feasibility-study` | go/no-go 探针(token 化结论)|
| | `eval-retrospective` | 失误复盘(时间线 + 根因 + 教训)|
| **charter(2)** | `charter` | 重轨纲领(scope/phase/exit/trigger)|
| | `charter-lite` | 轻 charter + 决策冻结 + design-necessity 闸 |
| **design(3)** | `design-neo` | 重轨默认:净新契约 + 跨功能一致性 + 深 tradeoff |
| | `design-sketch` | Track C 内单簇净新补丁 |
| | `design`(原全量版)| legacy 候选;新工作改用 `design-neo` |
| **decision(1)** | `qna` | **owner 决策唯一真源(register)** |
| **action-plan(1)** | `action-plan` | 执行序列(phase / 工作项 / 测试 / 收口)|
| **respond / 附加章节(4)** | `code-review-respond` | 实现者回应(append code-review §6)|
| | `respond-execution-log` | 执行日志回填(append action-plan §9)|
| | `respond-post-freeze` | 冻结后补强(append design/eval 续号)|
| | `respond-verification` | 代码碰撞核实矩阵(append 附录)|
| **review / closure / 专科(4)** | `code-review` | 评审制品 + verdict |
| | `closure` | 收口 + 价值/负债台账 + handoff |
| | `api-compliance` | API 合规审查 |
| | `bug-analysis-report` | bug 根因分析 |

---

## 2. 模板详解 + 模块分解(核心)

> 每个模板:**何时用/何时不用 · 文档状态 · 谁写·何时·上游→下游 · 模块分解表(模块 | 用途/责任 | 填写时机)**。`★` = 承重/灵魂模块;`可选/可省` = 视情形删除。

### 2.1 eval 家族(7)—— 共享「使用纪律(共有脊)」:本文是 eval,**冻结零决策**;凡需 owner 拍板列为 OPEN 或回 qna。头部/性质声明/TL;DR/输入锚定/修订历史为共有脊。**状态**:纯分析型 `draft|reviewed|superseded`;基线/锚型 `+frozen`(§4.1)。

#### `eval-general-purpose`
- **何时用**:charter 前的开放式提案/scoping(initial/re-planning/scope-analysis);不归其它 flavor 的 eval 的**默认兜底**。**何时不用**:冻边界→charter;写验收→design;排序→action-plan;对照找缺口→gap-study。
- **谁写·何时**:作者(可 panel),开工想清楚阶段;上游=charter/closure/eval,下游=charter/design。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 TL;DR / 论点 | 一段论点 + 一句话:做什么、为什么、留 owner 决断什么 | 必填 |
| 1 上游输入与锚定 | 站在哪些 frozen 之上 + 不重讨论的前提 | 必填 |
| 2 In/Out-Scope(提案边界)| 提议纳入/排除/灰区判定(非冻结边界)| 必填 |
| 3 提议的相位/工作簇 | 给候选单元命名(命名≠冻结)| 必填 |
| 4 逐簇工作台账 | "打算做什么"(非执行任务)| 必填 |
| 5 依赖图 DAG | 关键路径 + 并行窗 | 可选 |
| 6 Owner 决策门/开放问题 | 把必须拍板点列 OPEN,交 charter/qna 收口 | 必填 |
| 7 风险册 / 8 建议与下一步 | 风险 + 推荐序列 + 可解锁下游 | 必填 |
| 附录 A 二次意见 / B 修订历史 | round-trip / 版本 | 可选/必填 |

#### `eval-planning`(stage-aware:一套骨架,`stage` 开关切三态)
- **何时用**:子阶段会派生 **≥2 份 action-plan**、需走完整三态(initial 速写→proposed 重锚→final 冻结派生)。**何时不用**:单 AP 轻量 scoping→general-purpose;冻边界→charter;写验收→design;排单份序列→action-plan。
- **承重不变量**:每一态**辨证裁定其前序**(§2 承重段)。**stage 是成熟度轴,独立于 status**(§4.2)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 TL;DR / 1 Reference anchors | 论点 + 输入与依据 | 必填 |
| **2 辨证审核(裁定上一阶段)★** | 承重段:2.A initial 裁定原始 evals / 2.B proposed Δ vs initial / 2.C final critique vs proposed | 按 stage 选一块 |
| 3 范围 / 4 跨阶段贯穿主题 / 5 DAG | scope + red-line/治理/migration + 关键路径 | 必填/必填/必填 |
| 6 逐 phase 工作台账 | initial first-cut → proposed 重分配+verdict → final action-plan 绑定(lane/复用/退出/evidence/[Qn])| 必填(随态加厚)|
| 7 Owner gates | 7.A open(initial/proposed)/ 7.B final gate-closure map(全由冻结 QnA 关闭)| 按 stage |
| 8 测试计划 / 9 风险 | A/B/D 分层(+final capstone)| 必填 |
| 10 后继解锁 + AP 派生图 | 10.A final:命名并排序下游 action-plan(§6 phase 簇 1:1 映射)| final 必填 |
| 11 Final recommendation | 收尾 | 必填 |
| 12 [final] HEAD 实测/净新章节 | 用真实代码修正前序前提 | final 可选 |
| **13 [final] 冻结槽(双填充,至少一)** | 13.A owner-decision-freeze(QnA 索引,NORMATIVE)和/或 13.B contract-surface-freeze | final 必填 ≥1 |
| 附录 A stage 速用 / B 裁定动词 rubric | 填哪些块 + 动词词表(可按 lineage 覆盖)| 参考 |

#### `eval-reference-anchor`
- **何时用**:design 前,为功能簇系统盘点 `context/` 参考 + web 来源,产出可核验「借鉴台账」,并用 substrate-fit/TR 过滤防"把思路误抄成机制"。**何时不用**:找我方缺口→gap-study;做设计决策→design(本文只喂 design);穷尽外部 CLI→legacy/investigation。
- **图例**:借鉴 verdict `✅借/🔶部分借/⛔反例/🆕净新`(§4.4,**勿与复用判定混用**)。**基线/锚型,可 frozen**。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 如何读台账 | 0.1 Verdict 图例 / 0.2 置信分层(HEAD 实测>context 锚>web)/ 0.3 主题轴 | 必填 |
| 1 逐主题轴锚定矩阵 | 每个可借鉴点钉到 `path:line`/URL + 借鉴 verdict | 必填 |
| 2 反例坑表 ⛔ / 3 净新表 🆕 | 要避开的反例 / 无先例必须净新写的 | 必填 |
| 4 Web 来源台账 | 外部 URL 锚 + 可信度 | 可选 |
| **5 Substrate-fit / TR 过滤复核 ★** | 核心价值段:把借来的机制按 nano-agent 技术路线(TR-1..10)降级/重映射 | 必填 |
| 6 核验记录 / 附录 A 修订历史 | HEAD 实测 vs context 待 re-pin | 必填 |

#### `eval-gap-study`
- **何时用**:以参考实现为标尺,研究 **nano-agent 某子系统**缺什么、该建什么 → 喂 charter/design。**何时不用**:穷尽外部 CLI 本身→legacy/investigation;提案整阶段→general-purpose;go/no-go→feasibility。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 Verdict(结论先行)| 缺口总判定 | 必填 |
| 1 方法与可采信证据基线 | 证据可信度 | 必填 |
| 2 主体分析(轴自选)| A 按子系统 / B 按调查问题 Q1..Qn / C 单参考标尺走查 | 选一轴 |
| **3 缺口/断点台账 ★** | 核心产出:缺什么、断在哪 | 必填 |
| 4 参考对比矩阵 | vs 参考实现 | 可选 |
| 5 优先级建造建议 / 6 收尾 Verdict 与 charter 交接 | 排序 + 交接 | 必填 |

#### `eval-state-analysis`
- **何时用**:里程碑/相位完成后,回溯**已交付真实状态**(交付了什么、债多少、声称 vs 真实对得上吗),再交接下一周期(周期铰链)。**何时不用**:给制品下收口结论→closure;复盘失误→retrospective;提案新阶段→general-purpose。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 水位/健康一句话 | TL;DR | 必填 |
| 1 方法与对照基线 / 2 回看清单 | 2.1 交付价值台账 / 2.2 Deferred 台账(每条带 reopen 触发器)| 必填 |
| **3 对账诚实 ★(灵魂段)** | 声称 vs 代码真实;frozen≠done;占位猎杀 | 必填 |
| 4 归因/缺口分析 | 为什么有差距 | 可选 |
| 5 Verdict(价值-债务/达成度/健康评级)/ 6 前瞻交接 | 评级 + 下周期入口 | 必填 |
| 7 Spike/Test 水位 / 8 债务评分台账 | profile 扩展 | 可选 |

#### `eval-feasibility-study`
- **何时用**:charter/design 前,对**单个关键决策**做 go/no-go 探针(技术选型/前提),给 token 化结论。**何时不用**:泛泛找缺口→gap-study;提案整阶段→general-purpose。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 Verdict(结论先行)| go / no-go / conditional | 必填 |
| 1 假设/问题 / 2 现状/锚点 | 要验的命题 + 起点 | 必填 |
| 3 方法·试了什么(诚实段)| 真做了什么实验 | 必填 |
| 4 结果 | 4.1 原型数字 / 4.2 分类缺口矩阵 | 如适用 |
| 5 风险与残余 | 5.1 风险×缓解 / 5.2 残余风险硬前置条件(带进下相位)| 必填 |
| 6 结论与交接 | 交接 | 必填 |

#### `eval-retrospective`
- **何时用**:某 charter/design/action-plan 方向走错并已纠偏后,固化"学习化石"。**何时不用**:回看代码现状→state-analysis;评审制品→code-review;阶段收口→closure。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 一句话 | 错在哪 + 现在对的形态 | 必填 |
| 1 时间线 | 做了什么→何时发现→谁纠偏→纠成什么 | 必填 |
| **2 根因表 ★** | 追到机制/认知层(认知混淆/边界错置/信息缺失/流程缺口)| 必填 |
| 3 教训 / 4 现在的正确形态 | "下次遇 X 应 Y" + 旧→新对比 | 必填 |
| 5 接受批评/失败模式/重设计 | 长版(对 owner 指令内省时)| 可选 |

### 2.2 charter 家族(2)

#### `charter`(重轨纲领)
- **何时用**:foundation / 多月大阶段 / 多 sub-phase 需统一纲领。**何时不用**:它不替代 design/qna/action-plan/closure;小·低模糊→charter-lite。**状态**:`active charter | closed charter`(§4.1)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 为什么现在写 | 时点根本原因 + 要消除的模糊 + 职责边界 | 必填 |
| 1 Owner Decisions 与基石事实 | 直接生效决策 + 已冻结真相 + 不再重讨论前提 | 必填 |
| 2 Reality Snapshot | shipped/frozen truth + 核心 gap + 必须拒绝的错误前提 | 必填 |
| 3 一句话目标 | 产出 + 非目标 | 必填 |
| 4 全局 In/Out-Scope | + 灰区判定 + 硬纪律 + 例外 | 必填 |
| 5 方法论 | 对 phases 的直接影响 | 必填 |
| 6 Phase 总览与职责划分 | 总表 + 职责矩阵 + 交接原则 | 必填 |
| 7 各 Phase 详细说明 | 逐 phase 展开 | 必填 |
| 8 执行顺序与 Gate / 9 测试与验证策略 | DAG + Gate + 验证层/不变量 | 必填 |
| 10 收口分析(Exit/Non-Exit)| Primary Exit 硬闸 + NOT-成功识别 + 收口类型判定 | 必填 |
| 11 下一阶段触发条件 | 会纳入什么 + 为什么不前移 | 必填 |
| 12 Owner/Architect 决策区 | 内嵌 Q(应指向 qna register)| 可选 |
| 13 后续文档生产清单 | design/action-plan/closure + 撰写顺序 | 必填 |
| 14 最终 Verdict / 15 维护约定 | 阶段定义 + 工程/业务价值 | 必填 |

#### `charter-lite`(Track B)
- **何时用**:小阶段/快速迭代/敏捷收尾,**扩展既有 substrate·无净新·grounding 平凡**。**何时不用**:foundation/多月→charter;grounding 非平凡或要多 AP→Track C;命中 design-necessity→升级。
- **责任(精确)**:承担 charter 角色;**只替代 design 的「决策冻结」一项**;grounding 非平凡须配 reference-anchor(否则漏给 AP,教训 MIX5 SSRF)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 为什么现在做 + 不替代什么 | 0.2 为什么 charter-lite 而非 Track C / 完整 charter + 0.3 职责边界 | 必填 |
| **1 Owner Decisions + 冻结 QNA + 闸 ★(核心)** | 1.1 直接生效 / **1.2 冻结 QNA(硬闸一)** / 1.3 完整性自检 / **1.4 design-necessity 闸(硬闸二,6 条)** / 1.5 grounding 自检 / 1.6 不再重讨论 | 必填 |
| 2 现实起点(精简)| shipped/frozen + gap + 上阶段 defer/KI 碰撞 + 拒绝的错误前提 | 必填 |
| 3 阶段目标与边界 | 一句话目标 + In/Out + 灰区 + 硬纪律 | 必填 |
| 4 Phase 总览(精简)/ 5 执行顺序与 Gate | 总表 + DAG + Gate | 必填 |
| 6 验证与收口 | 策略 + 收口类型 + Primary Exit 硬闸 + NOT-成功识别 | 必填 |
| 7 下一阶段触发 + 后续文档(强制锚定)/ 8 维护约定 | 触发条件 + 产物清单 | 必填 |

### 2.3 design 家族(3)—— 三者定位见 design-sketch 头部「三件套定位表」。**状态**:`draft|reviewed|frozen|superseded`;**frozen 须 owner 裁决 §QNA,严禁自答,且落 `docs/design/` 户口**。

#### `design-neo`(Track D 重轨默认 · 减法版)
- **何时用**:重轨(有 charter)下的净新/争议架构;**跨功能一致性是首要价值**。**委派**:既有边界/锚→reference-anchor;决策→qna;相位/排期→eval-planning;work-item exit→action-plan;删 Value Verdict。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 背景与委派声明 | 明确委派出去了什么 | 必填 |
| 1 功能簇定义与术语对齐 | 净新概念消歧 | 必填 |
| **2 跨功能系统一致性 ★(首要价值)** | 2.1 整体形态 / 2.2 功能间一致性契约 / 2.3 数据·控制流贯穿图 / 2.4 跨 worker 不变量 | 必填 |
| 3 净新架构边界(仅净新)| 既有 → reference-anchor | 仅净新 |
| 4 净新契约叙述规格 | 从零定义对外契约(input/output/edge/schema)| 仅净新契约 |
| 5 深度 Tradeoff 辩证 | 选 X 不选 Y / 代价 / 重评(+风险缓解)| 仅争议架构 |
| **6 验收格栅 ★** | feature-level `功能 F → 收口目标 → Test-ID`(work-item exit 归 action-plan)| 必填 |
| 7 收口/户口/下游 | frozen 标准 + docs/design 户口 + 修订历史 | 必填 |

#### `design-sketch`(Track C 内单簇净新逃生口)
- **何时用**:整条 sub-phase 走 combo 轻轨,但**恰有一处** combo 装不下的净新契约/接缝(命中 design-necessity),给那一处轻量补丁,不为它整轨升重。**何时不用**:整 phase 净新多/争议→design-neo+charter;纯扩展既有→不写 design。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 背景:为什么这一处需 design 而其余不需 | 划清 combo 承载 vs 本文承载 | 必填 |
| 1 净新簇定义与术语对齐 | 单簇消歧 | 必填 |
| 2 净新架构边界(仅净新)| 既有 → reference-anchor | 必填 |
| **3 净新契约叙述规格 ★(核心)** | 把这一处净新契约从零叙述清楚 | 必填 |
| 4 In/Out-Scope(仅本簇)| 扩展既有交回 combo | 必填 |
| 5 Tradeoff | 仅本簇有争议取舍时 | 可选 |
| **6 QNA/决策登记(冻结门槛段)** | 必须 owner 裁决才能 frozen;指向 qna register | 必填 |
| 7 收口/户口/下游 | docs/design 正本或交叉索引 | 必填 |

#### `design`(原全量版 · legacy 候选)
- **何时用**:仅需完整三方对比 + Value Verdict 的特殊/历史场景;**新工作改用 design-neo**。腐烂段:§4 三方参考(委派 reference-anchor)、§9 决策(委派 qna)、§10 Value Verdict(仪式,可删)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 背景与前置约束 / 1 讨论对象 / 2 在 nano-agent 中的定位 | 功能簇 + 角色 + 交互矩阵 | 必填 |
| 3 架构稳定性与扩展策略 | 精简点/接口保留/完全解耦/聚合点 | 必填(★承重)|
| 4 参考实现/precedent 对比 | mini-agent/codex/cc 横向对比 | **已腐烂→委派 reference-anchor** |
| 5 In/Out-Scope 判断 / 6 Tradeoff 辩证与价值判断 | 边界 + 核心取舍 + 价值 | 必填(★承重)|
| 7 In-Scope 功能详细列表 | 功能清单 + 详述 + 非功能要求/验证策略 | 必填(★承重)|
| 8 可借鉴代码位置清单 | 仓内 file:line 锚 | **委派 reference-anchor** |
| 9 QNA/决策登记与收口 | 决策 + 完成标准 | **委派 qna**(只留新生决策+指针)|
| 10 综述总结与 Value Verdict | 自评打分 | **仪式,可删** |
| 附录 A 讨论记录 / B 版本历史 | 分歧留档 | 可选 |

### 2.4 decision 家族(1)

#### `qna`(owner 决策唯一真源 register)
- **何时用**:任何会影响下游 design/action-plan 的 owner/架构师决策——**收敛到一份单一清单**,别在多文档重复回答/漂移。**决策只活在 register**;其它文档只引 `Q 编号 + 业主回答`。
- **模块 = 逐 Q 块的字段 schema**(标准完整版):

| 字段(模块)| 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 影响范围 / 为什么必须确认 | 不拍板的后果 | 必填 |
| 当前建议 / Reasoning | 推荐路线 + 写给首次参与的业主的依据 | 必填 |
| Opus second opinion | panel 二次意见(身份反转版替换此槽角色名)| 未征求则留空,勿删结构 |
| 问题 / **业主回答** | 二元/具体问题 + **业主只在此填** | 业主裁决时 |
| §3 使用约束 | 哪些进/不进 QNA + 各字段写法 + 身份反转版 | 参考 |

### 2.5 action-plan 家族(1)

#### `action-plan`(执行序列 · 全轨终点 · v2 自带锚区 + 测试台账)
- **何时用**:落地——消费已 frozen 的 design/qna/closure,排"怎么做/何序/怎么测/怎么收口"。**纪律**:不开 Q/A(回 design/qna 冻结);只消费已冻结结论。**状态**:`+executing|executed`(§4.1)。**合法上游按轨**见 §1.2。
- **v2 要点(2026-05-31)**:**单一模板,不分 flavor/档位、不做前置体量检测**;把两块高价内容做成固定段(**§7 内置 reference-anchor 锚区**、**§8 测试台账**),收口口径=测试台账全 PASS 映射。设计依据见 `re-design/action-plan-new-version-proposal.md`(v0.2)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 执行背景与目标 | 从哪些 frozen 继承 + 直接产出 + 不重讨论结论 | 必填 |
| 1 执行综述 | 总体方式 + Phase 总览/说明 + 执行策略(§1.4 勿重述冻结决策)+ 影响结构图 | 必填 |
| 2 In/Out-Scope + 边界判定 | 本次明确做/不做 | 必填 |
| **3 业务工作总表 ★** | 每行 = 不可约三元组 `涉及文件(file:line) | 收口目标 | 测试映射(→§8 Test-ID)`;安全项指向威胁模型 | 必填 |
| 4 Phase 业务表格 / 5 Phase 详情 | 工作项 → phase → 文件级任务;**`工作内容` 是承重列,分解度与净新度/风险成正比(净新/高风险拆有序子步 a/b/c + 边界;复用/扩展既有一句话)**;测试只引 Test-ID(细节归 §8)| 必填 |
| 6 依赖的冻结设计决策(只读引用)| 只引 register Q 编号,不复制 | 必填 |
| **7 内置 Reference-Anchor 锚区 ★新** | 7.1 锚表(path:line + 复用判定处置)/ 7.2 反例 ledger⛔ / 7.3 上游真源指针 + 安全项威胁模型(不得留空,堵 MIX5)| 必填 |
| **8 测试台账 ★★新核心** | 8.1 测试清单(类型 短途/spike/mega/soak · 层 · 来源 🆕新增/♻️沿用/🔱fork · 映射 · 四元组 PASS)/ 8.2 复用台账 / 8.3 分层跑法 / 8.4 缺口 / 8.5 防假绿 | 必填 |
| 9 风险/约束/文档同步/完成后状态 | 风险 + 约束前提 + 文档同步 + 完成后预期 | 必填 |
| 10 收口(DoD = 测试台账全 PASS 映射)| 收口硬闸 + 收口映射表(收口目标↔Test-ID↔证据)+ closure 五态 | 必填 |
| 11 执行日志回填(仅 executed)| 薄占位;详细回填改用 `respond-execution-log` | executed 后 |

### 2.6 review / closure / 专科(4)

#### `code-review`(评审制品 + verdict)
- **何时用**:评审 design/action-plan/code/docs/closure。**状态**:`reviewed|changes-requested|re-reviewed|closed`。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 总结结论 | 一句话 verdict + 等级(approve/changes-requested/blocked)+ 是否可关闭 | 必填 |
| 1 审查方法与已核实事实 | 正面/负面事实 + 证据可信度 | 必填 |
| 2 审查发现 | Finding 汇总表 + R1..Rn 详情 | 必填 |
| 3 In-Scope 逐项对齐审核 | 是否满足 design/AP 收口标准 | 必填 |
| 4 Out-of-Scope 核查 | 防越界 + 防把 deferred 误判 blocker | 必填 |
| 5 最终 verdict 与收口意见 | 收口意见 | 必填 |

#### `closure`(收口 + 价值/负债台账 + handoff)
- **何时用**:阶段/子阶段完成收口。**先选档**:子阶段(§0–5)/ 阶段 final(§0–7)/ grand(§0–9)。**纪律**:close-type 4 类 + 诚实收口 5 态 + ✅ 用四元组证据(commit+query/test+run-time)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 一句话 verdict | close-type(四选一)| 必填(全档)|
| 1 工作项收口表 / 2 Evidence·Validation 矩阵 / 3 Hard-gate 判定 | 逐项 + 证据 + 硬闸 | 必填(全档)|
| 4 Deferred/Carry-over ledger / **5 诚实收口声明 ★** | 三类 deferred + 诚实 5 态归类 | 必填(全档)|
| 6 Handoff / 下阶段 entry-gate 预核对 | 交接 | 阶段 final+ |
| 7 Cross-cut 不变量(0-drift)| 横切确认 | 阶段 final+ |
| 8 价值/负债台账 / 9 Closing + 定位裁定 | 5 级证据价值台账 | grand |

#### `api-compliance`(API 合规审查)
- **何时用**:对照 frozen contract / qna 审 API surface 合规(NACP)。**状态**同 code-review。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 总判定 + 簇级总览矩阵 + Finding 数量汇总 | Executive Summary | 必填 |
| 1 调查方法学 | 六维评估 + 严重级别 + 已核实事实 + 证据可信度 + 跨簇横切 | 必填 |
| 2 簇级总览矩阵(全端点)/ 3 簇级深度分析 | 逐端点 + 逐簇 | 必填 |
| 4 跨簇 NACP 协议合规 | Authority 翻译 / Trace UUID / Error Code 字典 / Tenant 边界 / Envelope 漂移 Drift Gate | 必填 |
| 5 Findings 总账 / 6 行动建议 / 7 测试覆盖矩阵 / 8 文件&引用索引 | 汇总 + 优先级 + 缺口 | 必填 |
| 9 复审与回应入口 / 10 实现者回应(仅 re-reviewed)| 回应 + blocker | re-reviewed 时 |

#### `bug-analysis-report`(owner-test → bug 根因)
- **何时用**:owner-test 回来后、动手写 charter/action-plan **之前**的诊断产物。**§6–§10 是灵魂**(架构定性/DAG/测试归责/执行顺序/测试方案)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 0 一句话 Verdict + owner 最关心问题 | TL;DR | 必填 |
| 1 调查方法与证据基线 / 2 截图真相→D1/证据对照 | 取证先行 | 必填 |
| 3 Bug 平铺与业务簇归类 / 4 逐业务簇深度分析(代码级证据)| 分簇 + 根因 | 必填 |
| 5 横向交叉分析(共因)| 多 bug 共因 | 必填 |
| **6 架构判定 + hot-fix vs 长治修复 ★** | 逐簇定性(hot-fix 不许带债)| 必填 |
| **7 完整 DAG 修复结构 ★** | 前端修什么/后端修什么/依赖边/波次 | 必填 |
| **8 测试体系归责 ★** | 为什么没发现 + 该哪层抓 | 必填 |
| 9 修复执行顺序确认 / **10 修复后测试方案 ★** | 顺序 + 每簇映射到层 + 保真硬要求 | 必填 |
| 11 诚实边界/重大更正 / 12 owner 问题逐条回答 / 13 carry-over / 14 附录取证 | 诚实 + 回答 + 历史关系 | 必填 |
| 附录 Z FAX5–9 长期原则 | 证据纪律/执行顺序/修复定性/测试保真/收口诚实(刻死清单)| 保留 |

### 2.7 respond / 附加章节家族(4)—— **不是独立文档,是 append 到宿主的章节**。强制 banner:宿主 / 挂载位 / append-only / 作者·时机 / 回链 item-ID / 多轮。

#### `code-review-respond`(append code-review §6)
- **何时用**:实现者修复 code-review 后逐项回应。**append-only**:不改写 §0–§5;多轮追加 `6B/6C`。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 6.1 对本轮回应 / 6.2 逐项回应表 | R-ID × `fixed|deferred|rejected` | 必填 |
| 6.3 Blocker/Follow-up 状态 / 6.4 变更文件 / 6.5 验证结果 | 状态 + 文件 + 全绿计数 | 必填 |
| 6.6 未解决承接 / 6.7 Ready-for-rereview gate | 承接 + 可复审门 | 必填 |

#### `respond-execution-log`(append action-plan §9 · 厚版)
- **何时用**:action-plan `executed` 后回填执行日志。**纪律**:计划 vs 实际逐条偏差;pre-existing 失败带 git 证据甩锅;residual 交后继,不回填本阶段。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| 9 摘要(仅 executed)/ 9.1 逐工作项状态 | `工作项|状态(✅/⚠️/❌)|PR|实际落点|备注` | 必填 |
| 9.2 关键指标演进 / 9.3 时序执行日志 / 9.4 关键决策日志 | before/after · 多轮 · 决策 | 可选 |
| 9.5 pre-existing 失败甩锅 / 9.6 文档状态 | git 证据 · draft→executing→executed | 可选/必填 |

#### `respond-post-freeze`(append 续号到 frozen design/eval)
- **何时用**:主体 frozen 后,因 owner 裁决/驳回/提问触发的补强。**最硬纪律**:不重开任何冻结裁决;supersede 须点名 + 回 qna 重开;对照**当前代码**复核;新 file:line 本轮 verify;新工作项用新 ID 前缀(`R-*`)。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| N.0 判据/约束重述 | 校准非改写冻结理由 | 如适用 |
| N.1 重新基线化缺口/价值台账 | 对照当前代码 | 必填 |
| N.2 补强/re-scope 工作列表 | 新 ID 前缀 | 必填 |
| N.3 收口标准/自检矩阵 / N.4 待议·已裁决开放项 / N.5 诚实边界·supersede 声明 | 自检 + supersede 点名 | 必填 |

#### `respond-verification`(append 附录 · 冻结前对抗自检)
- **何时用**:作者本人(经扇出 sub-agent)在 frozen 前对宿主台账做代码碰撞核实。**最硬纪律**:只读真实代码(`workers/**/src`、`clients/web/src`、`migrations`、`test`),不读 docs/.tmp;每行带 file:line;凭记忆/closure 与代码不符须显式标 `修正`。

| 模块 | 用途 / 承担的责任 | 填写时机 |
|------|-------------------|----------|
| X.1 碰撞核实矩阵 | `项(host-ID)|核实状态(ACTIVE/STALE/PARTIAL)|file:line 证据|对台账影响(含修正)` | 必填 |
| X.2 核实结论 | N 项碰撞 / K 处修正 / 净影响 | 必填 |
| X.3 核验记录 / X.4 技术路线适配审查 | substrate/reference 变体(置信分层 / TR 过滤)| 可选 |

---

## 3. 模块重组指南(跨模板组合)

### 3.1 原则
- **默认选一个模板**;只有当一个分析同时需要多个模板的能力时才组合。
- 组合时**以一个模板作主骨架,从别处借模块嵌入**,并在头部写 `结构来源(dogfood):…`。
- 组合**不改变模块的语义与纪律**(借 `design §6 Tradeoff` 就得写"选 X 不选 Y/代价/重评条件";借 `state-analysis §3 对账诚实` 就得真对账代码)。

### 3.2 真实先例(已落地,可直接仿照)

| 产物 | 主骨架 | 借入的模块 |
|------|--------|------------|
| `re-design/value-proposition-of-template-docs.md` | `eval-state-analysis` 骨架 | + `design §6 Tradeoff` + `design §10 Value Verdict` + `eval-gap-study 缺口台账` |
| `re-design/nano-agent-vs-SDD.md` | `eval-gap-study` 对照骨架 | + `design §6 Tradeoff` + `design §10 Verdict` |
| `re-design/CCMD-vs-SDD-by-opus.md` | `eval-general-purpose` 共有脊 | + `eval-retrospective §2 根因表` + `design §6 Tradeoff` + `design §10 Verdict` |

### 3.3 高复用模块目录(最常被借出的零件)

| 模块 | 出处 | 借来做什么 |
|------|------|------------|
| **TL;DR / Verdict 结论先行** | 所有 eval / code-review §0 / closure §0 | 任何分析的开头一句话裁定 |
| **Tradeoff 辩证**(选 X 不选 Y / 代价 / 重评条件)| `design §6` / `design-neo §5` | 任何有争议性取舍的分析 |
| **Value Verdict 多维评分矩阵** | `design §10` | 任何要给"值不值/各维度打分"的评定 |
| **对账诚实**(声称 vs 代码 / frozen≠done / 占位猎杀)| `eval-state-analysis §3` | 任何要防"文档剧场" |
| **根因表**(追到机制/认知层)| `eval-retrospective §2` | 任何要复盘失误为什么发生 |
| **substrate-fit / TR 过滤** | `eval-reference-anchor §5` | 任何要把外部机制按本仓技术路线降级/重映射 |
| **碰撞核实矩阵**(仅读真实代码)| `respond-verification` | 任何要对抗性自检"台账 vs 代码" |
| **验收格栅**(F→收口目标→Test-ID)| `design-neo §6` | 任何要可验证完工标准 |
| **裁定动词 + rubric**(KEEP/REFRAME/…)| `eval-planning §2 + 附录 B` | 任何要裁定/对比前序版本 |
| **诚实收口 5 态 + 价值-负债台账** | `closure §5 / §8` | 任何要给交付物分级证据 |
| **DAG 修复结构 + 测试归责** | `bug-analysis §7 / §8` | 任何多问题共因 + 分层归责 |
| **eval 共有脊**(头部/性质/输入锚定/修订历史)| 所有 eval | 任何新分析文档的骨架 |

---

## 4. 统一约定(CANONICAL —— 唯一真源)

### 4.1 文档状态词汇

- **核心四态(所有文档共用)**:`draft → reviewed → frozen → superseded`
  - `draft` 在写 · `reviewed` 已评审 · `frozen` 定稿锁定(决策/边界/规格/基线锁死,只能 supersede 不能改)· `superseded` 被新版取代
- **家族合法扩展**(仅以下情形可加):
  - `action-plan`:+ `executing | executed`(执行态)
  - `charter`:用 `active charter | closed charter`(active=生效中,closed≈frozen)
  - `code-review` / `api-compliance` / `*-respond`:`reviewed | changes-requested | re-reviewed | closed`
- **eval 家族细分**:
  - 纯分析型(general-purpose / gap-study / state-analysis / feasibility / retrospective):`draft | reviewed | superseded`(快照,不 freeze)
  - 基线/锚型(`eval-planning` 的 final 阶段 / `eval-reference-anchor`):`draft | reviewed | frozen | superseded`(会冻结基线)
- **澄清**:`frozen`(文档定稿锁定)≠ eval 的"冻结零决策"(指 eval 不替 owner 拍板)。前者说**文档状态**,后者说 eval **不抢 owner 决策权**——两者不矛盾。

### 4.2 stage 轴(仅 `eval-planning`)

`stage: initial | proposed | final` —— 这是**成熟度轴,独立于 status**。不要把 stage 值塞进 status 字段。

### 4.3 轨道命名(canonical)

`Track A 单遍 / Track B charter-lite / Track C combo(= 三态规划 + reference-anchor + qna)/ Track D 重轨`。引用时统一用 `Track X 名称`。

### 4.4 符号图例(两套,语义不同,**勿混用**)

- **复用判定**(我方代码处置;用于 `design-neo` / `design-sketch` / `eval-planning` 的工作台账):
  `✅ 复用` / `♻️ 重 substrate`(在既有 substrate 上重建)/ `🆕 净新`
- **借鉴 verdict**(外部参考裁定;**仅 `eval-reference-anchor`**):
  `✅ 借` / `🔶 部分借` / `⛔ 反例(避开)` / `🆕 净新(无先例)`
- 注:两套都含 `✅` 与 `🆕`,但语境不同(前=我方代码,后=外部参考),**不可互换**。

### 4.5 裁定动词 rubric(`eval-planning §2` / `better-planning`,可按 lineage 覆盖)

- proposed 态(vs initial):`KEEP / REFRAME / CLOSED / NEW`
- final 态(vs proposed):`CONFIRM / CORRECT / REFINE / RESIZE / GAP`

### 4.6 design-necessity 6 条(canonical 治理闸 —— `charter-lite §1.4` 与 `workflow-tracks §4` 必须与本表逐字一致)

满足**任一** ⇒ 不能只靠 charter-lite/combo,需 design(`design-sketch` 单簇 / `design-neo` 多簇):

1. 新增**对外 contract surface**(从零定义,非扩展既有)
2. 新增**架构接缝**(净新 decouple/aggregate;reference-anchor 无既有 ARCH 可锚)
3. **跨 worker 不变量 / 多功能必须拼成一个整体形态**
4. 验收是**多字段 / 非显然**的(一两句 QNA 答不清"做完长什么样")
5. 涉及**安全信任边界**(威胁模型)—— 强制升级
6. **onboarding 关键**:需新贡献者读懂的叙述式契约

### 4.7 核心名词表(统一中英用法)

| 名词 | 含义 | 用法 |
|------|------|------|
| `净新`(net-new) | 从零定义的对外契约 / 架构接缝 | 中文优先用"净新" |
| `扩展既有`(additive) | 在已建 substrate 上加列/加端点 | 中文优先用"扩展既有" |
| `grounding` | 架构边界 + 仓内 file:line 锚 的落地依据 | 保留英文,不译 |
| `substrate` | 仓库现实代码基底 | 保留英文,不译 |
| `缝 / seam` | 跨模块 / 契约的接缝 | 中英皆可,同义 |
| `收口目标` | 一句话可验证完工标准 | 统一"收口目标"(非"完工标准/done criterion"混用)|
| `验收格栅`(acceptance lattice) | `功能 F → 收口目标 → Test-ID` 三联 | design-neo §6 / eval-planning final |
| `frozen / 冻结` | owner 裁决后锁定 | 见 §4.1 |
| `qna register` | owner 决策唯一真源 | 见 §4.8 |

### 4.8 交叉引用与占位符约定

- **引用模板**:用文件名根(`eval-reference-anchor` / `design-neo` / `qna` / `action-plan`),不裸缩写。`charter-lite` 内若用 `AP` 须首次出现处定义 `AP = action-plan`。
- **`qna` 大小写**:文件/register 一律小写 `qna`(`qna.md` / `qna register`);大写 `QNA` 仅指通用 Q&A 机制/内嵌块。**决策只活在 register**,design-sketch/eval-planning/charter-lite 的内嵌 QNA 必须指向 register,不另立真源。
- **占位符**:统一 `{UPPER_SNAKE}`,backtick 包裹(如 `` `{PHASE_NAME}` ``)。
- **eval 家族共有脊**:头部统一含"`使用纪律(共有脊 · 所有 eval 模板一致)`"块(结构一致;首条声明"本文是 eval,冻结零决策";flavor 细节在 `模板类型` 字段)。
- **respond 家族 banner**:头部统一声明宿主 / 挂载位 / append-only / 作者·时机 / 回链 item-ID / 多轮。

---

## 5. legacy/ 说明

`docs/templates/legacy/` 存放已被 active 集取代的历史模板,**不用于新工作**:
- `investigation.md` → 外部 CLI 深析已由 `eval-gap-study`(我方缺口)/ `eval-reference-anchor`(借鉴锚)覆盖
- `code-review-eval.md` → 审查质量评价已并入 `code-review` 流程
- `code-megafile-header.md` / `_TEMPLATE-spike-finding.md` / `issue-closure-fax9-and-beyond.md` → 专项/陈旧

---

## 附录 · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿:active 22 模板索引 + 四轨速查 + canonical 统一约定 + legacy 说明 |
| v0.2 | 2026-05-31 | Opus 4.8 | **完整重写为可操作索引**:新增 §0 使用指南、§1 选择决策树、**§2 逐模板模块分解表(模块·责任·填写时机 + 何时用/何时不用 + 谁写·何时)**、**§3 模块重组指南(原则 + 3 真实先例 + 高复用模块目录)**;canonical 约定保留并补 respond banner;legacy 校正 |
| v0.3 | 2026-05-31 | Opus 4.8 | 同步 `action-plan` v2:§2.5 模块表更新为 11 段(新增 §7 内置 reference-anchor 锚区、§8 测试台账、§10 收口=台账全 PASS 映射、§11→respond-execution-log;§3 升为不可约三元组);依据 `re-design/action-plan-new-version-proposal.md` v0.2 |
