# Nano-Agent 文档模板体系 —— 索引与统一约定（canonical）

> 本文件是 `docs/templates/` 的**单一权威入口**：① active 模板家族索引；② **统一约定（canonical conventions）**——状态词汇、轨道命名、符号图例、核心名词、交叉引用风格的唯一真源。任何模板与本表冲突时，**以本表为准**。
> 设计/裁定背景见 `docs/templates/re-design/`（5 份再设计分析）。
> 历史/停用模板已移入 `docs/templates/legacy/`（investigation / code-review-eval / code-megafile-header / composition-factory.ts / _TEMPLATE-spike-finding / issue-closure-fax9 / wrangler-worker.toml）。

---

## 1. 模板家族索引（active 22）

| 家族 | 模板 | 一句话角色 |
|------|------|------------|
| **eval（7）** | `eval-general-purpose` | 提案"做什么"（兜底）|
| | `eval-planning` | 三态规划（initial→proposed→final）→ 派生多 action-plan |
| | `eval-reference-anchor` | grounding 锚台账（ARCH/TR/file:line + 借鉴 verdict）|
| | `eval-gap-study` | 我方缺口台账（对照参考）|
| | `eval-state-analysis` | 交付快照 + 对账诚实 + 前瞻交接（周期铰链）|
| | `eval-feasibility-study` | go/no-go 探针（token 化结论）|
| | `eval-retrospective` | 失误复盘（时间线 + 根因 + 教训）|
| **charter（2）** | `charter` | 重轨纲领（scope/phase/exit/trigger）|
| | `charter-lite` | 轻 charter + 决策冻结 + design-necessity 闸 |
| **design（3）** | `design-neo` | 重轨默认：净新契约 + 跨功能一致性 + 深 tradeoff |
| | `design-sketch` | Track C 内单簇净新补丁 |
| | `design`（原全量版）| legacy 候选；新工作改用 `design-neo` |
| **decision（1）** | `qna` | **owner 决策唯一真源（register）** |
| **action-plan（1）** | `action-plan` | 执行序列（phase / 工作项 / 测试 / 收口）|
| **respond / 附加章节（4）** | `code-review-respond` | 实现者回应（append code-review §6）|
| | `respond-execution-log` | 执行日志回填（append action-plan §9）|
| | `respond-post-freeze` | 冻结后补强（append design/eval 续号）|
| | `respond-verification` | 代码碰撞核实矩阵（append 附录）|
| **review / closure / 专科（4）** | `code-review` | 评审制品 + verdict |
| | `closure` | 收口 + 价值/负债台账 + handoff |
| | `api-compliance` | API 合规审查 |
| | `bug-analysis-report` | bug 根因分析 |

---

## 2. 四轨工作流（详见 `re-design/workflow-tracks.md`）

| 轨 | 进 action-plan 前的文档组合 | 适配 |
|----|------------------------------|------|
| **A 单遍** | `eval-general-purpose` → action-plan | trivial、无契约 |
| **B charter-lite** | `eval`（+ 可选 `eval-reference-anchor`）→ `charter-lite` → action-plan | 小·低模糊·扩展既有·无净新 |
| **C combo ★** | `eval-planning`(三态) + `eval-reference-anchor` + `qna`（+ `design-sketch` 若一处净新）→ action-plan | sub-phase·≥2 AP·需 grounding |
| **D 重轨** | `eval-gap-study`/`eval-state-analysis` → `charter` + `design-neo`(×N) + `eval-reference-anchor` + `qna` → action-plan | foundation·净新多·争议架构 |
| **闭环** | action-plan→`respond-execution-log`；impl→`code-review`→`code-review-respond`；阶段末→`closure`→`eval-state-analysis`(下周期) |

**轨道/design 选择**：见 `re-design/workflow-tracks.md` §4 决策树 + §3.6 的 design-necessity 6 条。

---

## 3. 统一约定（CANONICAL —— 唯一真源）

### 3.1 文档状态词汇

- **核心四态（所有文档共用）**：`draft → reviewed → frozen → superseded`
  - `draft` 在写 · `reviewed` 已评审 · `frozen` 定稿锁定（决策/边界/规格/基线锁死，只能 supersede 不能改）· `superseded` 被新版取代
- **家族合法扩展**（仅以下情形可加）：
  - `action-plan`：+ `executing | executed`（执行态）
  - `charter`：用 `active charter | closed charter`（active=生效中，closed≈frozen）
  - `code-review` / `*-respond`：`reviewed | changes-requested | re-reviewed | closed`
- **eval 家族细分**：
  - 纯分析型（general-purpose / gap-study / state-analysis / feasibility / retrospective）：`draft | reviewed | superseded`（快照，不 freeze）
  - 基线/锚型（`eval-planning` 的 final 阶段 / `eval-reference-anchor`）：`draft | reviewed | frozen | superseded`（会冻结基线）
- **澄清**：`frozen`（文档定稿锁定）≠ eval 的"冻结零决策"（指 eval 不替 owner 拍板）。前者说**文档状态**，后者说 eval **不抢 owner 决策权**——两者不矛盾。

