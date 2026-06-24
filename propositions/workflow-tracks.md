# 工作流轨道对比分析、推荐与 Verdict

> 文档对象：nano-agent 从 eval 到 action-plan 的**多条工作流轨道**——全谱对比、优缺点、分阶段推荐、当前工作流 verdict、重载轨 design 的再定位
> 作者：Claude Opus 4.8（综合本会话 5 份 re-design 调查 + MCX3-MCX4 实证 + charter-lite 自然实验）
> 日期：2026-05-30
> 文档性质：`eval / general-purpose`（辨证综合，冻结零决策）
> 文档状态：`draft — 待 owner 审阅`
> 上游证据（authoritative）：
> - `true-purpose-of-design-doc.md` — design 核心 = §7 验收 + §3 边界 + §1.1 术语 + §8 锚；§4/§9/§10 = 仪式
> - `better-planning.md` — eval-planning 三态 = 一个文档的三个成熟态
> - `eval-docs-re-design.md` / `design-sketch.md` / `more-templated-appendix.md`
> - 实证：MCX3-MCX4（combo 实跑：无 design、无 charter）、MIX-wave-1（charter-lite）、MID4↔MI4（重轨）

---

## 0. 一句话结论与 Verdict 速览

**owner 当前的工作流（combo 轨：eval-planning 三态 + reference-anchor + qna → action-plan，跳过 charter 与 design）处于合理、且对其目标场景接近最优的阶段。** 它不是"偷工"——它把 design 的不可替代核心**分发**到了更合适的文件，丢掉了仪式，并用 reference-anchor 堵住了 charter-lite 唯一的漏洞。MCX3-MCX4 是它跑通、被评审、已收口的实证。

**但它不是万能轨。** 它的适配区是"**在已建 substrate 上做扩展/附加的 sub-phase**"。一旦遇到**净新对外契约面 / 真正有争议的架构 / 安全信任边界 / foundation 多月阶段**，combo 轨的"叙述式契约规格 + 跨功能一致性 + 深度 tradeoff"会变薄甚至漏进 action-plan——此时需要**重轨**。

**改进潜力（3 条）**：① 把"轨道选择"从直觉变成**显式必要性测试**（防止在该用重轨的活上误用轻轨，如 MIX5 SSRF）；② combo 轨内给净新契约面留**逃生口**（§13.B 契约冻结 / 插一份 design-sketch）；③ **裸 charter-lite 可退役**，被 combo 轨取代（combo = charter-lite + reference-anchor，严格更强）。

**重载下 design 怎么调整**（owner 直接问的）：把重轨 design 砍成 **combo 覆盖不了的补集**——只保留①净新契约的**叙述式规格**（§7.2 prose）②**跨功能系统一致性**③**深度 tradeoff 辩证**（§6）④术语（§1.1）⑤净新架构边界（§3，仅净新时）；把 §4 外部参考、§8 锚、§9 决策**委派给 reference-anchor / qna**，删 §10。详见 §7。

---

## 1. 谱系基础：5 个能力维度

任何工作流，在进入 action-plan 前，都必须以某种形式产出/冻结这 9 类信息。问题只是"由哪份文件承载"：

| 能力 | 含义 | 重轨归属 | combo 归属 |
|------|------|----------|------------|
| **决策冻结** | owner 二元裁决（做哪个）| qna | qna |
| **scope/phase 边界** | 做什么/不做、相位职责、退出判据 | charter | eval-planning final |
| **架构边界（既有）** | 在已有代码上哪里砍/留/解耦/聚合 | design §3 | reference-anchor ARCH/TR |
| **仓内代码锚** | file:line 借鉴/反例 | design §8 | reference-anchor §1/§2 |
| **work-item 验收** | 每个工作项 exit/evidence | design §7 + action-plan | eval-planning final §6/§8 |
| **净新契约规格** | 全新对外契约 input/output/edge/schema（叙述）| **design §7.2** | ⚠️ §13.B / 测试面（薄）|
| **跨功能一致性** | N 个功能如何拼成一个整体形态 | **design（整篇）** | ⚠️ DAG（部分）|
| **深度 tradeoff** | 选 X 不选 Y 的争议性辩证 | **design §6** | reference-anchor TR（仅机制）|
| **外部参考对比** | vs codex/cc/cf-agents | design §4（已腐烂）| reference-anchor |

