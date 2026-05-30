# Nano-Agent Eval 模板 · gap-study

> **模板类型**：`eval / gap-study`
> **一句话用途**：以参考实现为标尺，研究 **nano-agent 某子系统/接口面** 缺什么、接下来该建什么，产出编码缺口台账 + 优先级建造建议，喂给 charter/design。
> **何时用**：`*-gap-study` / `*-analysis`（我方某模块）/ `<reference>-compared` / `mc-investigation-<subsystem>` 这类"对照参考找我方缺口"的调查。
> **何时不用**：① **穷尽分析一个外部 CLI 本身**（对象=参考）→ 用 `investigation.md`；② 提案整个阶段范围（前瞻、冻结零）→ 用 `eval-general-purpose.md`；③ go/no-go 探针 → 用 `eval-feasibility-study.md`。
>
> **三方划界（务必看清，本 flavor 最易混）**：
> - `investigation.md`：研究**对象 = 外部 CLI**，产出"外部工具能力清单/评分"。
> - **`eval-gap-study.md`（本模板）**：研究**对象 = nano-agent**，参考只是**标尺/借鉴源**，产出"我方缺口台账 + 建造建议"。
> - `eval-general-purpose.md`：**提案**阶段范围，冻结零决策。
>
> **使用纪律（共有脊 · 所有 eval 模板一致）**：
> 1. 本文是 **eval**，**冻结零决策**——产出缺口与建造建议供 charter/design 消费，不冻结。
> 2. 每条缺口必须**编码 + 带 file:line 证据**；建造建议必须带优先级与工作量/工作块。
> 3. 头部 / 性质声明 / TL;DR / 输入锚定 / 修订历史为**共有脊**，跨 eval 模板一致。

---

# `{GAP_STUDY_TITLE}`

> **对象（我方）**：`{NANO_AGENT_SUBSYSTEM_OR_SURFACE}`
> **日期**：`{DATE}`
> **作者**：`{AUTHOR}`（panel：`{PANEL_OR_NONE}`）
> **文档性质**：`eval / gap-study`（对象是 nano-agent，参考为标尺；冻结零决策）
> **调查类型 / body 轴**：`subsystem | API-category | 调查问题 | 单参考标尺`（见 §2 选其一）
> **范围围栏（scope-fence）**：`{ONLY_THESE_SOURCES_NO_DIVERGENCE}`
> **对照参考**：`{REFERENCE_YARDSTICKS：claude-code / codex / gemini-cli / cf-agents / smind-* / 内部 precedent}`
> **文档状态**：`draft | reviewed | superseded`
> **上游权威输入**：
> - `{INPUT_1}`
> **下游消费者**：`{CHARTER_OR_DESIGN_THIS_FEEDS}`

---

## 0. Verdict（结论先行）

- **一句话缺口判断**：`{ONE_LINE_GAP_VERDICT}`
- **最关键的 N 个断点**：`{TOP_BLOCKERS}`
- **总体方向建议**：`{推进 / 渐进重构 / 重写 / 暂缓}`

---

## 1. 方法与可采信证据基线

> 读了哪些代码/文档；什么算可采信证据；范围围栏（不发散到哪）。

- **证据来源**：`{CODE_PATHS / API_DOCS / BUG_HISTORY / REFERENCE_REPOS}`
- **可采信判据**：`{WHAT_COUNTS_AS_EVIDENCE}`
- **范围围栏**：`{SCOPE_FENCE}`

---

## 2. 主体分析（轴自选）

> **body 轴由作者选定并在头部声明**：按子系统 / 按 API 类别 / 按调查问题 / 按单参考标尺走查。下面给四种轴的可选骨架，**选一种填，删其余**。

### 选项 A — 按子系统 / API 类别

#### 2.A `{SUBSYSTEM_OR_CATEGORY}`
- **我方现状**：`{CURRENT_STATE}`（锚点 `{FILE_LINE}`）
- **参考做法**：`{REFERENCE_APPROACH}`
- **差距**：`{GAP}`

### 选项 B — 按调查问题（Q1..Qn）

#### 2.B Q`{N}`：`{QUESTION}`
- **直接回答**：`{ANSWER}`
- **证据**：`{FILE_LINE_OR_REFERENCE}`

### 选项 C — 单参考标尺走查

#### 2.C 以 `{SINGLE_REFERENCE}` 为尺，模拟一次 `{TURN/FLOW}`
- **覆盖矩阵**：

| 能力点 | 我方 | `{REFERENCE}` | 判定 |
|--------|------|---------------|------|
| `{CAPABILITY}` | `✅/⚠️/❌` | `✅` | `{VERDICT}` |

- **走查断点**：`{BREAKPOINT_TRACE}`

---

## 3. 缺口 / 断点台账（核心产出）

> 每条编码、带严重度、带 file:line 证据、带影响。这是喂给 charter 的"我方缺什么"清单。

| 编号 | 缺口 / 断点 | 严重度 | 证据（file:line） | 影响 |
|------|-------------|--------|-------------------|------|
| `B1` | `{GAP}` | `blocker / high / med / low` | `{FILE_LINE}` | `{IMPACT}` |
| `B2` | `{GAP}` | `blocker / high / med / low` | `{FILE_LINE}` | `{IMPACT}` |

---

## 4. [可选] 参考对比矩阵

> 与多个参考横向对比；仅在对比能改变建造选择时写。

| 维度 | 我方 | `{REF_1}` | `{REF_2}` | 我方倾向 |
|------|------|-----------|-----------|----------|
| `{DIMENSION}` | `{OURS}` | `{V1}` | `{V2}` | `{OUR_CHOICE}` |

---

## 5. 优先级建造建议

> 把缺口转成"接下来建什么"，带优先级、工作量/工作块、依赖。

| 优先级 | 建造项 | 对应缺口 | 工作量 / 工作块 | 依赖 |
|--------|--------|----------|------------------|------|
| `P0` | `{BUILD_ITEM}` | `B1` | `S/M/L 或 WB-x` | `{DEP}` |
| `P1` | `{BUILD_ITEM}` | `B2` | `S/M/L 或 WB-x` | `{DEP}` |

---

## 6. 收尾 Verdict 与 charter 交接

- **总体 verdict**：`{OVERALL_VERDICT}`
- **read-only 声明**：本文仅调查，未改任何代码。
- **charter 交接**：`{WHAT_THE_NEXT_CHARTER_SHOULD_PICK_UP}`
- **需进入 qna register 的问题**：`{QNA_ITEMS_OR_NONE}`

---

## 附录

### A. 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿 |
