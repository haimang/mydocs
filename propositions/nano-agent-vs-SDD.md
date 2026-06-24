# nano-agent 方法论 vs. Spec-Driven Development（SDD）—— 辨证对比

> 文档对象：owner 这套 "prompt 剧本 + 文档模板闭环" 方法论 与 业界 **Spec-Driven Development（SDD）** 的异同、价值取向、可借鉴点
> 作者：Claude Opus 4.8（SDD 三大代表 web 调研：GitHub Spec Kit / AWS Kiro / Tessl + SDD 批评面 + 与本仓现状对照）
> 日期：2026-05-30
> 文档性质：`eval / gap-study`（对照参考找异同，冻结零决策）
> 文档状态：`draft | reviewed | frozen | superseded`
> 结构来源（dogfood 自身模板）：`eval-gap-study` 对照骨架 + `design §6 Tradeoff` + `design §10 Value Verdict`
> 上游输入：本会话 re-design 六件套 + `value-proposition-of-template-docs.md`(v0.2) + `.anote/` prompt 剧本认知 + 外部 web 调研

---

## 0. TL;DR / 一句话结论

**你的直觉对：它"像 SDD 但不是 SDD"。同源、不同宗。**

- **同源**：两者都是 2025 年对 **vibe-coding**（"描述目标→拿一坨看着对其实不对的代码"）的**结构化反动**——都"先规格、后代码"，都用 markdown 制品分阶段喂 AI，都有 constitution/charter 式的项目 DNA。
- **不同宗（最深的一条轴）**：**SDD 赌"spec 是唯一真源、代码是派生物（可从 spec 重生成）"；你赌"代码是真源、文档是外部记忆/协调/计划，且必须诚实地对账于代码"。** 这是**认识论的反转**。你那条 `state-analysis 对账诚实 / frozen≠done / 占位猎杀`纪律，恰恰把代码当 ground-truth、把文档当"可能漂移的声称"——与 SDD 的"从 spec 重生成代码"**正好相反**。
- 另外两条让你"不是 SDD"的：**多模型 panel**（SDD 是单 agent）+ **owner 是指挥而非 spec 作者**（你写驱动 agent 的 prompt，agent 才写规格类文档）+ **工序编码在 prompt 库里而非工具里**（tool-agnostic）。

**裁定（§8）**：你造的是 SDD 的**同辈/堂亲**——可命名为"**指挥驱动的多 agent 开发 · 代码为真源**（conductor-driven, code-as-truth multi-agent development）"。它有 SDD 的结构纪律，**没有** SDD 的 spec-primacy 赌注，**多出** SDD 没有的多 agent 协调层与防腐对账层。两者各自在不同约束régime下占优。

---

## 1. 调查方法与输入

| 路 | 内容 |
|----|------|
| SDD 定义与代表 | GitHub **Spec Kit**（/constitution→/specify→/plan→/tasks→/implement）、AWS **Kiro**（requirements/design/tasks + EARS）、**Tessl**（specs-as-primary-artifact）|
| SDD 批评面 | "dressed-up waterfall"、多 agent 仪式过重、role-switching 困扰单模型、迁移撞 context limit、工具锁定、多文件/分布式任务 AI Pass@1 仅 19.36% |
| 本仓现状 | re-design 六件套 + value-proposition v0.2 + `.anote/` 三层 prompt 剧本 |

---

## 2. SDD 是什么（带 Sources）

**核心定义**（Thoughtworks/Tessl/IBM）：SDD = "一份可执行、纳入版本控制的**规格**——而非代码——是**唯一真源**"。规格**权威**、代码**派生**；"维护软件 = 演化规格，代码是 last-mile"。SDD 于 2025 年作为对 vibe-coding 失败模式（看似可信、却偏离意图、幻觉 API、随规模腐烂）的回应而兴起。