> 加粗 = combo 承载偏薄的三项（净新契约规格 / 跨功能一致性 / 深度 tradeoff）——这正是**重轨 design 的真身**（§7）。

## 2. 工作流轨道全景

按"仪式重量 / 模糊承载力"从轻到重，仓库里实际出现过 4 条轨：

### Track A · 单遍轻量（trivial）
`eval-general-purpose → action-plan`
- 适配：单文件级改动、无对外契约、无架构接缝、无 owner 决策。
- 实例：零散 housekeeping。

### Track B · charter-lite（light）
`eval → charter-lite（内含强制冻结 qna）→ action-plan`（跳过 design）
- 设计意图：design 的"消除模糊"由强制冻结的 qna 一次性补偿。
- 实例：MIX-wave-1（MIX1/2/3）。
- **已知漏洞**：charter-lite 显式丢掉 design 的 §3/§8 grounding（"不要求引用参照产品代码"）→ 高模糊活（MIX5 SSRF）的威胁模型/信任边界**漏进 action-plan**。

### Track C · combo / 三态（light+，owner 当前）★
`eval-planning(initial→proposed→final) + reference-anchor + qna → action-plan`（跳过 charter 与 design）
- 实例：**MCX3-MCX4（已跑通收口）**、MCS4+MCX6（进行中）。
- **= charter-lite + reference-anchor**：reference-anchor 补回了 B 丢掉的 §3/§8 grounding（ARCH 实测 + TR substrate-fit + file:line），**结构上堵住了 B 的漏洞**。MCX3-MCX4 没有 MIX5 式泄漏，正因边界先被 reference-anchor 冻住。

### Track D · 重轨（heavy）
`eval → full-charter → design(×N) + qna → action-plan`
- 适配：foundation、多月大阶段、净新契约面、争议性架构、onboarding 关键路径。
- 实例：MID1-7→MI、MCD1-7→MC、Z*/HP*/RH*/PP* 编号链。

## 3. 逐轨道优缺点对比

| 维度 | A 单遍 | B charter-lite | **C combo/三态** | D 重轨 |
|------|--------|----------------|------------------|--------|
| 进 action-plan 前的文件数 | 1 | 2 | 3（+ 三态= 3 份 planning 实例）| 2 + N 份 design |
| 决策冻结 | inline（弱）| qna（强制）| qna | qna |
| scope/phase | 无 | charter-lite | eval-planning final | full charter |
| 架构边界（既有）| 无 | **丢→漏** | reference-anchor ✓ | design §3 ✓ |
| 仓内锚 | 无 | **丢→漏** | reference-anchor ✓ | design §8 ✓ |
| work-item 验收 | inline | charter-lite ledger | eval-planning final ✓ | design §7 + AP |
| 净新契约规格 | 无 | **无→漏** | ⚠️ §13.B/测试面（薄）| design §7.2 ✓ |
| 跨功能一致性 | 无 | 无 | ⚠️ 部分（DAG）| design ✓ |
| 深度 tradeoff | 无 | 无 | TR（仅机制）| design §6 ✓ |
| 模糊承载力 | 极低 | 低 | **中**（净新契约处变薄）| 高 |
| 主要优点 | 最快 | 比重轨快、qna 硬闸防漏 | **快 + 有 grounding + 三态成熟可派生多 AP** | 承载净新/争议/叙述规格 |
| 主要缺点 | 几乎不防错 | 高模糊漏进 AP | 净新契约/跨功能一致性偏薄 | 重、慢、§4/§9/§10 仪式 |
| 适配区 | trivial | 小·低模糊·已有契约 | **sub-phase·扩展既有 substrate·≥2 AP** | foundation·净新契约·争议架构 |
| 实证 | — | MIX1（成）/ MIX5（漏）| **MCX3-MCX4（成）** | MID4↔MI4（成）|

**两条结论性观察**：
1. **C 严格强于 B**：C = B + reference-anchor，且 reference-anchor 正好补 B 的漏。除非连"借鉴"都不需要（纯内部 additive），否则没理由再用裸 B。→ **建议 B 退役/并入 C**。
2. **C 与 D 的真实分界 = "净新 vs 扩展"**：C 在"扩展已有 substrate"上接近最优（MCX3-MCX4 全是 additive：ARCH 反复显示"schema 已支持，只加一列/一读端点"）；D 的不可替代性只在"净新契约 / 争议架构 / 跨功能整体形态 / 叙述规格"上才显现。

