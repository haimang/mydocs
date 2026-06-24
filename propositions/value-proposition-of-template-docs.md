# nano-agent 文档/模板体系的价值评定（v0.2 · 看到"驱动端"后的重写）

> 文档对象：nano-agent 这套"因开发而生"的体系的价值——**含输出端（模板+产出文档）与输入端（`.anote/` prompt 剧本）的完整双面**
> 作者：Claude Opus 4.8（语料普查 + 6 个外部文档框架 web 调研 + `.anote/` 三层 prompt 剧本采样 + 本会话 6 份 re-design 综合）
> 日期：2026-05-30
> 文档性质：`eval / general-purpose`（辨证价值分析，冻结零决策）
> 文档状态：`draft | reviewed | superseded`
> **本文取代**：v0.1（已删除）。v0.1 只看到输出端，把它定性为"文档系统"；本版看到了驱动端（`.anote/`），重定性为**双面互锁、与开发协同演化的闭环方法论**。
> 结构来源（dogfood 自身模板）：`eval-state-analysis` 骨架 + `design §6 Tradeoff` + `design §10 Value Verdict` + `eval-gap-study 缺口台账`
> 上游输入：本会话 re-design 六件套 + `README.md`(canon) + 语料普查 + 外部 web 调研 + `.anote/{1-temp,2-plan,3-exec}` 采样

---

## 0. TL;DR / 一句话价值结论

**v0.1 只看到了这套系统的一半。** 当时只见输出端（模板 + 产出文档），结论是"无持久记忆异构 LLM 集群的外部记忆 + 协调协议"。看到 `.anote/` 的 prompt 剧本后，完整图景是：

> **这是一个双面互锁、与开发同步演化的闭环方法论。** 输入端（prompt 剧本：`1-temp` 流水带 + `2-plan`/`3-exec` 蒸馏库）**驱动**，输出端（模板 + 产出文档）**承载**；两端共享**同一套"模板↔实例"两层架构**，并随开发逐阶段**协同演化**——`1-temp` 是不可变的演化化石，学习不断**蒸馏回库**（本会话的减重，就是这个蒸馏机制作用在输出端的一次实例）。

价值因此比 v0.1 判定的**更高、更自洽**（综合 4 → **4.5**，§9）——升幅来自 v0.1 漏看的**闭环自洽 + 输入-输出对称 + 自蒸馏演化机制**，不是空话。主要成本（token/仪式/验证/onboarding）依旧真实。

---

## 1. 调查方法与输入

| 路 | 内容 |
|----|------|
| 输出端普查 | `docs/{eval,design,action-plan,issue}` 文件/行数、阶段数、qna 数、多模型署名（§2.1）|
| **输入端采样（新）** | `.anote/2-plan`(205 行库) + `.anote/3-exec`(206 行库) + `.anote/1-temp`(3496 行 live ledger 尾部 ~480 行)（§2.2）|
| 外部对标 | 6 个文档框架 web 调研：Diátaxis / ADR / Oxide-RFD+Rust-RFC / Amazon PR-FAQ / docs-as-code / C4-arc42（§6，附 Sources）|
| 内部综合 | 本会话 re-design 六件套结论 |

---

## 2. 这套系统的全貌：双面互锁闭环

### 2.1 输出端（模板 + 产出文档）—— v0.1 看到的那一半

把"想法→落地"全程结构化的产物流水线：`eval（7 型）→ charter/charter-lite → design 家族 + qna → action-plan → respond → closure → state-analysis`，四轨（A/B/C/D）按模糊度/净新度选重轻。规模量化：

| 指标 | 数值 |
|------|------|
| 受治文档 | **~1,064**（eval 400 + design 175 + action-plan 204 + issue 285）|
| 总行数（eval+design+action-plan） | **355,671 行** |
| 阶段族 | **16** |
| qna 决策册 | **23** |
| 带 `-by-<model>` 署名的 eval | **308（≈77%）** |
| active 模板 + canon | 23 + README |

### 2.2 输入/驱动端（`.anote/` prompt 剧本）—— v0.1 漏看的那一半

owner 不直接写代码/文档，而是用结构化自然语言 work-order 调度异构模型。这一端也是**两层**：

- **`1-temp`（3496 行，live ledger）** = **生产流水带**：按时间 append 的真实 prompt 记录（MI1-9 → MIX → MIS → spike → web-v80 FE/FEX……），每条都填了本次真实的文件名/审查者/closure 路径。
- **`2-plan` / `3-exec`（库）** = 从流水带**蒸馏**出来的可复用模式（plan 阶段 / exec 阶段）。

这些 prompt **逐字编码了本会话反向工程出的全部纪律**：流水线分步、`不得跨阶段`、`每个 TODO 重新拉上下文`（=无状态补偿）、`3-4 位同事独立审查→平铺→合并→核查→修复→回填`（=panel）、`仅用你自己的 reasoning，不考虑其他同事`（=独立纪律）、`使用 docs/templates/X.md 作为模板`（=prompt→模板的接线）、`回 context/ 用 sub-agent 锚参考`（=reference-anchor）。

### 2.3 互锁闭环 + 输入-输出对称（核心新认知）

- **co-design 互锁**：prompt 把模板**点名为产出目标**，模板的结构又让 prompt 的"产出 X"**可验证**。模板约束输出→prompt 不必写死格式；prompt 驱动填充→模板不会沦为死文档。**这种"工序↔产物 schema 互相兜底"是真正承重的创新。**
- **同构对称**：`库 : 流水带 :: docs/templates/ : docs/eval+design+action-plan/`。**owner 在输入端和输出端用了同一套"模板↔实例"两层架构。** 不是巧合，是自洽的元设计。

### 2.4 协同演化（drift 是健康化石，不是病）

看 `1-temp` 尾部能直接看到 prompt 在**变好**：独立纪律加固（后期加"也不考虑已存在的分析报告"）、评审长出"二轮跨 package + D1 drift 校准 + api-docs 碰撞 + known-issue 关闭"四件套、`测试↔️修复 循环`措辞稳定。**三种变化要分清**：

1. **逐实例定制**（流水带填具体文件名/审查者）——不是 drift，是正确实例化。
2. **逐阶段演化**（纪律加固、结构成熟）——健康成熟；流水带应**不可变**（像 git log，不回改历史）。
3. **真错误传播**——唯一该动手的：如 `context/af-agents`（应为 `cf-agents` 的笔误，在 1-temp 多处复现）、各 block 的 context 目录集不一致。

> **演化是有形状的**：最反复、最稳定、几乎一字不变穿越每阶段的是**独立纪律**与**二轮审查结构**（=被验证的承重核）；context 目录名、步骤措辞这些**外围**一直在微调。**核心收敛、外围流动**——这是成熟的形状，既非僵化亦非混乱。**纪律：蒸馏回库、修库里的真笔误；永不回改流水带的历史。**

---

## 3. 正面价值（V1–V8）

> V1/V2 是 LLM-agent 开发独有的放大项；**V8 是 v0.2 新增的"驱动端/闭环"价值**。

- **V1 · 跨无状态会话的持久记忆**：每次 compaction = 失忆，文档是唯一跨会话存活的项目状态。**本会话就是被压缩后从 docs rehydrate 续作的活证据**。
- **V2 · 异构多模型协调协议**：308 份 `-by-model` + qna 身份反转 + panel + 对抗复核——业界框架都假设人类作者，**没有这一层**。
- **V3 · 决策溯源**：qna 冻结 → design/action-plan 只读引用 `Q 编号`，端到端可追。
- **V4 · 漂移/腐朽防御**：state-analysis 的"对账诚实 / frozen≠done / 占位猎杀"——比业界泛泛"定期 review"更硬。
- **V5 · 模态纪律**：eval=提案 / charter=冻边界 / design=冻决策+写验收 / action-plan=排序执行，防范畴错误（charter-lite 的 design-necessity 闸制度化它）。
- **V6 · 测试/缝治理**：spike/mega/seam + 6 根因缝，把"测什么、漏哪"结构化。
- **V7 · 可 fan-out 结构**：模板化让 sub-agent 并行扇出可归并（本会话反复用 3-6 路并行 agent）。
- **V8 ·（新）闭环驱动端 + 自蒸馏演化**：prompt 剧本把"怎么驱动 agent"也外置成两层库，与输出端对称互锁；并且体系**会自我蒸馏减重**（本会话即一次）。这让它从"一堆好文档"升级为"**一个会自我维护的活方法论**"。

---

## 4. 量化：proxy 指标 + 测量诚实

**诚实前提**：文档价值本质**反事实**，下面是**代理指标**，非直接 ROI。

| 可测代理 | 现值 | 解读 |
|----------|------|------|
| 输出端外部记忆体量 | 1,064 文档 / 355k 行 | rehydration 的信息底座 |
| **输入端剧本体量（新）** | `1-temp` 3496 行 ledger + 2 个蒸馏库 | 驱动工序也被外置/可复用 |
| 多模型协作率 | 77% eval 带署名 | panel 真实落地 |
| 决策溯源密度 | 23 qna 册 | 决策有冻结真源 |
| 演化证据（新） | 1-temp 可见纪律逐阶段加固 | 体系在活着长 |
| 自蒸馏进展 | 本会话减重 + canon | 体系能自我维护 |

**建议引入的前瞻领先指标**（仍缺，§8）：① 决策可追率 >90%；② state-analysis 每轮 doc-rot 命中数（应降）；③ rehydration 成功率（本会话=成功一例）；④ 轨道误用事件数（MIX5=一次失败，目标 0）；⑤（新）**库↔流水带蒸馏延迟**（最佳 prompt 多久回流到 2-plan/3-exec）。

---

## 5. 成本与反面（C1–C5，已按新认知修正）

- **C1 · token/时间开销**：355k 行 + 多轮 panel + 反复拉上下文，对"上下文是瓶颈"的 LLM 是真实成本。文档越多 rehydration 越贵。
- **C2 · 默认过冲**：系统默认上重轨，事后才学会减重（combo/charter-lite）。无主动反压（必要性测试）会自我长胖。
- **C3 · 验证问题（最深）**：文档可能"好看但脱节代码"（frozen≠done / design 误存 eval / 占位假零都真发生过）。state-analysis 对抗它，但 panel 可能共享盲点，最终 ground truth 仍是 owner——而 owner 注意力正是系统想省的，存在张力。
- **C4 · onboarding/可发现性**：~1,064 文档 + 剧本 + 16 阶段，对新人墙很高（Diátaxis 缺口）；README 前无索引是历史欠账。
- **C5 · 元工作增殖**：现有 6 份"关于模板的" re-design 文档（含本篇）。需警惕元层喧宾夺主。
- **（已撤销的 v0.1 旧 C：「drift 是病」）**：经 §2.4 修正——**drift 大部分是健康协同演化，不计入成本**；只有"真错误传播"（如 af-agents 笔误）是该修的残余，且修法是蒸馏回库、不改流水带。

---

## 6. 外部参考对比（web 调研）+ 我们的位置

| 框架 | 它做什么 | 借鉴点 |
|------|----------|--------|
| **Diátaxis**（tutorial/how-to/reference/explanation）| 按用户需求组织 | ➕ 补"用户向/onboarding 模式"（我们是作者/流程向）|
| **ADR**（不可变/2 页/superseded 链）| 轻量决策记录 | ➕ qna 接受即不可变 + 双向链接 |
| **Oxide RFD + Rust RFC**（状态机/FCP/编号索引）| 提案状态机 + 终评门 | ➕ 形式化状态机 + frozen 前终评期；✅ 编号索引（README 已起步）|
| **Amazon PR-FAQ / 6-pager**（倒推/长度上限）| 倒推 + 长度纪律 | ➕ 长度纪律（文档巨大）|
| **docs-as-code / GitLab**（git 真源/PR review/模块化）| 工程化维护 | ✅ git 真源；➕ doc 改动走 review 门 |
| **C4 / arc42**（分层架构视图）| 架构图分层 | ➕ C4 分层图用于 design-neo 跨功能一致性段 |