三大代表：
- **GitHub Spec Kit**（开源，30+ agent）：`/constitution`（项目 DNA：栈/命名/分层/允许库/auth/logging）→ `/specify`（要什么）→ `/plan`（技术方案）→ `/tasks`（可执行任务表）→ `/implement`。每阶段产 markdown 喂下一阶段。
- **AWS Kiro**（agentic IDE）：`requirements.md`（**EARS 记法**的 user story + 验收：`WHEN <trigger> THE SYSTEM SHALL <response>`，源自 Rolls-Royce）→ `design.md`（架构 + 时序图）→ `tasks.md`（按依赖排序）。
- **Tessl**："specs—not code—are the primary artifact；agents generate code to match。"

---

## 3. 相同点（共享 DNA）

| 维度 | SDD | nano-agent |
|------|-----|------------|
| 反 vibe-coding、先规格后代码 | ✅ | ✅ |
| 多阶段流水线 + markdown 制品逐级喂 | spec→plan→tasks→implement | eval→charter→design→qna→action-plan→code→closure |
| 项目 DNA / 治理基线 | /constitution | charter + canon README + 硬纪律 |
| WHAT / HOW 分离 | spec/design ↔ tasks | design ↔ action-plan |
| 模型/工具无关倾向 | Spec Kit 支持 30+ agent | prompt-loop 任何模型/harness 可跑 |
| 结构化模板 + 质量清单 | Spec Kit 内置 | 23 模板 + code-review/closure |

**所以你"觉得像 SDD"不是错觉——骨架确实同源。**

---

## 4. 不同点（让你"不是 SDD"的 7 条，#1 最深）

| # | 轴 | SDD | nano-agent | 性质 |
|---|----|-----|------------|------|
| **1** | **真源（最深）** | **spec 是真源，代码派生、可从 spec 重生成** | **代码是真源，文档是外部记忆/协调/计划，须对账于代码**（state-analysis 诚实纪律）| **认识论反转** |
| 2 | 作者数 | 单 agent（一个 session 一个 agent）| **异构多模型 panel** + 独立纪律 + 对抗二轮 | 结构性不同 |
| 3 | 人的角色 | 人**写 spec** | owner **写驱动 agent 的 prompt**，agent 才写规格类文档；owner 只裁决（qna）| 元层更高 |
| 4 | 工序载体 | 编码在**工具**（slash 命令 / IDE）| 编码在**可复用 NL prompt 库**（`.anote/`）+ 模板 | tool-agnostic vs tool-locked |
| 5 | 后端治理 | 多止于 `/implement` | 富 closure + **state-analysis 防腐** + seam/测试治理 + deferred 台账 | 防腐/审计更重 |
| 6 | 持久核 | **spec** 持久 | **qna register（冻结决策）** 持久；design/action-plan 可被 supersede；代码为真 | "什么活得最久"不同 |
| 7 | 演化方式 | 随**厂商产品**升级 | 模板+prompt **随开发协同演化**（化石 ledger + 蒸馏回库）| 内生 vs 外生 |

> **关键巧合**：SDD 的一条公开批评是"agent role-switching 困扰 context-limited 模型"。你的 panel **恰好规避了它**——不在一个 session 内切角色，而是**用不同模型/会话各担一角**。你等于在 SDD 还没解的弱点上，先走了一步。

---

## 5. 各自价值取向上的优势（辨证，公平给分）

### 5.1 SDD 占优的场景
- **单人 + 单强 agent** 的 greenfield 功能生成。
- **想要"重生成"** 的场景:规格够精确 → 改 spec 即重生成代码（**对 port/refactor 极强**——讽刺的是,这正是你 smind 迁移的命门,见 §6）。
- **IDE 工效**:slash 命令、即时反馈,上手快。
- **EARS** 给验收条件机器可测的严谨。
- 真源在 spec → "演化 spec、代码作 last-mile" 的长期可维护性叙事。

### 5.2 nano-agent 占优的场景
- **多 stateless 异构模型 + 一个指挥**:panel 抵消单模型盲点;prompt 库让任意模型可接。
- **多会话 + context-compaction**:文档=外部记忆(SDD 的单 session 不直接解这个)。
- **诚实关键 / 反"文档剧场"**:代码为真源 + 对账诚实,挡住"spec 好看但代码偏离"。
- **跨项目/跨范式可移植**:tool-agnostic 闭环已实证迁到 smind(CF 分布式→本地 Python)。
- **重验证/重收口**:closure + state-analysis + seam 治理远强于 SDD 的"止于 implement"。
- **一人指挥巨型多-worker 产品**:owner 用 prompt 调度一支 fleet。

> 一句话:**SDD 赌"一个强 agent + spec 为真";你赌"许多 stateless agent + 代码为真 + 指挥"。约束régime不同,各自为王。**

---

## 6. 可借鉴（从 SDD 拿什么,4 条;#1 直接补我们上一轮发现的缺口）

| # | 借鉴点 | 来源 | 怎么用（守住"代码为真源"的前提下） | 价值 |
|---|--------|------|-------------------------------------|------|
| **1** | **"重生成 spec" 专用于迁移/refactor** | SDD spec-as-regenerable | 全局仍代码为真;但**迁移类任务**(如 smind CF→Python)引入一份**行为级 regeneration spec**——精确到能"重生成目标 + 行为 diff"。**这正补 v0.2 §8 的"迁移保真"缺口**:把"原系统↔新系统行为对账"设成 closure 硬闸 | 高 |
| 2 | **EARS 记法** 用于验收格栅 | Kiro | `design-neo §6 验收格栅` / `收口目标` 采 `WHEN <trigger> THE SYSTEM SHALL <response>`,让"做完长什么样"机器可测 | 中-高 |
| 3 | **slash 命令 / CLI 工效** | Spec Kit | 把 `.anote/` prompt 库包成 slash 命令/薄 CLI,实例化从手工复制变填表——**降本 + 灭 `af-agents` 这类手抄笔误**;但保留 NL 库,**不学 SDD 的工具锁定** | 中 |
| 4 | **单一 /constitution 文档** | Spec Kit | 每个项目一份显式"宪章"(= canon README + charter 硬纪律合并),**尤其利于 smind 式跨项目迁移**:新项目开局先立 constitution | 中 |

---

## 7. Tradeoff 辩证（最深的那条轴：spec 为真 vs 代码为真）

**我们选"代码为真源 + 文档为记忆/协调/计划",而不是 SDD 的"spec 为真源、代码可重生成"**
- **为什么**:开发者是**无持久记忆的异构 LLM 集群**。SDD 的"代码可从 spec 重生成"要求 spec 精确到近乎形式化、且单一强 agent 能可靠重生成;在 stateless 多模型régime下,更稳的是**承认代码是唯一不会幻觉的真相**,文档只做记忆与协调,并**持续对账**(挡文档剧场)。
- **我们接受的代价**:① 失去"改 spec 即重生成"的强迁移能力(→ §6.1 借鉴补);② 文档不能被信过代码,验证压力常在(owner 是 ground-truth 瓶颈)。
- **未来重评条件(关键)**:**当 agent 足够强 + 足够 stateful(可靠长期记忆/对代码 RAG),"代码为真"的诚实税下降,可向 SDD 的 spec-primacy 收敛**——这与 value-prop v0.2 §7 的重评点同源。**简言之:模型越强越稳,越该靠近 SDD;模型越多越健忘,越该留在 nano-agent 这侧。**

**第二取舍:多模型 panel vs 单 agent** —— 为什么:异构交叉验证 + 规避 role-switching;代价:协调开销 + 文档膨胀;重评:模型趋同时 panel 边际收益降。

---

## 8. Verdict —— 它是 SDD 吗?

**不是 SDD,是 SDD 的同辈。** 给它一个名字:**Conductor-Driven, Code-as-Truth Multi-Agent Development**(指挥驱动 · 代码为真源 · 多 agent 开发)。它 = SDD 的结构纪律 −(spec-primacy 赌注)+(多 agent 协调层)+(对账防腐层)+(tool-agnostic prompt 闭环)。

| 评估维度 | SDD | nano-agent 方法论 | 一句话 |
|----------|-----|-------------------|--------|
| 反 vibe-coding 的结构纪律 | 5 | 5 | 同源 |
| 单人单 agent 工效 | **5** | 3 | SDD 工具化更顺手 |
| 重生成/迁移能力 | **5** | 2.5 | SDD 的 spec-as-truth 天生强(我们 §6.1 补) |
| 多 stateless 异构模型适配 | 2 | **5** | nano panel 无对标 |
| 跨会话记忆 / 防 compaction | 2.5 | **5** | nano 文档=外部记忆 |
| 防"文档剧场" / 代码诚实 | 3 | **4.5** | nano 对账纪律更硬 |
| 跨项目/跨范式可移植 | 3(工具锁定) | **4.5** | nano 实证迁 smind |
| 收口/审计/防腐治理 | 2.5 | **4.5** | SDD 多止于 implement |
| 上手成本 / onboarding | **4** | 2.5 | SDD 工具+社区成熟 |
| **综合(就各自régime而言)** | **4** | **4.5** | 各自为王;nano 在"多 stateless agent + 诚实 + 巨型产品"régime更优 |

> 给 owner 的一句话裁定:**你不是在做 SDD,你是在做 SDD 的一个为"多无状态异构模型 + 一个指挥 + 代码诚实"量身定制的变体。** 它在 SDD 的弱点(role-switching、单 agent、止于 implement、迁移撞 context)上反而更强;它该向 SDD 借的,是**迁移用的重生成 spec(补保真缺口)、EARS 验收、slash 工效、单一 constitution**——但**别学 SDD 的 spec-primacy 与工具锁定**。

---

## 9. 一句话结论

SDD 与你的方法论是同一场"反 vibe-coding"运动里分叉的两支:**SDD 把宝押在"spec 为真、代码可重生成、单强 agent",你把宝押在"代码为真、文档为外部记忆与协调、多 stateless 模型 + 一个指挥、持续对账防腐"。** 你的直觉准确——同源不同宗,而分宗点就是**真源的认识论**。两者都对,只是对的是**不同的约束régime**;并且随着模型变强变 stateful,两支会向 SDD 一侧收敛。**该向 SDD 借四样**(迁移重生成 spec / EARS / slash 工效 / constitution),其中"迁移重生成 spec"正好补上你 smind 迁移最薄的那道"行为保真"缝。

---

## 附录 A · 来源（Sources）

- 定义/综述：[Thoughtworks · Spec-driven development](https://thoughtworks.medium.com/spec-driven-development-d85995a81387)、[Martin Fowler · Understanding SDD: Kiro, spec-kit, Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html)、[IBM · What is SDD](https://www.ibm.com/think/topics/spec-driven-development)、[arXiv · SDD: From Code to Contract](https://arxiv.org/html/2602.00180v1)
- GitHub Spec Kit：[github/spec-kit](https://github.com/github/spec-kit)、[GitHub Blog · SDD toolkit](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)、[Microsoft Dev Blog](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)
- AWS Kiro / EARS：[kiro.dev](https://kiro.dev/)、[Kiro EARS 写作指南](https://kiro.directory/tips/spec-writing)
- Tessl / spec-as-source-of-truth：[Augment · Spec as Source of Truth](https://www.augmentcode.com/guides/spec-as-source-of-truth-rebuildable-codebase)
- 批评/局限：[Augment · What is SDD](https://www.augmentcode.com/guides/what-is-spec-driven-development)、[SoftwareSeni · SDD 2025](https://www.softwareseni.com/spec-driven-development-in-2025-the-complete-guide-to-using-ai-to-write-production-code/)

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：SDD（Spec Kit/Kiro/Tessl）对比 + 7 条差异（真源反转为核）+ 各自régime优势 + 4 条借鉴（迁移重生成 spec 补保真缺口）+ Verdict（同辈非 SDD，命名 conductor-driven code-as-truth）|