## 4. 轨道选择决策树（把直觉变成显式测试）

> 现状：owner 凭直觉选轨。风险：在该用重轨的活上误用轻轨（MIX5 本该被"安全边界"挡回重轨，却漏进了 AP）。下面把它显式化。

**第一关 · 是否需要 charter（scope/phase/exit 纲领）？**
- foundation / 多月 / 多 sub-phase 需要统一纲领 → **需要 charter**（Track D，或 charter-lite 若模糊低）
- 单个 sub-phase / 附加章节，自身 scope 由 planning 承载即可 → **不需要独立 charter**（Track C 的 eval-planning final 即承载）

**第二关 · 是否需要 design（净新契约 / 争议架构 / 叙述规格）？满足任一即需要**（canonical：见 `docs/templates/README.md` §3.6，与 `charter-lite §1.4` 逐字一致）：
1. 新增**对外 contract surface**（从零定义，非扩展既有）
2. 新增**架构接缝**（净新 decouple/aggregate；reference-anchor 无既有 ARCH 可锚）
3. **跨 worker 不变量 / 多功能必须拼成一个整体形态**
4. 验收是**多字段 / 非显然**的（一两句 QNA 答不清“做完长什么样”）
5. 涉及**安全信任边界**（威胁模型）—— 强制升级
6. **onboarding 关键**：需新贡献者读懂的叙述式契约

→ 命中任一 → **需要 design（重轨 D，或在 C 内插一份 design-sketch）**
→ 全不命中 → **Track C（combo）足矣**；连借鉴都不需要 → Track B/A

```text
            ┌─ 需要统一纲领(foundation/多月/多sub-phase)? ─ 是 ─▶ 含 charter
   work ───▶│
            └─ 否 ─▶ 单 sub-phase
                      │
                      ├─ 命中"design 必要性测试"任一条? ─ 是 ─▶ 重轨 D / 或 C 内插 design-sketch
                      │
                      └─ 否 ─▶ Track C(combo) ◀── owner 当前默认，正确
                                  └─ 连借鉴都不需要 ─▶ Track B/A
```

## 5. 分执行阶段的推荐

| 工作阶段类型 | 推荐轨 | 理由 |
|--------------|--------|------|
| Foundation / 契约冻结 / 多月大阶段 | **D 重轨** | 净新契约 + 跨功能整体形态 + 叙述规格 + onboarding |
| 能力建设·扩展既有 substrate（≥2 AP）| **C combo** ★ | MCX3-MCX4 模式；reference-anchor 锚既有、三态派生多 AP |
| 净新对外契约面的 sub-phase | **C + design-sketch** | C 主体 + 一份 design-sketch 承载净新契约（§13.B 或 design-sketch）|
| 测试体系治理 / spike | **C combo**（eval-planning）| MCS3/MCS4 模式；治理无对外契约 |
| 安全 / SSRF / 信任边界 | **D 重轨**（强制）| 威胁模型必须显式冻结，不可漏进 AP（MIX5 教训）|
| Hotfix / 清理 / housekeeping | **B / A** | 低模糊、无契约 |
| 附加章节（MCX/MIX/MCS 这类 X 簇）| **C combo** ★ | 本就是 C 的诞生场景 |

## 6. VERDICT：owner 当前工作流是否合理 + 改进潜力

### 6.1 评价：合理，且对其目标接近最优

- **合理性**：✅ Track C 对"扩展既有 substrate 的 sub-phase"是**结构完备**的——9 类能力它覆盖 6 类强、3 类（净新契约/跨功能/深 tradeoff）在 additive 场景下用不到。MCX3-MCX4 实证：跑通、评审、收口，无 charter-lite 式泄漏。
- **相对优越性**：✅ C 严格强于 B（堵住 grounding 漏洞），比 D 快得多且无 §4/§9/§10 仪式。这是 **charter-lite 的正确进化版**。
- **它独立印证了我的 design 分析**：owner 没保留 design 文件，而是把 design 的核心**分发**（§3/§8→reference-anchor、§9→qna、§7/scope→eval-planning final）、丢掉仪式（§4/§10）。这正是"refocus design"的更彻底实现。

### 6.2 改进潜力（3 条，都不是推翻，是加固）

