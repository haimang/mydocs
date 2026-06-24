# mydocs 文档体系价值评定（after-0624 · 大重组 + 毕业独立仓之后）

> **文档对象**：从 nano-agent 生长出来、并于 2026-06 毕业为独立仓 `mydocs` 的这套文档模板体系——含本轮（0624）对 `planning` / `qna` / `truth` 的大规模重组、新增与退役之后的**完整价值**。
> **作者**：Claude Opus 4.8（亲历本轮重组 + 通读 active 26 模板 + 对照 v0.2 价值评定 + 三支柱 CCMD 框架）
> **日期**：2026-06-24
> **文档性质**：`eval / state-analysis`（里程碑后现状快照 + 对账诚实 + 前瞻交接；**冻结零决策**——评定不替 owner 拍板）
> **文档状态**：`draft | reviewed | superseded`
> **结构来源（dogfood 自身模板）**：`eval-state-analysis` 骨架（§1-3 现状/对账/交接）+ `eval-retrospective §2 根因表`（§4 为何重组）+ `design §6 Tradeoff`（§8）+ `design §10 Value Verdict`（§10）+ `eval-gap-study 缺口台账`（§9）+ **`truth/per-cluster-value-proposition` 三态承诺 + T1-T4**（§7，自我 dogfood）+ `closure §8 价值/负债台账`（§6）
> **上游对照基线**：`propositions/value-proposition-of-template-docs.md` v0.2（2026-05-30，综合 **4.5/5**，定性"双面互锁闭环方法论"）· `CCMD-vs-SDD-by-opus.md`（三支柱：注意力/价值/成本异质 → 发散）· `nano-agent-vs-SDD.md`（code-as-truth 真源）

---

## 0. TL;DR / 一句话价值结论（相对 v0.2 的增量）

**v0.2 看到的是「双面互锁闭环方法论」（prompt 剧本 ↔ 模板/文档 co-design），综合 4.5。0624 的成熟做了两件大事，把价值往深处推、同时记上新债：**

1. **毕业为独立仓 `mydocs`**：output 端从 nano-agent 剥离、带完整历史 + 独立 remote + 独立版本线（本轮 5 笔干净分批已 push）。这把"它是不是可复用资产"从猜想变成**事实**——它现在能被任意项目 clone/submodule，不再寄生一个产品。
2. **装上第三条脊：真相奠基（truth-grounding）**。0624 把一个**统一、带 ID、互锁**的"真相"概念贯穿全链——`qna` 冻结 owner-gated `T-O` → `planning §2` CITE `T-O` 并记 reference-checked `T-R` → `truth/` 簇用 `T1-T4` 评系统真值层并 reverse-water 反假绿。体系由此从"**协调无状态 agent 的流程模板**"深化为"**一套真相奠基的决策-执行方法论**"。

**但要诚实**：毕业把 input 端（`.anote/` 剧本，仍在 nano-agent）与 output 端（mydocs）**切到两个仓**——v0.2 引以为头号价值的"双面互锁"现在**跨仓、独立版本化**（物理仍可解析，治理上解耦）；复杂度墙更高（23→26 模板 + 4 簇 + Truth-ID 命名空间）；`charter` 家族退役留下一个**多阶段纲领的概念缺口**；快速重组累积了**陈旧交叉引用债**。

**综合裁定（§10）：维持 4.5/5——价值更深、债也更明。** 真相奠基脊是真实的最大增益；跨仓互锁张力 + charter 缺口 + onboarding 墙是诚实的扣分项。

---

## 1. 调查方法与输入（相对 v0.2 变了什么）

| 路 | 内容 |
|----|------|
| 自身实测 | 亲历 0624 全部重组（建 truth/ 3 + planning 3 + qna 2、退役 charter/eval-planning/qna/design-neo/sketch/respond-*、重写 README v0.6、5 笔分批提交 push origin/main）|
| 对照基线 | v0.2 价值评定（4.5）+ 其 V1-V8 / C1-C5 / 缺口台账 / Value Verdict 矩阵 |
| active 普查 | 26 份 active（§1.3 README）+ 4 簇共有脊 + Truth-ID 命名空间（§4.2 README）|
| 框架对标 | 沿用 v0.2 的 Diátaxis/ADR/RFD-RFC/PR-FAQ/docs-as-code/C4 对照 |

> **诚实前提（沿用 v0.2）**：文档价值本质**反事实**；下面是代理指标 + 辨证判断，非直接 ROI。

---

## 2. 这次重组到底改了什么（交付价值台账）

| # | 改动 | 性质 | 价值动作 |
|---|------|------|----------|
| D-1 | `eval-planning`（一文件三态开关）→ `planning-{initial,proposed,final}` | 拆分·去开关 | 每态一张干净骨架；新增 **§2 规划真相台账 + §辨证调整溯因（驱动真相 Truth-ID）+ 双门渐进冻结** |
| D-2 | `qna`（身份写死 GPT问Opus答）→ `qna-{singular,progressive}` | 拆分·解耦 | **角色参数化中性槽**（消每次"反转"声明）+ second-opinion 三态 present/waived/retired + **truth-gate 产 T-O** + progressive 多轮锁死三件 |
| D-3 | 新增 `truth/` 子簇（3） | 净新能力 | **系统真值奠基 campaign**：T1-T4 + 7 点 rubric + 反假绿 + reverse-water + FE readiness 三态承诺 |
| D-4 | 新增顶层 `assessment` 簇（2）+ `report/`（2）+ `eval-README` | 归位·补缺 | design-prelude 前置研究 / 专科调查归 `report/` / 对外项目 README |
| D-5 | 退役 `charter`+`charter-lite`+`design-neo`+`design-sketch`+`respond-post-freeze`+`respond-verification` | 剪枝 | 体系学会"偏好专用形态、shed 仪式"；但 charter 留下纲领缺口（§6 C-7） |
| D-6 | **毕业独立仓 mydocs** + README v0.6 重写 | 资产化 | 独立 git 历史/remote/版本线；canonical 索引刷新（active 26 + Truth-ID 命名空间） |
| D-7 | Truth-ID 命名空间（`T-O`/`T-R`/`T-P` 贯穿 qna↔planning↔truth）| 架构脊 | 把"真相、谁冻的、如何约束工作、是否假绿"做成**一等、可追、互锁**的关切 |

---

## 3. 对账诚实 ★（声称 vs 真实 —— 灵魂段）

> 本体系自带"对账诚实"纪律，评定自己时更不能放水。

- **✅ 真交付**：planning/qna/truth 三簇**确实落盘 + 互链 + push**（commit `b76308f..5abf97d`，本地==origin/main）；Truth-ID 互锁**真接线**（qna 两形态都 `[[planning-*]]` 引用、planning §2 CITE T-O，自检命中）。不是 vaporware。
- **⚠ 声称 vs 真实的张力**：
  1. **"双面互锁"已跨仓**：v0.2 头号价值是 prompt↔模板 co-design。毕业后 `.anote/` 仍在 nano-agent、模板在 mydocs——**物理路径仍可解析**（nested 仓），但**两端独立版本化**，互锁从"同仓共生"降为"跨仓约定"。若 `.anote/` 剧本未同步指向新模板名（`planning-final` 而非 `eval-planning`、`qna-singular` 而非 `qna`），**驱动端会指向已退役模板**——这是 active 风险，非空言。
  2. **active 模板内含陈旧交叉引用**：eval 家族"何时不用→charter"、planning 头部历史措辞，指向已退役 `charter`/`re-design/`。README v0.6 已**显式登记**此 known-gap（§5 注），未掩盖，但**未就地修**——是 partial-delivery，不是 done。
  3. **truth/ 簇零实例验证**：模板已建，但**尚无一个真实 campaign 用新 `truth/` 模板跑出来**（既有 `clients/truth-grounding/` 是模板的抽取来源、非用新模板产出）。模板的价值是**设计推定**，未经一次完整 dogfood 实证——标 `T2`（离线对，未 live 重证），不冒充 `T1`。
- **frozen≠done**：README v0.6 `frozen` 是文档定稿，不等于"体系已稳态"——三簇都是 v0.1 模板，等首轮真实使用反馈。

---

## 4. 为什么这么改（根因表 · retrospective）