**关键升级（v0.2）**：上述框架**全都只覆盖"输出端"（人类作者写的文档）**。**没有一个有"输入/驱动端"**——因为它们假设作者是有持久记忆、自带工序的人，不需要把"怎么驱动作者"也外置。**nano-agent 的 prompt↔模板闭环，比 v0.1 以为的更新更稀有**：它是为"无记忆、需被驱动的 agent 作者"补上的那半个方法论，业界无现成对标。

**我们 LLM-native 地领先**：① 多模型协调协议；② 反 doc-rot 命名机制；③ 三态成熟链是收敛进化的独立佐证；④（新）**输入端剧本 + 输入-输出对称 + 自蒸馏演化**——整套闭环无对标。
**我们该补**：用户向模式、长度/不可变纪律、形式化状态机+索引。

---

## 7. Tradeoff 辩证（核心取舍）

1. **选"重双面 substrate" 而非 "轻文档 + 代码自解释"**
   - 为什么：agent 无持久记忆、需被驱动；代码自解释不足以跨会话/跨模型。
   - 代价：token/仪式（C1/C2）。
   - 重评条件：**若 agent 获可靠长期记忆 / 对代码的 RAG 足够强**，可大幅减重。← 未来最该盯的重评点。
2. **选"prompt↔模板互锁" 而非 "二者各自为政"**
   - 为什么：互相兜底（模板省 prompt、prompt 救模板腐烂）。
   - 代价：两端都要维护、都会漂移。
   - 重评条件：演化纪律（§2.4）能否持续——核心稳、外围流、蒸馏回库。
3. **选"流水带不可变 + 蒸馏回库" 而非 "原地改史 / 自由放养"**
   - 为什么：保留演化化石（可追因）+ 让新实例从当前最佳起步。
   - 代价：需周期性蒸馏动作（又是元工作）。
   - 重评条件：蒸馏延迟过大 → 库陈旧 → 新实例从旧版起步。

---

## 8. 可提高空间（缺口台账，按价值排序）

| # | 缺口 | 借鉴源 | 建议 | 价值 |
|---|------|--------|------|------|
| 1 | 默认过冲（C2）| RFC 分级 | "轨道/design 必要性测试"提为开工前全局 checklist | 高 |
| 2 | **输入端库未蒸馏（新）**：1-temp 已成熟的最佳 prompt 未回流 2-plan/3-exec；`af-agents` 等真笔误在库/流水带传播 | 自蒸馏纪律 | **过一遍 `2-plan`/`3-exec`**：回填加固版独立纪律/二轮四件套/测试↔修复措辞 + 修 `cf-agents` 笔误 + 统一 context 目录集（**改库，不改 1-temp 历史**）| 高 |
| 3 | 无长度纪律 | PR-FAQ/ADR | 各模板软长度上限 + 超限降轨信号 | 高 |
| 4 | 用户向/onboarding 缺位 | Diátaxis | 加 onboarding/how-to 文档类型 | 中-高 |
| 5 | 状态是标签非状态机；无 FCP | RFD/RFC | 形式化状态机 + frozen 前终评期 | 中 |
| 6 | qna 不可变性不严格 | ADR | qna 接受即不可变 + supersede 双链 | 中 |
| 7 | 缺可量化领先指标 | — | 落地 §4 的 5 个前瞻指标（含蒸馏延迟）| 中 |
| 8 | 元工作增殖（C5）| — | re-design 系列收口冻结 | 低-中 |

> **注**：drift **本身不在缺口表**——它是健康演化（§2.4）；只有 #2 的"真笔误传播"是该修的残余。

---

## 9. Value Verdict（多维评定 · v0.2 上修）