1. **显式化轨道选择**（高价值）：把 §4 的"design 必要性测试 6 条"写成开工前 checklist。**防的是"在该用 D 的活上误用 C"**——尤其安全边界（第 5 条）。MIX5 就是反例：它用了轻轨（B），威胁模型漏进 AP。代价极低、收益高。
2. **C 轨内的净新契约逃生口**（中价值）：当一个 sub-phase 恰好有一处净新契约，不必整轨升 D——在 eval-planning final **§13.B contract-surface-freeze** 显式冻该契约，或插一份 **design-sketch** 只覆盖那一处。让 C 有梯度，而非"要么 C 要么 D"硬墙。
3. **退役裸 charter-lite，并入 C**（低价值·整洁）：C = B + reference-anchor 且更强；保留 B 只增认知负担。除非"连借鉴都不需要"的纯内部 additive，否则默认 C。

> **Verdict 一句话**：owner 当前工作流处于**合理且接近其目标最优**的阶段；改进不在"换轨"，而在"把轨道选择显式化 + 给 C 留净新契约逃生口 + 退役冗余的 B"。

## 7. 重载下 design 文件应如何调整（owner 直接问的）

**核心原则：当 C 已经把 design 的一半活分发掉之后，重轨 D 的 design 就该收缩成"C 覆盖不了的补集"——只做净新、争议、跨功能、叙述这四件 C 做不好的事。**

### 7.1 重轨 design 应**保留并强化**的（C 的薄弱区 = design 的真身）

| 保留项 | 为什么只有 design 能做 | 相对现状 |
|--------|------------------------|----------|
| **§7.2 净新契约叙述规格**（input/output/core-logic/edge-cases/schema 的 prose）| reference-anchor 锚的是**既有** ARCH；净新契约无既有可锚，必须有人**从零叙述** | 强化：明确"仅净新契约面才填，扩展既有则指向 reference-anchor ARCH"|
| **跨功能系统一致性**（N 个功能拼成一个整体形态）| eval-planning 的 per-work-item 台账只见树木；combo 看不到"整片森林的形状" | **新增/提升为 design 的首要价值**——这是 combo 结构上最缺的 |
| **§6 深度 tradeoff 辩证**（选 X 不选 Y · 争议性架构）| reference-anchor TR 只裁"机制是否适配"，不做争议性方案对比；qna 只记结论不留辩证 | 保留（仅争议架构时填，非争议可省）|
| **§3 净新架构边界**（净新 decouple/aggregate 点）| 既有边界由 reference-anchor ARCH 承载；**净新**边界无 ARCH 可锚，须 design 定义 | 收缩：只在净新时填，扩展既有则委派 reference-anchor |
| **§1.1 术语对齐** | 唯一权威消歧（如禁掉不存在的枚举）| 保留 |

### 7.2 重轨 design 应**委派/删除**的（C 的三文件已做得更好）

| 删/委派项 | 去向 | 理由 |
|-----------|------|------|
| §4 外部三方对比 | **委派 reference-anchor** | 命名三件套已腐烂（mini-agent 列 4/5 空）；reference-anchor 是它的正经家 |
| §8 仓内代码锚 | **委派 reference-anchor** | reference-anchor §1/§2 就是 file:line 锚台账 |
| §9 决策登记 | **委派 qna** | action-plan 一律绕过 design §9 直引 qna；只留"本文新生决策 + 指针"|
| §10 Value Verdict | **删** | 自评仪式，下游不消费 |
| work-item 级 exit | **让 eval-planning final / action-plan 承载** | design 给契约规格，不给执行台账 |

### 7.3 调整后的"重轨 design" = 净新契约 + 系统一致性 + 深 tradeoff doc

一句话定义重轨 design 的新身份：

> **它是处理"净新与争议"的文档——只在 C 轨承载不了的地方出现：从零定义对外契约的叙述规格、把多功能拼成一个可理解的整体形态、对争议性架构做深度辩证。其余（既有边界/锚/决策/参考）全部委派给 reference-anchor + qna + eval-planning。**

这样，**即使在重轨，design 也不再是"什么都装的大文件"，而是与 reference-anchor / qna / eval-planning 并列的、只管净新与一致性的专科文件**。它的价值因此**最锐利**——因为它只在自己不可替代的地方出现。这恰好回答 owner："design 在重载下如何更好实现自身价值"——答案是**做减法**，把它收缩到 combo 永远做不到的那三件事上。

### 7.4 落地形态建议

- **轻净新**（一两处净新契约）：不升重轨，在 C 内用 **design-sketch**（§7 验收 + §3 边界 + 净新契约规格，已建模板）。
- **重净新 / foundation**：重轨 D，design 按 §7.1/§7.2 refocus（保留净新契约规格 + 系统一致性 + 深 tradeoff + 术语 + 净新边界；委派其余）。
- **统一动作**：把 `design.md` 模板按 §7.2 删 §10、§4/§8/§9 降级为"委派指针"，新增显式的"跨功能系统一致性"段，并在头部写明"扩展既有 → 用 C；净新/争议 → 用本模板"。

## 8. 一句话结论与给 owner 的决策问题

**一句话**：owner 的 combo 轨处于合理且接近最优的阶段，是 charter-lite 的正确进化版；它不需要换轨，只需要**把轨道选择显式化、给净新契约留逃生口、退役冗余的裸 charter-lite**。而重轨 design 的正确调整是**做减法**——收缩成"净新契约规格 + 跨功能系统一致性 + 深度 tradeoff + 术语 + 净新边界"的专科文件，把既有边界/锚/决策/参考全部委派给 reference-anchor + qna + eval-planning，从而在重载下让 design 的价值最锐利。

**3 个决策问题**：
1. **是否把 §4 的"6 条 design 必要性测试"立为开工前 checklist**（C vs D 的显式判定），并把安全边界设为强制升重轨条款？
2. **是否退役裸 charter-lite**，以 Track C（combo）为唯一轻轨默认？
3. **是否按 §7 refocus `design.md`**（删 §10、§4/§8/§9 委派、新增"跨功能系统一致性"段、限定为"净新/争议"专用），让重轨 design 与 reference-anchor/qna/eval-planning 并列分工？

---

## 附录 A · 四轨速查

| | A 单遍 | B charter-lite | C combo/三态 ★ | D 重轨 |
|---|---|---|---|---|
| 文件组合 | eval-gp → AP | eval + charter-lite(qna) → AP | eval-planning三态 + reference-anchor + qna → AP | charter + design×N + qna → AP |
| 跳过 | charter+design | design | **charter+design** | — |
| grounding(§3/§8) | 无 | 丢→漏 | reference-anchor ✓ | design ✓ |
| 净新契约 | 无 | 无→漏 | 薄（§13.B/sketch）| design §7.2 ✓ |
| 适配 | trivial | 小·低模糊 | 扩展既有·sub-phase ★ | 净新·争议·foundation |
| 状态 | 保留 | **建议退役→C** | **当前默认，合理** | 保留，design 按 §7 refocus |

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：四轨全谱对比 + 决策树 + 分阶段推荐 + combo 轨 verdict（合理/接近最优）+ 重轨 design 做减法的再定位 |
| v0.2 | 2026-05-30 | Opus 4.8 | 增补 §9–§11：active 模板文档矩阵（22 个）+ 逐文件使用分析 + 8 处断层与可提高空间（含 action-plan.md 上游词表过时这一真断层）|

---

# 增补（v0.2）：文档矩阵 —— 构建 action-plan 应该用什么文档

> 回应 owner：判断"什么时候用什么文档引导构建 action-plan"，给出 active 模板矩阵 + 逐文件用法 + 断层/改进空间。
> **重要前置**：owner 已把 `investigation.md / code-review-eval / code-megafile-header / composition-factory.ts / _TEMPLATE-spike-finding / issue-closure-fax9 / wrangler-worker.toml` 移入 `docs/templates/legacy/`——这独立印证了本会话结论（如 investigation 的"外部 CLI 深析"已被 eval-gap-study/reference-anchor 覆盖）。下表只列 **active 集（22 个）**。

## 9. 文档矩阵（active 22 个 · 按家族）

| 文档 | 家族 | 轨 | 在"进 action-plan"前的角色 | 何时用（触发）| 成熟度 |
|------|------|----|------------------------------|----------------|--------|
| `eval-general-purpose` | eval | A·兜底 | 提案"做什么"（冻结零）| 轻量单次 scoping / 长尾兜底 | 🟠 新 |
| `eval-planning` | eval | C | 三态(initial→proposed→final)成熟 → 派生多 AP | 子阶段需 **≥2 份 AP** | 🟡 已 dogfood 1 次(MCS4+MCX6) |
| `eval-reference-anchor` | eval | C·D | grounding 锚台账（ARCH/TR/file:line + 借鉴 verdict）| 需借鉴/grounding 非平凡 | 🟠 新 |
| `eval-gap-study` | eval | charter 前 | 我方缺口台账（对照参考）| 进 charter 前找"缺什么" | 🟠 新 |
| `eval-state-analysis` | eval | **周期铰链** | 交付快照 + 对账诚实 + 前瞻交接 | 里程碑/相位完成后 | 🟠 新 |
| `eval-feasibility-study` | eval | 任意轨前 | go/no-go 探针（token 化结论）| gate 单个关键决策 | 🟠 新 |
| `eval-retrospective` | eval | 学习 | 失误复盘（时间线+根因+教训）| 走错路并纠偏后 | 🟠 新 |
| `charter` | charter | D | 重轨纲领（scope/phase/exit/trigger）| foundation/多月/多 sub-phase | 🟢 成熟 |
| `charter-lite` | charter | B | 轻 charter + 决策冻结(qna) + design-necessity 闸 | 小·低模糊·扩展既有·无净新 | 🟠 刚重写 |
| `design-neo` | design | D | 净新契约规格 + **跨功能一致性** + 深 tradeoff | 重轨净新/争议架构 | 🟠 新 |
| `design-sketch` | design | C 内 | 单簇净新补丁 | combo 主体 + **一处**净新 | 🟠 新 |
| `design`（原版）| design | D | 全量（含已腐烂 §4/§10）| 特殊/历史；**新工作改用 design-neo** | 🟢 但 legacy 候选 |
| `qna` | 决策 | **全轨** | **owner 决策唯一真源**（register）| 任何需 owner 拍板 | 🟢 成熟 |
| `action-plan` | 执行 | **全轨终点** | 执行序列（phase/工作项/测试/收口）| 落地 | 🟢 但上游词表过时(断层#1) |
| `code-review-respond` | respond | review 后 | 实现者逐项回应（append §6）| 修复 code-review 后 | 🟢 成熟 |
| `respond-execution-log` | respond | AP 后 | 执行日志回填（append §9）| AP `executed` 后 | 🟠 新 |
| `respond-post-freeze` | respond | design/eval 后 | 冻结后补强（不重开冻结）| frozen 后 owner 触发 | 🟠 新 |
| `respond-verification` | respond | design/eval | 代码碰撞核实矩阵 | 冻结前对抗自检 | 🟠 新 |
| `code-review` | review | impl 后 | 评审制品 + verdict | 评审 design/AP/code | 🟢 成熟 |
| `closure` | 收口 | 阶段末 | 收口 + 价值/负债台账 + handoff | 阶段完成 | 🟢 成熟 |
| `api-compliance` | 专科 | 横切 | API 合规审查 | API surface 审查 | 🟢 成熟 |
| `bug-analysis-report` | 专科 | 横切 | bug 根因分析 | bug 调查 | 🟢 成熟 |

## 9.1 按轨道的"进 action-plan 前文档组合"速查

| 轨 | 进 action-plan 前应有的文档组合 |
|----|--------------------------------|
| **A 单遍** | `eval-general-purpose` → action-plan |
| **B charter-lite** | `eval`（+ 可选 `eval-reference-anchor` 若 grounding 非平凡）→ `charter-lite` → action-plan |
| **C combo ★** | `eval-planning`(三态) + `eval-reference-anchor` + `qna`（+ `design-sketch` 若一处净新）→ action-plan |
| **D 重轨** | `eval-gap-study`/`eval-state-analysis` → `charter` + `design-neo`(×N) + `eval-reference-anchor` + `qna` → action-plan |
| **回填/闭环（全轨）** | action-plan→`respond-execution-log`；impl→`code-review`→`code-review-respond`；阶段末→`closure`→`eval-state-analysis`(开下周期) |

> **周期是闭环的**：`eval-state-analysis` 既收尾上一周期、又作下一周期的 STEP-1 eval（铰链）。

## 10. 逐文件使用分析（非显然处的用法注记）

- **eval 七件套的分流**：planning→C（多 AP）；reference-anchor→C/D 的 grounding；gap-study→喂 charter（D 前）；state-analysis→周期铰链；feasibility→gate 单决策；retrospective→学习；general-purpose→兜底。**对照外部 CLI 本身**已无 active 模板（investigation 入 legacy）——若需读外部参考，用 reference-anchor（借鉴锚）或 gap-study（我方缺口对照）。
- **design 三件套的判定**：扩展既有→无 design（combo 三件套足）；combo 内一处净新→design-sketch；重轨多净新/争议→design-neo；要全量仪式→design（不推荐新用）。
- **qna 是唯一决策真源**：design-sketch / eval-planning / charter-lite 里的"内嵌 QNA"都必须**指向 qna register**，不另立真源。决策只活在 register，引用方只看 `Q 编号 + 业主回答`。
- **respond 四件套是 append-only 章节**，不是独立文档：execution-log 挂 action-plan §9、post-freeze 挂 design/eval 续号、verification 挂附录、code-review-respond 挂 review §6。
- **closure ≠ state-analysis**：closure 给阶段下收口裁定；state-analysis 回看交付现状 + 开下周期。二者一前一后接力。

## 11. 断层与可提高空间（8 处，按价值排序）

| # | 断层 / 改进点 | 性质 | 建议 |
|---|---------------|------|------|
| **1** | **`action-plan.md` 上游词表过时（真断层）**：它成稿于 4-27，§0/§6 只认 "design / QNA"，**不认** eval-planning final / reference-anchor / design-neo / design-sketch；§9 执行日志也未指向 `respond-execution-log`。| 结构断层 | **改 action-plan.md §0/§6**：按轨枚举合法上游（A/B/C/D 各自的输入组合，= §9.1）；§9 指向 respond-execution-log。**最高优先，最具体。** |
| **2** | **`design.md` vs `design-neo` 冗余**：两个重轨 design，"何时用 design.md"理由薄（§4/§10 已腐烂；investigation 入 legacy 同源印证）| 冗余 | design.md 头部标 **"legacy 候选；新工作用 design-neo"**；或择期移入 `legacy/`。 |
| **3** | **appended-section 家族不完整**：respond-* 建了 3 + code-review-respond；但 `more-templated-appendix.md` 还推荐 **qna freeze-declaration 尾块、design 讨论记录段、`_revision-history` 共享 snippet** —— 未建 | 缺件 | batch 2：充实 `qna.md`(freeze 尾块) + `design-neo`(讨论记录) + 抽 `_revision-history` 共享片段 |
| **4** | **13 个新模板未 dogfood**（仅 eval-planning 跑过 1 次）| 成熟度断层 | 各用 ≥1 历史文档回填验证（SA→state-analysis-after-MCX4、gap→api-gap-study、neo→某 MID、sketch→某净新簇、respond-*→某 executed AP）|
| **5** | **单-AP 中量活的最轻路径曾模糊**：A(trivial) 与 C(≥2 AP) 之间的"1 个 AP、中量、扩展既有" | 已澄清 | 走 **B(charter-lite)**；已写入 §9.1，不再是空档 |
| **6** | **track-selector 无单一权威家**：necessity test 散在 workflow-tracks §4 + charter-lite §1.4 | 治理 | 本矩阵 + §4 决策树 = **正式 router**；可抽一张一页"intake 卡"贴在 templates README |
| **7** | **qna register vs 内嵌 QNA 的真源歧义** | 纪律 | 各模板已要求内嵌 QNA 指向 register；矩阵 §10 重申"决策只活在 register" |
| **8** | **无 templates README/索引**：22 个 active + legacy/ 无总览入口 | 可发现性 | 加 `docs/templates/README.md`：家族分组 + §9 矩阵 + §4 决策树链接 |

### 11.1 改进优先级建议

1. **先做断层 #1**（action-plan.md 上游词表）——它是唯一会让"新轨产出的文档接不进 action-plan"的真结构断层，且改动小、最具体。
2. **再做 #2 + #8**（design.md 标 legacy + 加 templates README/索引）——便宜、提可发现性。
3. **#3 + #4**（补全 respond 家族 + dogfood 新模板）——中等投入，巩固新体系。
4. #5/#6/#7 已基本由本矩阵闭合，属"重申/固化"。

### 11.2 一句话 verdict（文档体系层面）

active 22 个模板**覆盖了四轨从 eval 到 action-plan 的全部承载需求，无功能性缺口**；唯一的**真结构断层是 `action-plan.md` 的上游词表过时**（新轨产出物在 action-plan 模板里"无名分"）。其余多为"新模板待 dogfood""家族待补全""索引待建"的**成熟度/完整度**问题，非断裂。**建议先修 #1，其余按 §11.1 顺序固化。**