### 3.2 stage 轴（仅 `eval-planning`）

`stage: initial | proposed | final` —— 这是**成熟度轴，独立于 status**。不要把 stage 值塞进 status 字段。

### 3.3 轨道命名（canonical）

`Track A 单遍 / Track B charter-lite / Track C combo（= 三态规划 + reference-anchor + qna）/ Track D 重轨`。引用时统一用 `Track X 名称`。

### 3.4 符号图例（两套，语义不同，**勿混用**）

- **复用判定**（我方代码处置；用于 `design-neo` / `design-sketch` / `eval-planning` 的工作台账）：
  `✅ 复用` / `♻️ 重 substrate`（在既有 substrate 上重建）/ `🆕 净新`
- **借鉴 verdict**（外部参考裁定；**仅 `eval-reference-anchor`**）：
  `✅ 借` / `🔶 部分借` / `⛔ 反例（避开）` / `🆕 净新（无先例）`
- 注：两套都含 `✅` 与 `🆕`，但语境不同（前=我方代码，后=外部参考），**不可互换**。

### 3.5 裁定动词 rubric（`eval-planning §2` / `better-planning`，可按 lineage 覆盖）

- proposed 态（vs initial）：`KEEP / REFRAME / CLOSED / NEW`
- final 态（vs proposed）：`CONFIRM / CORRECT / REFINE / RESIZE / GAP`

### 3.6 design-necessity 6 条（canonical 治理闸 —— `charter-lite §1.4` 与 `workflow-tracks §4` 必须与本表逐字一致）

满足**任一** ⇒ 不能只靠 charter-lite/combo，需 design（`design-sketch` 单簇 / `design-neo` 多簇）：

1. 新增**对外 contract surface**（从零定义，非扩展既有）
2. 新增**架构接缝**（净新 decouple/aggregate；reference-anchor 无既有 ARCH 可锚）
3. **跨 worker 不变量 / 多功能必须拼成一个整体形态**
4. 验收是**多字段 / 非显然**的（一两句 QNA 答不清“做完长什么样”）
5. 涉及**安全信任边界**（威胁模型）—— 强制升级
6. **onboarding 关键**：需新贡献者读懂的叙述式契约

### 3.7 核心名词表（统一中英用法）

| 名词 | 含义 | 用法 |
|------|------|------|
| `净新`（net-new） | 从零定义的对外契约 / 架构接缝 | 中文优先用"净新" |
| `扩展既有`（additive） | 在已建 substrate 上加列/加端点 | 中文优先用"扩展既有" |
| `grounding` | 架构边界(§3) + 仓内 file:line 锚(§8) 的落地依据 | 保留英文，不译 |
| `substrate` | 仓库现实代码基底 | 保留英文，不译 |
| `缝 / seam` | 跨模块 / 契约的接缝 | 中英皆可，同义 |
| `收口目标` | 一句话可验证完工标准 | 统一"收口目标"（非"完工标准/done criterion"混用）|
| `验收格栅`（acceptance lattice） | `功能 F → 收口目标 → Test-ID` 三联 | design-neo §6 / eval-planning final |
| `frozen / 冻结` | owner 裁决后锁定 | 见 §3.1 |
| `qna register` | owner 决策唯一真源 | 见 §3.8 |

### 3.8 交叉引用与占位符约定

- **引用模板**：用文件名根（`eval-reference-anchor` / `design-neo` / `qna` / `action-plan`），不裸缩写。`charter-lite` 内若用 `AP` 须首次出现处定义 `AP = action-plan`。
- **`qna` 大小写**：文件/register 一律小写 `qna`（`qna.md` / `qna register`）；大写 `QNA` 仅指通用 Q&A 机制/内嵌块。**决策只活在 register**，design-sketch/eval-planning/charter-lite 的内嵌 QNA 必须指向 register，不另立真源。
- **占位符**：统一 `{UPPER_SNAKE}`，backtick 包裹（如 `` `{PHASE_NAME}` ``）。
- **eval 家族共有脊**：头部统一含"`使用纪律（共有脊 · 所有 eval 模板一致）`"块（结构一致；首条声明"本文是 eval，冻结零决策"，flavor 细节在 `模板类型` 字段）。

---

## 4. legacy/ 说明

`docs/templates/legacy/` 存放已被 active 集取代的历史模板，**不用于新工作**：
- `investigation.md` → 外部 CLI 深析已由 `eval-gap-study`（我方缺口）/ `eval-reference-anchor`（借鉴锚）覆盖
- `code-review-eval.md` → 审查质量评价已并入 `code-review` 流程
- `code-megafile-header.md` / `composition-factory.ts` / `wrangler-worker.toml` / `_TEMPLATE-spike-finding.md` / `issue-closure-fax9-and-beyond.md` → 专项/陈旧

---

## 附录 · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：active 22 模板索引 + 四轨速查 + canonical 统一约定（状态/stage/轨道/符号/裁定动词/design-necessity/名词/交叉引用）+ legacy 说明 |