| 评估维度 | v0.1 | **v0.2** | 一句话（变动理由）|
|----------|------|----------|------|
| 对 nano-agent 核心定位贴合度 | 5 | **5** | 双面承重基础设施，不是可选卫生 |
| 当前实现性价比 | 3.5 | **3.5** | 价值高、默认偏重、刚开始减重 |
| 对未来演进的杠杆 | 4 | **4.5** | ↑ 自蒸馏演化机制让它可持续自我维护 |
| 日用/可发现友好度 | 3 | **3** | README 前可发现性差、文档长 |
| 风险（rot/drift）可控度 | 4 | **4.5** | ↑ 看清 drift 多为健康演化，真风险面更小 |
| 可量化程度 | 2.5 | **2.5** | 仍仅代理指标 |
| LLM-native 创新度 | 4.5 | **5** | ↑ 输入↔输出闭环对称，业界全无对标 |
| **闭环自洽 / 输入-输出对称（新维度）** | — | **5** | prompt↔模板 co-design + 同构两层 + 自蒸馏 |
| **综合价值** | 4 | **4.5** | ↑ 升幅来自看到完整闭环与演化机制，非空言 |

---

## 10. 一句话结论

我之前低估了它，因为只看到一半。完整看，nano-agent 这套东西是**一个为"无持久记忆、需被驱动的异构 LLM 作者"量身造的、双面互锁、会自我蒸馏演化的闭环开发方法论**——输入端（prompt 剧本）与输出端（模板+文档）共享同一套"模板↔实例"架构，随开发逐阶段长大，核心收敛、外围流动、学习蒸馏回库而历史不改。这是人类团队框架（Diátaxis/ADR/RFC/PR-FAQ/C4）**全都只覆盖输出端、缺驱动端**的地方——**业界无对标的 LLM-native 价值**。综合 **4.5/5**：真实、领先、且活着。不该废除或推翻，而是**借业界之长补 onboarding/长度/状态机**，并把**自蒸馏纪律同样施加到输入端库**（蒸馏 1-temp→2-plan/3-exec、修真笔误、永不改史）——把"好"推到"优"，同时始终警惕仪式累积、守住"方法论服务产品、文档不脱节代码"的本分。

---

## 附录 A · 外部参考来源（Sources）

- Diátaxis：[diataxis.fr](https://diataxis.fr/)、[Start here](https://diataxis.fr/start-here/)
- ADR：[Martin Fowler · ADR](https://martinfowler.com/bliki/ArchitectureDecisionRecord.html)、[joelparkerhenderson/architecture-decision-record](https://github.com/joelparkerhenderson/architecture-decision-record)、[AWS · ADR process](https://docs.aws.amazon.com/prescriptive-guidance/latest/architectural-decision-records/adr-process.html)
- Oxide RFD：[RFD 1](https://rfd.shared.oxide.computer/rfd/0001)、[Oxide blog · RFD 1](https://oxide.computer/blog/rfd-1-requests-for-discussion)；Rust RFC：[rust-lang/rfcs](https://github.com/rust-lang/rfcs)、[The Rust RFC Book](https://rust-lang.github.io/rfcs/)
- Amazon PR-FAQ / Working Backwards：[workingbackwards.com · PR-FAQ](https://workingbackwards.com/concepts/working-backwards-pr-faq-process/)、[The Amazon Writing Culture](https://www.theprfaq.com/articles/amazon-writing-culture)
- Docs-as-code / doc-rot：[Kong · What is Docs as Code](https://konghq.com/blog/learning-center/what-is-docs-as-code)、[getdx · Code rot](https://getdx.com/blog/code-rot/)
- C4 / arc42：[arc42 FAQ B-17](https://faq.arc42.org/questions/B-17/)、[Comparing SW Architecture Documentation Models](https://dev.to/adityasatrio/comparing-software-architecture-documentation-models-and-when-to-use-them-495n)

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿（已删除）：只见输出端，定性为"文档系统"，综合 4/5 |
| v0.2 | 2026-05-30 | Opus 4.8 | **重写**：看到 `.anote/` 驱动端，重定性为**双面互锁闭环方法论**；新增输入-输出对称/co-evolution/自蒸馏；修正 drift 为健康演化；综合上修 4→4.5 |
