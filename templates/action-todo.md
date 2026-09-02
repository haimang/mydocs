<!--
═══════════════════════════════════════════════════════════════════════════════
 action-todo 模板使用说明（META）—— 产出落盘前删除本区块
═══════════════════════════════════════════════════════════════════════════════

定位：action-todo 是“把目标变成可执行、可验证、可交接事项”的轻量模板。
它可以承接 action-plan，也可以直接服务于一个小型任务；它不替代 design、qna、
action-plan 或 closure，也不自行产生执行授权。

必须 follow 的核心脊只有五件事：
1. 目标与边界：说清楚做什么、不做什么、谁/什么有权决定。
2. 依赖指引：用任意清晰形式表达 DAG/执行图；节点、依赖、入口、出口和失败处理不可隐藏。
3. 工作项：每项有稳定 ID、实际动作、落点、完成判据和验证映射，并且必须有 checkbox。
4. 执行回写：每完成一个工作 ID，必须回到本 todo 把 `[ ]` 改为 `[x]`，登记 `执行状态`、时间和证据；未跑、部分、阻塞和 deferred 保持未勾选并诚实标记。
5. 交接：随时能看出当前节点、下一动作、阻塞项和责任/承接方。

可选插件不是装饰，而是按触发条件启用的模块：
- 代码/行为修复 → RED-first / falsifier；
- 有路径、数量、跨边界或安全限制 → scope / no-sideload；
- 需要仓内或外部依据 → context / reference-anchor；
- 多层或多轮验证 → test ledger；
- 远端、部署、provider、D1、导出或付费面 → live / billing / root；
- 实际执行且有偏差 → execution log；
- 阶段结束或需要责任交接 → closure / handoff。

没有触发条件的插件应删除；一旦触发，对应插件的最低字段就变成该任务的必需项。
DAG 的画法、节点数量、是否分 phase、是否并行由 agent 根据任务选择；不得把示例任务的
BLOCK 名称、数量、路径上限或执行顺序机械复制到所有任务。若有 retry/loop，把边界和次数
显式写出，不要藏在一个“重试若干次”里。

产出前删除本 META 区块、未启用插件、未替换占位符和本文件末尾的自检注释。
═══════════════════════════════════════════════════════════════════════════════
-->

# `{TODO_ID}` Action Todo — `{TITLE}`

> 文档性质：`action-todo`（DAG-guided execution；不是新的设计或授权文件）
> 目标：`{GOAL}`
> In-scope：`{IN_SCOPE}`
> Out-of-scope：`{OUT_OF_SCOPE}`
> 上游依据：`{UPSTREAM_SOURCES_OR_NA}`
> 关联 action-plan / design / issue：`{RELATED_PLAN_OR_NA}`
> authority / owner：`{AUTHORITY_OR_OWNER}` · 授权边界：`{AUTHORIZATION_BOUNDARY}`
> 基线（如适用）：`{BASELINE_OR_NA}`
> 文档状态：`{DOCUMENT_STATE}` · 执行状态：`{EXECUTION_STATE}`

## 1. 核心脊（必须 follow）

> 本节和 §§2–5 是每份 action-todo 都必须具备的最小结构。可以改标题、换表格或改用图/列表，但不得删掉语义。

- **目标与边界**：本 todo 要交付 `{DELIVERABLE}`；明确 `{NON_GOAL_OR_CONSTRAINT}`。
- **权威与决策**：已确定的依据是 `{FROZEN_OR_AUTHORITATIVE_INPUTS}`；未确定的问题回到 `{DECISION_OWNER_OR_REGISTER}`，不在 todo 中偷偷裁决。
- **完成定义**：本任务只有在 `{COMPLETION_DEFINITION}` 成立时才可标记完成。
- **证据原则**：每个完成判据都要有 `{EVIDENCE_FORM}`；“写过计划、数量变绿、请求可达或状态看起来成功”不能单独充当完成证据。
- **执行回写**：每个 `Item ID` 都必须使用 `- [ ]` / `- [x]`；`[x]` 只表示该项完成，且同一项的执行状态、UTC 时间和证据已经登记。
- **交接原则**：不能完成的事项必须写明 `{BLOCKER_OR_DEFERRED_REASON}`、下一动作和责任/承接方。

## 2. 依赖关系 / DAG 指引（必须有；表达形式自由）

> agent 可选择 flowchart、dependency table、编号列表、泳道图或混合形式。这里不规定 block 数量，也不要求所有任务都拆成 phase。最小要求是：每个节点有 ID，依赖可见，入口/出口可判断，失败/阻塞/交接路径可追踪。

> 若任务只有一个节点，也要明确写出“无前置依赖 / 单节点任务”。如需并行、汇合、条件分支或 retry，写出触发条件、边界和汇合点；不要把隐含顺序留给读者猜。

### 2.1 依赖图（可替换为其他形式）

```text
{NODE_A} ──depends on──▶ {NODE_B} ──depends on──▶ {NODE_C}
   │                        │
   └──on failure──▶ {FAILURE_OR_HANDOFF_A}
                            └──on blocked──▶ {BLOCKED_NEXT_STEP}
```