| # | 重组动作 | 根因（追到机制/认知层）| 类型 |
|---|----------|------------------------|------|
| R1 | 拆 eval-planning / qna 为专用形态 | **开关式单模板邀请漂移**——实测 MCCM 把 stage 字段丢了、6 份 qna 各写各的角色声明（认知：一个模板装多态，作者每次心算"填哪块"会漂）| 流程缺口 |
| R2 | 装 Truth-ID 命名空间（qna↔planning 互锁）| **决策溯源原本端到端、但"真相"散落**（qna 冻结、planning HEAD 实测、closure 收口各记各的）；统一 ID 把"真相是什么+谁冻的+如何约束"收成一条可追链 | 认知统一 |
| R3 | 建 truth/ 簇 | **反假绿原本是分散纪律**（state-analysis 对账、closure 诚实）；truth-grounding campaign 把"系统真值层 T1-T4 + reverse-water"制度化为独立能力 | 能力补缺 |
| R4 | 退役 charter | owner 实践中**charter 的定边界/冻决策角色被 planning 三态（scope/phase/exit）+ qna 双门（决策）吸收**；但"多月纲领/阶段触发"这半未显式安置（§6 C-7）| 边界迁移（含残债）|
| R5 | 毕业独立仓 | 体系成熟到**项目无关、可复用**——继续寄生 nano-agent 会让方法论演进淹没在产品 churn 里 | 资产化 |

> **教训沉淀**：0624 验证了 v0.2 §2.4 的"协同演化"论——**核心收敛（逐级辨证、code-as-truth、反假绿不变）、外围流动（模板形态重组）、学习蒸馏回库（开关→专用形态）**。这次蒸馏作用在 output 端模板自身。

---

## 5. 正面价值更新（V1-V8 承接 + V9/V10 新增）

> V1-V8 沿用 v0.2（持久记忆 / 异构多模型协调 / 决策溯源 / 漂移防御 / 模态纪律 / 测试治理 / fan-out / 闭环自蒸馏），**仍成立**。0624 新增两项：

- **V9 ·（新）真相奠基脊 + 反假绿一等化**。`T-O`/`T-R`/`T-P` 三类真相 + `T1-T4` + reverse-water + planning-final/qna-progressive 的**锁死台账**，把"别信二手 closure、对着代码验、假绿必点名留痕"从分散纪律升级为**贯穿决策→规划→评估的可追架构**。对"无状态异构 LLM 集群"这种**天然爱产假绿**的工作模式，这是稀缺且高杠杆的价值——直接服务 CCMD 三支柱里的"诚实"内核。
- **V10 ·（新）资产化 / 可复用毕业**。独立仓 = 可被任意项目复用 + 独立版本演进 + 可对外发布（对标 Diátaxis/ADR 那样的公开方法论）。v0.2 缺口表里的"可移植性未证"被本轮**部分兑现**（剥离成功；跨项目实用仍待首个外部使用者）。

---

## 6. 成本与反面更新（价值/负债台账）

> C1-C5 沿用 v0.2（token 开销 / 默认过冲 / 验证问题 / onboarding 墙 / 元工作增殖），0624 **加重 + 新增**：

| 级 | 项 | 0624 的变化 |
|---|----|-------------|
| 🔴 债 | **C4 onboarding 墙↑** | 23→26 模板 + 4 簇 + Truth-ID 命名空间 + 双门——**概念负载更高**；README v0.6 改善了"可发现性"（索引），但**未降低"可理解性"成本** |
| 🔴 债 | **C-7（新）charter 缺口** | 退役后**无 active 的多阶段纲领模板**（scope/phase/exit/trigger 的统一冻结面）；planning 是 per-子阶段策划链、qna 是决策点——都不是跨多阶段的纲领。foundation 级大阶段现无专用骨架 |
| 🟠 半债 | **C-8（新）跨仓互锁张力** | 双面互锁跨 nano-agent↔mydocs 两仓；需一次 `.anote/` 剧本同步（指新模板名）才能保互锁不空转（§3 ⚠1）|
| 🟠 半债 | **C-9（新）一致性债** | 快速重组累积陈旧交叉引用（→charter / re-design 路径）；已登记未修（§3 ⚠2）|
| 🟡 观察 | **C1 token/仪式↑** | 锁死台账（4 台账/AP、真相台账、锁死三件）对高风险震中值，对轻量工作是过冲——靠 `[可选]` 缓解但锁死部分强制 |
| 🟢 已偿 | C4 可发现性(索引) | README v0.6 补上 active 26 索引 + Truth-ID canonical——v0.2 缺口#（onboarding 索引）部分还债 |