### 2.2 节点台账（可与上图二选一；复杂任务建议保留）

| 节点 ID | 目的 / 动作 | depends on | entry condition | exit condition | failure / blocked / handoff |
|---------|-------------|------------|-----------------|----------------|------------------------------|
| `{NODE_A}` | `{NODE_A_ACTION}` | `{NODE_A_DEPENDENCY}` | `{NODE_A_ENTRY}` | `{NODE_A_EXIT}` | `{NODE_A_FAILURE_PATH}` |
| `{NODE_B}` | `{NODE_B_ACTION}` | `{NODE_B_DEPENDENCY}` | `{NODE_B_ENTRY}` | `{NODE_B_EXIT}` | `{NODE_B_FAILURE_PATH}` |
| `{NODE_C}` | `{NODE_C_ACTION}` | `{NODE_C_DEPENDENCY}` | `{NODE_C_ENTRY}` | `{NODE_C_EXIT}` | `{NODE_C_FAILURE_PATH}` |

**DAG / execution-graph notes：** `{ORDERING_OR_BRANCHING_NOTES}`

## 3. 工作项清单（必须有 checkbox）

> 一项只承载一个可交付结果。工作项可以对应一个节点、一个 phase 或一个小步骤；不要求所有任务采用同一种粒度。**表达形式可以灵活，但每个 Item ID 必须保留 `- [ ]` / `- [x]` checkbox。**

### 3.1 工作项与执行登记

- [ ] `{ITEM_01}` — `{ACTION_01}`
  - **落点 / 对象**：`{TARGET_01}`
  - **完成判据**：`{DONE_01}`
  - **验证映射**：`{CHECK_01}` · **依赖**：`{DEPENDENCY_01}`
  - **执行状态**：`not-started` · **执行时间**：`-` · **证据 / 备注**：`{EXECUTION_RECORD_01}`
- [ ] `{ITEM_02}` — `{ACTION_02}`
  - **落点 / 对象**：`{TARGET_02}`
  - **完成判据**：`{DONE_02}`
  - **验证映射**：`{CHECK_02}` · **依赖**：`{DEPENDENCY_02}`
  - **执行状态**：`not-started` · **执行时间**：`-` · **证据 / 备注**：`{EXECUTION_RECORD_02}`
- [ ] `{ITEM_03}` — `{ACTION_03}`
  - **落点 / 对象**：`{TARGET_03}`
  - **完成判据**：`{DONE_03}`
  - **验证映射**：`{CHECK_03}` · **依赖**：`{DEPENDENCY_03}`
  - **执行状态**：`not-started` · **执行时间**：`-` · **证据 / 备注**：`{EXECUTION_RECORD_03}`

> **完成一个工作 ID 后必须回写本节**：将 `- [ ]` 改为 `- [x]`，把执行状态改为 `complete`，补齐 UTC 执行时间和证据引用。`in-progress | blocked | partial | deferred` 必须保持 `- [ ]`，并写明 reason、下一动作和责任/承接方。可按需增加工作项；Item-ID 是 review、执行记录、closure 和 successor handoff 的共同索引。

## 4. 验收与证据（必须有）

> 验证方式由任务决定：可以是 unit/integration/e2e test、静态检查、源码审阅、查询、receipt、owner decision 或组合。每个 `pass` 都要能回答“验证了什么、怎样复现、实际结果是什么”。

| Check ID | 验证什么 | 方法 / 命令 / 产物 | 预期 | 实际结果 | 证据引用 | 状态 |
|----------|----------|--------------------|------|----------|----------|------|
| `{CHECK_01}` | `{WHAT_CHECK_01}` | `{METHOD_01}` | `{EXPECTED_01}` | `{ACTUAL_01}` | `{EVIDENCE_01}` | `{PASS_PARTIAL_PENDING_01}` |
| `{CHECK_02}` | `{WHAT_CHECK_02}` | `{METHOD_02}` | `{EXPECTED_02}` | `{ACTUAL_02}` | `{EVIDENCE_02}` | `{PASS_PARTIAL_PENDING_02}` |
| `{CHECK_03}` | `{WHAT_CHECK_03}` | `{METHOD_03}` | `{EXPECTED_03}` | `{ACTUAL_03}` | `{EVIDENCE_03}` | `{PASS_PARTIAL_PENDING_03}` |

- **状态词**：`pass | partial | pending | blocked | not-applicable`；后四类都要写 reason，不能用空白代替。
- **可复核性**：需要代码/运行证明时，记录适用的版本或 commit、测试/命令/查询/receipt 和时间；无需某类证据时写 `N/A + reason`。
- **真实成功**：业务输出、授权、provider、部署或 live 能力不能仅凭 HTTP 状态、terminal metadata、计数、catalog、health 或空结果抬绿；按 `{TASK_SPECIFIC_SUCCESS_POLARITY}` 判定。

## 5. 当前状态与交接（必须有）

- **当前节点 / 已完成**：`{CURRENT_NODE_OR_NODES}` / `{COMPLETED_ITEMS}`
- **下一动作**：`{NEXT_ACTION}`
- **当前阻塞**：`{CURRENT_BLOCKERS_OR_NONE}`
- **待 owner / 外部决定**：`{OWNER_PENDING_OR_NONE}`
- **最终交接目标**：`{SUCCESSOR_OR_HANDOFF_TARGET}`

| Item / node | 当前状态 | 原因或证据 | 下一动作 | 责任 / 承接方 | 重开条件 |
|-------------|----------|------------|----------|---------------|----------|
| `{HANDOFF_ITEM_01}` | `{HANDOFF_STATUS_01}` | `{HANDOFF_EVIDENCE_01}` | `{HANDOFF_NEXT_01}` | `{HANDOFF_OWNER_01}` | `{REOPEN_01}` |
| `{HANDOFF_ITEM_02}` | `{HANDOFF_STATUS_02}` | `{HANDOFF_EVIDENCE_02}` | `{HANDOFF_NEXT_02}` | `{HANDOFF_OWNER_02}` | `{REOPEN_02}` |

## 6. 可选插件菜单（按触发条件启用）

> 先判断是否触发，再插入对应模块。没有触发条件的模块应删除；触发后，表中的“最低要求”就是该任务的必需内容。插件可以重命名、合并或拆分，但不能以删名代替履行。

| 插件 ID | 何时启用 | 最低要求 |
|---------|----------|----------|
| `P-CTX` Context / rebaseline | 任务跨多轮、代码可能漂移、接续旧工作或需 current HEAD | 读取依据、基线、差异、影响及继续条件 |
| `P-RED` RED-first / falsifier | 修 bug、改行为、归因 first-red 或声称修复 | 原始 RED、falsifier、修复后验证、残余 RED |
| `P-SCOPE` Scope / no-sideload | 有路径/数量 cap、跨边界、迁移、权限或安全约束 | allowlist、禁止面、scope audit、越界处理 |
| `P-REF` Reference-anchor | 依赖 file:line、外部参考、设计/真相锚点 | 锚点、用途、复用/新建判定和反例 |
| `P-TEST` Test ledger | 多个测试层、复杂验收或需要复用/fork 既有用例 | Test-ID、层级、来源、PASS 证据和缺口 |
| `P-LIVE` Live / billing / root | 远端、部署、provider、D1/R2、导出、alarm 或其他付费/外部操作 | owner grant、预算、身份、fresh root、停止条件、terminal/receipt |
| `P-EXEC` Execution log | 已实际执行、存在多步/多轮或计划与实际有偏差 | 在本节 checkbox/状态回写之外，追加 append-only 日志、偏差、first-red、实际证据 |
| `P-CLOSE` Closure / handoff | 阶段收口、责任转移、需要 closure 或 successor | final state、known gaps、deferred、责任方、重开条件 |

### 6.1 已启用插件

> 将启用的插件插入下方；未启用时删除本节或保留 `none`。每个插件只写本任务特有内容，通用规则引用本菜单即可。

#### `{PLUGIN_ID}` — `{PLUGIN_NAME}`

- **触发理由**：`{PLUGIN_TRIGGER}`
- **本任务最低要求 / 允许写面**：`{PLUGIN_MINIMUM_AND_SCOPE}`
- **实际记录**：`{PLUGIN_RECORD}`
- **证据 / 状态 / handoff**：`{PLUGIN_EVIDENCE_AND_HANDOFF}`

## 7. Todo 自检（提交或交接前）

- [ ] 核心脊 §§1–5 齐全；目标、边界、authority、完成定义和当前下一步没有歧义。
- [ ] DAG/执行图的依赖、入口、出口、失败/阻塞/交接路径可读；没有复制无关示例的固定 block 数量或顺序。
- [ ] 每个 Item ID 都是 `- [ ]` / `- [x]` checkbox；完成项同时登记 `执行状态=complete`、UTC 时间和证据，未完成项保持未勾选并有 reason。
- [ ] 每个 Item 都有完成判据和 Check-ID；每个 `pass` 都有实际证据，其他状态都有 reason。
- [ ] 所有适用插件已启用；不适用插件已删除；scope、RED、live/billing 和 owner 边界没有被省略。
- [ ] 未把计划、授权、可达性、计数、health、terminal 或空结果写成实际完成；未完成项已明确 successor / reopen condition。
- [ ] 已删除本文件首尾 META/自检注释、未替换占位符和无关章节。

<!--
实例化检查：
□ 本文件可以脱离对话被另一位 agent 继续执行。
□ 如需 detailed execution log，已挂接 `.adocs/templates/code-execution-log.md`；如需 closure，已挂接 `.adocs/templates/closure.md`。
□ 如涉及本仓远端操作，已按 `AGENTS.md`、`TOPOLOGY.md`、`LIVE_ROOT.md`、`BILLING_TRUTH.md` 执行对应插件的闸门。
-->