---

## 7. 三态价值承诺（自我 dogfood `truth/per-cluster-value-proposition`）

> 用我们**刚建的 truth/ 模板**评估"产它的 mydocs 体系自己今天能承诺什么"——是否 live-proven（T1）还是设计推定（T2）。

### 🟢 今天能可信承诺（T1/强 T2 · 可放心据此工作）
- **决策溯源 + 真相互锁**：qna 冻 T-O → planning CITE，端到端可追（接线自检 live-green）。
- **资产独立性**：mydocs 独立仓/历史/remote 真实存在（push 实证）。
- **反假绿纪律**：对账诚实 / reverse-water / 锁死台账已制度化（多阶段实战沉淀，v0.2 已背书 V4）。
- **多模型协调**：身份解耦 qna + panel + 对抗复核（本轮即 3-6 路并行 agent 多次）。

### 🟡 部分承诺（T2 · 可建但须知缺口）
- **planning/qna/truth 三簇模板质量**：设计扎实、互链齐，但**零真实实例验证**（§3 ⚠3）——离线对，未经首轮 dogfood live。
- **onboarding 友好度**：有 README v0.6 索引，但概念负载高，新人/新项目上手成本未实测。

### 🔴 暂不能承诺 / 必须围栏
- **跨仓双面互锁**：未同步 `.anote/` 前，驱动端可能指向已退役模板——**不能假设 input↔output 仍无缝互锁**，须先做剧本同步。
- **多阶段 foundation 纲领**：charter 退役后**无 active 模板覆盖**——大阶段开纲领时勿假设有现成骨架（C-7）。
- **可移植到外部项目**：剥离成功 ≠ 别的项目能直接用；**无外部使用者实证**，勿宣称"通用方法论"已验证。

---

## 8. Tradeoff 辩证（核心取舍 · 0624 新增轴）

> v0.2 三轴（重双面 substrate / prompt↔模板互锁 / 流水带不可变）仍成立。0624 新增两轴：

1. **选「毕业独立仓」而非「留在 nano-agent 同仓共生」**
   - 为什么：资产化、独立演进、可复用、可发布。
   - 代价：双面互锁跨仓、独立版本化（C-8）；需剧本同步维护。
   - **重评条件**：若出现首个外部使用者 → 复用价值兑现、毕业值；若 `.anote/` 长期不同步 → 互锁空转、毕业反成割裂。← 最该盯。
2. **选「真相奠基重仪式（锁死台账 + Truth-ID）」而非「轻流程模板」**
   - 为什么：无状态异构集群爱产假绿；可追真相 + 反假绿防的是**最贵的返工与自欺**（呼应 CCMD 支柱三：省的是返工的钱）。
   - 代价：token/仪式↑、概念负载↑（C1/C4）。
   - **重评条件**：若轻量工作被锁死台账拖累 → 需更细的"按风险缩放仪式"判据（planning-final §3 R3 已起步）。

---

## 9. 缺口台账（按价值排序 · 0624 后该补的）

| # | 缺口 | 借鉴源/出处 | 建议 | 价值 |
|---|------|-------------|------|------|
| 1 | **`.anote/` 剧本未同步新模板名** | 自蒸馏纪律 | 过一遍剧本：`eval-planning→planning-*`、`qna→qna-singular/progressive`、`charter→planning+qna`；保跨仓互锁不空转 | 高 |
| 2 | **active 模板陈旧交叉引用（→charter / re-design）** | docs-as-code | 逐份模板下次保养时订正"何时不用"措辞（README §5 已登记）| 高 |
| 3 | **charter 缺口（多阶段纲领无 active 模板）** | RFC/charter 历史 | owner 裁定：要么承认 planning+qna 已够、要么补一份轻量 `phase-charter` | 高 |
| 4 | **truth/三簇零实例验证** | dogfood 纪律 | 下一个真值 campaign 用新 `truth/` 模板跑一遍，回填实证（T2→T1）| 中-高 |
| 5 | onboarding 可理解性（非可发现性）| Diátaxis | 加一份"5 分钟上手"用户向导览（区别于 canonical README）| 中 |
| 6 | 长度/不可变纪律（沿用 v0.2）| PR-FAQ/ADR | 模板软长度上限 + qna 接受即不可变双链 | 中 |
| 7 | 元工作增殖（propositions/ 已 10 份含本篇）| — | propositions 系列周期性收口冻结，防元层喧宾夺主 | 低-中 |

---

## 10. Value Verdict（多维评定 · v0.3 对 v0.2 上修/下调）

| 评估维度 | v0.2 | **v0.3(0624)** | 一句话（变动理由）|
|----------|------|----------------|------|
| 对核心定位贴合度 | 5 | **5** | 真相奠基脊让它更是承重基础设施 |
| 当前实现性价比 | 3.5 | **3.5** | 价值更深、仪式也更重，净持平 |
| 对未来演进的杠杆 | 4.5 | **5** | ↑ 毕业独立仓 = 可复用/独立版本/可发布 |
| 日用/可发现友好度 | 3 | **3** | README v0.6 补索引(↑)，但 26 模板+4 簇概念负载(↓)，净持平 |
| 风险(rot/drift)可控度 | 4.5 | **4** | ↓ 快速重组累积陈旧交叉引用 + 跨仓互锁张力，真风险面回升 |
| 可量化程度 | 2.5 | **2.5** | 仍代理指标 |
| LLM-native 创新度 | 5 | **5** | 真相奠基互锁 + 反假绿一等化，业界更无对标 |
| 闭环自洽/输入-输出对称 | 5 | **4.5** | ↓ 毕业把两端切两仓，互锁降为跨仓约定（output 端内部自洽↑，但双面对称↓）|
| **真相奠基深度（新维度）** | — | **5** | Truth-ID 贯穿 qna↔planning↔truth + 反假绿制度化 |
| **可移植/资产化（新维度）** | — | **4** | 剥离成功(↑)，外部使用者实证未有(留扣) |
| **综合价值** | 4.5 | **4.5** | 持平：真相奠基脊 + 毕业(增益) ⊖ 复杂度墙 + charter 缺口 + 跨仓张力(新债)|

---

## 11. 一句话结论

0624 没有推翻 v0.2 的判断，而是**把它推深一层、也照出新债**。这套从 nano-agent 长出来的 mydocs 体系，现在是**一套真相奠基的、毕业为独立资产的、双面（跨仓）互锁闭环开发方法论**——它把"无状态异构 LLM 集群最爱产的假绿与自欺"用一条可追的真相脊（`T-O`/`T-R`/`T1-T4` + reverse-water + 锁死台账）系统性地按住，这是人类团队框架（Diátaxis/ADR/RFC/PR-FAQ/C4 全只覆盖输出端、且无"反 LLM 自欺"层）**全无对标的 LLM-native 价值**。综合**维持 4.5/5：真实、领先、且在长**。但毕业把驱动端与产出端切到两仓、charter 退役留了纲领缺口、快速重组欠下一致性债——所以下一步不是再加新簇，而是**收口**：同步 `.anote/` 剧本（保互锁）、订正陈旧交叉引用、给 truth/ 三簇跑一次真实 dogfood 把 T2 兑现成 T1、并请 owner 裁定 charter 缺口。把"好"守住、把新债还掉，别让重组的速度跑赢卫生。

---

## 附录 A · 价值血脉（propositions 系列）

| 版本 | 文件 | 日期 | 综合 | 定性 |
|------|------|------|------|------|
| v0.1 | value-proposition-of-template-docs（已删）| 2026-05-30 | 4/5 | "文档系统"（只见输出端）|
| v0.2 | value-proposition-of-template-docs | 2026-05-30 | 4.5/5 | "双面互锁闭环方法论"（见驱动端）|
| **v0.3** | **本文（mydocs-value-proposition-after-0624）** | **2026-06-24** | **4.5/5** | **"真相奠基 + 毕业独立资产 + 跨仓双面互锁方法论"** |

## 附录 B · 外部参考来源

沿用 v0.2 附录 A（Diátaxis / ADR / Oxide RFD + Rust RFC / Amazon PR-FAQ / docs-as-code / C4·arc42）。三支柱 CCMD 框架见 `CCMD-vs-SDD-by-opus.md`；code-as-truth 真源见 `nano-agent-vs-SDD.md`。
