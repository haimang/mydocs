# 可模板化的"附加章节"调查与再设计建议

> 文档对象：`docs/eval/**`、`docs/design/**`、`docs/action-plan/**` 正式文件**末尾的附加章节**（appended sections）
> 作者：Claude Opus 4.8（heading 模式全量扫描 776 文件 + 2 路并行子代理深读真实附加章节）
> 日期：2026-05-30
> 文档性质：`re-design 建议 / 向 owner 的汇报`（不冻结决策）
> 文档状态：`draft — 待 owner 审阅`
> 调查输入：
> - 现有附加章节模板：`docs/templates/code-review-respond.md`（archetype）
> - 现有整文件模板的尾部章节：`design.md`(附录 A/B)、`action-plan.md`(§9)、`qna.md`、`charter.md`(§15)、`closure.md`(修订历史)
> - 关联：`docs/templates/re-design/eval-docs-re-design.md`（§4.4 已建议给 qna.md 加 freeze 尾块）

---

## 0. 一句话结论（TL;DR）

`code-review-respond.md` 不是孤例——它是一整个**"附加章节模板"品类**的第一个成员。全量扫描后，正式文件末尾**反复出现 6 类形状稳定、可直接模板化的附加章节**，其中**两类的体量极大**（执行日志回填覆盖 **46% 的 action-plan**、讨论/分歧记录覆盖 **41% 的 design**），却只有薄占位或根本没有模板。

对 owner 的核心建议：**确立"附加章节模板"为继"整文件模板""可内嵌组件"之后的第三个模板品类**，并按下表落地：

| Tier | 动作 | 附加章节 | 宿主 | 体量 |
|------|------|----------|------|------|
| 已有 | 保留 | `code-review-respond`（实现者回应） | code-review | 21 |
| **提拔** | 薄→厚，独立成模板 | **`action-plan-respond`（执行日志回填）** ★ | action-plan | **94/204** |
| **新建** | 净新模板 | **`post-freeze-addendum`（冻结后补强）** ★ | design / 设计型 eval | 28+ |
| 新建 | 净新模板 | `verification-matrix`（代码碰撞核实） | design / eval | 10 |
| 充实 | 给 `qna.md` 加 freeze 尾块 | `业主裁决·一致性审查·冻结声明` | qna | 11 |
| 充实 | 充实 `design.md` 附录 A | `讨论/分歧记录` | design | **72/175** |
| 标准化 | 抽成共享 snippet（非重型模板） | `修订历史` | 全部 | 168 |

---

## 1. 调查方法（可复现）

"附加章节"= 正式文件**主交付物之后**追加的、代表**更晚 / 元活动**的章节（往往换了作者、换了时间）。检测两层：

1. **heading 模式全量统计**：抽取 `docs/eval+design+action-plan/**` 全部 30,379 行标题，按"晚到 / 元活动"关键词分桶计数（回填/执行日志、补强/增补/更新章节、裁决/冻结声明、回应、碰撞核实、分歧记录、修订历史、维护约定……），并按 **doc-type 分布**看每类集中在哪种宿主。
2. **date-stamped heading 信号**：标题里带 `（2026-..）` 的是"事后追加"的强信号——**172 个文件**命中。
3. **深读真实实例**：2 路子代理读了执行日志最丰的 action-plan、冻结后补强的设计型 eval、qna 冻结尾块、碰撞核实矩阵、分歧记录，抽取**真实**子结构（子标题/表列/状态枚举/纪律），使骨架建议有据。

> 扫描脚本见附录 A，可接入 `docs:check`。

## 2. 什么算"可模板化的附加章节"——从 code-review-respond 抽 6 条判据

读透 `code-review-respond.md`（`## 6 实现者回应`，6.1–6.7）后，它之所以能成模板，靠 6 个特征。一个附加章节满足越多，越值得模板化：

1. **挂宿主**：附在某种宿主文档的**固定位置**（review→§6、action-plan→§9、qna→§8、design→附录 A）。
2. **时间/作者位移**：写在主体**之后**，常**换作者**（respond：实现者≠审查者；裁决：owner；执行日志：执行者）。
3. **append-only 纪律**：不改写宿主主体，只往下追加（§6 规则第 1 条）。
4. **回链宿主 item-ID**：逐条对应 `R1/R2`、台账 ID、`Q1/Q2`、finding-ID，不许模糊"修了一些"。
5. **稳定子结构**：固定子标题 + 表 + 状态枚举（fixed/deferred/rejected…）。
6. **多轮机制**：6B/6C、dated `§N`、版本行。

## 3. 扫描结果：6 类复发附加章节（+1 通用 +1 小类）

| # | 附加章节 | 主宿主 | 体量(文件数 e/d/a) | 作者 / 时机 | 现状 |
|---|----------|--------|--------------------|-------------|------|
| 0 | **实现者回应** | code-review | e:21 | 实现者，修复后 | ✅ `code-review-respond.md` |
| 1 | **执行日志回填** | action-plan | **a:94** e:6 | 执行者，执行后 | 🔶 `action-plan.md §9` 薄占位 |
| 2 | **冻结后补强**（补强/更新章节/价值重审） | design / 设计型 eval | e:28 d:6 a:9 | 原作者，冻结后·owner 触发 | ❌ 无 |
| 3 | **业主裁决·一致性审查·冻结声明** | qna | e:11 d:1 | owner+作者，QnA 终点 | ❌ 无（qna.md 缺） |
| 4 | **代码碰撞核实矩阵** | design / eval | e:10 d:1 | 作者(扇出 sub-agent)，冻结前自检 | ❌ 无 |
| 5 | **讨论/分歧记录** | design | **d:72** e:5 | 作者，跨版本累积 | 🔶 `design.md 附录 A（可选）` 薄 |
| 通用 | **修订历史/版本历史** | 全部 | d:117 e:38 a:13 | 作者，每次改动 | 🔶 多处有、未统一 |
| 小类 | **维护约定** | charter / 规划 eval | e:12 | 作者 | 🔶 `charter.md §15` |

**读出的两条事实**：
- **执行日志回填（46% 的 action-plan）与讨论/分歧记录（41% 的 design）是两座金矿**——体量巨大、形状稳定，却只有薄占位。模板化它们的 ROI 最高。
- **冻结后补强（28+ 文件）完全没有模板**，却有最清晰的纪律（不重开冻结、dated、显式 supersede）——最强的净新候选。

## 4. 逐类剖析（基于真实实例，含纪律与真实骨架）

### 4.0 实现者回应（Type 0，已模板化，作对照基准）
- 6.1 本轮回应 / 6.2 逐项回应表（R-ID × fixed|deferred|rejected）/ 6.3 Blocker 汇总 / 6.4 变更文件 / 6.5 验证结果 / 6.6 未解决承接 / 6.7 ready-for-rereview gate。纪律：不改写 §0–§5；多轮 append `6B/6C`。**它是 6 条判据全中的满分样板。**

### 4.1 执行日志回填（Type 1）★ 体量第一
- **真实形态**（PEX5 最丰：§12.1 时序执行日志表 + §12.2 union 状态表 + §12.3 决策日志 + §12.4 pre-existing-fail 甩锅 + §12.5 文件清单 + §12.6 snapshot + §12.7 verdict）。MCX3/MCX4 是"5 bullet + 逐工作项状态表(`工作项|状态|PR|实际落点|备注`)"。
- **状态枚举**：`✅ / ⚠️(env-blocked No-Go) / ❌(OOS handoff)`；doc lifecycle `draft→executing→executed`；测试 `success/degraded/superseded-by`（degraded 必带机器 `reason`）。
- **纪律**：仅 `executed` 状态用；**计划 vs 实际偏差必须逐条**；回链台账 ID；dated；**pre-existing 失败要带 git 证据甩锅**，不许 silent overclaim；residual 交后继 charter，**不回填本阶段**。
- **作者/时机**：执行者本人、执行后、同会话。
- **判据命中**：1✅2✅(执行者)3✅4✅5✅6✅ → **满分，应独立成 `action-plan-respond.md`**（把 `action-plan.md §9` 提拔，关系完全对标 code-review ↔ code-review-respond）。

### 4.2 冻结后补强（Type 2）★ 最强净新
- **真实形态**：顶标题内嵌日期+触发（`# 13. 补强计划（post-freeze addendum，2026-05-22）`/`# 更新章节（2026-05-30）：…`/`# §11 价值台账重审（owner 驳回后）`），首块是 `性质/触发/方法/先认错` 引用块，然后**对照当前代码重新基线化的缺口表**，然后**新 ID 前缀的工作项**（MI-S2 用 `R-*` 区别于 expansion 的 `P*`），最后自检矩阵 + 诚实边界。
- **状态枚举**：交付/缩水 `✅已交付 / 🟩剩余 / 🟥缩水 / ⬜OUT`；冻结友好判据 `C1..C5`；动作分层 `P0 必做/P0.5 选做/押后禁做`；开放项 `~~item~~ → 裁决`。
- **纪律（最清晰）**：**不重开任何冻结裁决**；冻结**决策**不动、冻结**措辞**可校准；**显式 supersede 须点名 + 回上游 QnA 重开**，不别处改口；**对照当前代码而非旧水位**重新基线；新 file:line 须本轮 verify。
- **作者/时机**：**原作者**、冻结后、**owner 触发**。多轮 = dated `§N` 章 + 版本行（冻结行不动）。
- **判据**：1✅(挂 design/eval)2✅3✅(不重开冻结=最强 append-only)4✅5✅6✅ → **新建 `post-freeze-addendum.md`，跨宿主（design / 设计型 eval / 偶尔 action-plan）**。

### 4.3 业主裁决·一致性审查·冻结声明（Type 3）
- **真实形态**（MCX3-MCX4-qna §8）：8.1 裁决摘要表(`Q|主题|裁决结论|来源(业主指定/联合建议)`) → 8.2 业主 vs 联合建议差异 → 8.3 下游 scope 影响(一致性审查) → 8.4 跨文档一致性核对(逐份"无冲突") → 8.5 冻结声明(blockquote+日期+版本) → §9 修订历史。
- **枚举**：来源 `业主指定/采 Opus×GPT 联合/业主直接裁决`；freeze `🔒 FROZEN / v1.0(FROZEN)`；override `覆盖 GPT 保守默认`；gate 绑定 `G-X-1↔Q2`。
- **纪律**：业主只填 `业主回答`；冻结后下游**只看 `Q 编号 + 业主回答`**；补题从末号起、ID 稳定；推翻须本文追加修订；**一致性审查(8.3/8.4)强制**。
- **判据**：1✅(挂 qna)2✅(owner 填)3✅4✅(Q-ID)5✅6△ → **给 `qna.md` 加 freeze 尾块**（与 eval-docs-re-design §4.4 的建议合流、并细化）。

### 4.4 代码碰撞核实矩阵（Type 4）
- **真实形态**：`## 附录 C. 代码碰撞核实矩阵（date · N 路并行 sub-agent · 仅读真实代码）` + 表(`项(host-ID)|核实状态|file:line 证据|对台账的影响`) + `C.1 核实结论`。reference-anchor 变体加 `核验记录(✅HEAD 实测 / ⏳context 待 re-pin)` + `技术路线公理表(TR-1..10)` + `被剔除/重映射清单`。
- **枚举**：`ACTIVE(债真在)/STALE(已实现或超越)/PARTIAL`；机制 `✅适配/🔶须重映射/⛔无效` + `DROP/REMAP`；**置信分层在这里**（HEAD 实测高 / context ±数行待 re-pin / web 高低）。
- **纪律**：**只读真实代码、不转抄 closure**；每行必带 file:line；**修正项必须显式记录**；作者自审（非 owner）；net-effect 即使不变也要声明。
- **判据**：1✅2△(作者晚些自检)3✅4✅(finding-ID)5✅6△ → **新建 `verification-matrix.md`**（冻结前对抗性自检）。

### 4.5 讨论/分歧记录（Type 5）★ 体量第二
- **真实形态**（design.md 附录 A 的充实版）：`### A. 讨论记录摘要` 下逐条 `- **分歧 N**：<问题>` + `A 方观点(来源)` / `B 方观点(来源)` / `最终共识(或最终裁决)`；配 `### B. 版本历史` 表。**是 bullet 不是 table**（与 3/4 的结构签名差异）。
- **枚举**：`A 方/B 方`、`最终共识/最终裁决`、胜方 token(`B 方`/中间方案 `scope-narrow`/`NO-GO`)；常带 `QNA-ID frozen` 交叉引用。
- **纪律**：**败方观点保留在案**（"GPT『先单后双』保留记录"）；每方**标来源**；最终共识**常用 file:line 直接 trace 落地**（借了 Type 4 的取证）；标 `（可选）`，只在真有分歧时填。
- **判据**：1✅2△3△(累积)4△(松，靠 prose/Q-ID)5🔶(bullet)6✅(版本行) → **充实 `design.md 附录 A`**（体量 41% 值得从"可选薄占位"升级为有纪律的标准块），暂不独立成文件。

### 4.6 修订历史（通用）& 维护约定（小类）
- 修订历史：168 文件、4 列表(`版本|日期|作者|主要变更`)，**琐碎但无处不在且列名不统一** → **抽成单一 canonical snippet**，所有模板引用，不做重型模板。
- 维护约定：12 文件 + charter §15，小而独特 → 维持现状/折进各模板尾部。

## 5. 推荐：确立"附加章节模板"为第三品类

我们的模板体系现在有三层，应显式承认：

1. **整文件模板**（design / action-plan / qna / charter / closure / investigation / eval-* / design-sketch …）
2. **附加章节模板**（code-review-respond + 本文推荐的新成员）← **本次确立**
3. **可内嵌组件**（qna 的逐 Q 块、修订历史 snippet——可被多种文档引用）

### 5.1 三档推荐光谱

| 档 | 模板集 | 优点 | 缺点 |
|----|--------|------|------|
| 最小 | 只提拔 `action-plan-respond`（体量第一） | 改动最小 | 28+ 的冻结后补强仍无家 |
| **推荐 ★** | `action-plan-respond` + `post-freeze-addendum` + `verification-matrix` 三个新模板 + 充实 `qna.md`(freeze 尾块) & `design.md`(附录 A) + 抽 `_revision-history` snippet | 覆盖全部高频/高纪律附加章节，长尾留给现有 | 多 3 文件 + 2 处充实 |
| 最大 | 推荐 + 把"维护约定""讨论记录"也独立成文件 | 全有家 | 低频模板增殖 |

**我推荐"推荐档"**：新建 **3** 个独立附加章节模板（`action-plan-respond` / `post-freeze-addendum` / `verification-matrix`）+ 充实 **2** 个既有整文件模板的尾段（qna freeze、design 分歧）+ 标准化 **1** 个共享 snippet（修订历史）。

### 5.2 命名与治理约定（所有附加章节模板共享）

- **命名**：回应型用 `<host>-respond.md`（对标 code-review-respond）；补强型用 `<concept>-addendum.md`；其余按功能命名。
- **强制 banner**（修复 code-review-respond 当前缺失的一点）：每个附加章节模板**开头必须声明** ① 宿主文档类型、② 挂载位置（§N / 附录 X）、③ **append-only 规则**、④ 作者与时机、⑤ 回链宿主 item-ID 的方式、⑥ 多轮处理方式。code-review-respond 现在只有规则没有"我是附加章节、挂在 code-review 之后"的显式声明，建议补。

## 6. 推荐模板的骨架草案（深读所得，可直接落地）

> 仅列脊；细节待 owner 拍板数量后填。

**`action-plan-respond.md`（= 提拔的 §9）**
```
## 9. 执行日志回填（仅 executed）
> 状态：executed（{DATE}，{EXECUTOR} {模式}）。代码改动统计：{…}
- 实际执行摘要 / Phase 偏差(逐条带分类) / 阻塞与处理 / 测试发现(含全绿计数) / 后续 handoff
### 9.x 逐工作项状态  | 工作项 | 状态(✅/⚠️/❌) | PR | 实际落点(file:line) | 备注 |
### 9.x 关键指标演进(可选)  | 指标 | prev | this | Δ |
### 9.x 时序执行日志(可选,多轮)  | 时点(T0..) | 步骤 | 决策/产出 |
### 9.x pre-existing 失败甩锅(可选)  ← git 证据证明非本轮引入
### 9.x 文档状态  draft→executing→executed；residual→后继 charter(不回填本阶段)
```

**`post-freeze-addendum.md`（新建，跨宿主）**
```
## {N}. {补强|更新章节|价值重审}（post-freeze addendum，{DATE} — {主题}）
> 性质：§0–§{frozen}(frozen {ver}) 的事后补强；**不重开任何冻结裁决**，只追加。
> 触发：{owner 裁决/驳回/提问}；方法：新 file:line 均本轮 verify；（可选）先认错。
### {N}.0 判据/约束重述(校准非改写)
### {N}.1 重新基线化缺口(对照当前代码,非旧态)  | 旧标缺口 | 当前真实状态({DATE},file:line) | 状态(✅/🟩/🟥/⬜) | 处理 |
### {N}.2 补强工作列表(新 ID 前缀 R-*)  | R-* | 工作项 | 宿主锚点 | @layer | 净新增 | 价值 | 风险 |
### {N}.x 收口/自检矩阵  | 项 | C1 | C2 | … |
### {N}.x 诚实边界 / supersede 声明(点名冻结 §x；推翻须回 {QnA} 重开)
> 多轮：文末版本表 append 一行，冻结行不动。
```

**`verification-matrix.md`（新建）**
```
## 附录 C. 代码碰撞核实矩阵（{DATE} · N 路并行 sub-agent · 仅读真实代码）
> 方法：仅读 workers/**/src · clients/web/src · migrations · test，不读 docs/.tmp。
> 状态：ACTIVE=债真在 / STALE=已实现或超越 / PARTIAL。
| 项(host-ID) | 核实状态 | file:line 证据 | 对台账的影响(含**修正**) |
### C.1 核实结论：N 项碰撞；K 处修正；净影响 {scope 是否改变}
[substrate 变体追加] 核验记录(✅HEAD 实测/⏳context 待 re-pin) · TR-1..10 公理表 · 剔除/重映射清单
```

**`qna.md` freeze 尾块（充实）** — `业主裁决摘要表(Q|主题|裁决|来源)` → `业主 vs 联合差异` → `下游 scope 一致性审查` → `跨文档一致性核对` → `冻结声明(blockquote+date+ver)`。

**`design.md 附录 A`（充实）** — `分歧 N(版本/触发)`：`A 方(来源)` / `B 方(来源)` / `最终共识(带 file:line 或 QNA-ID；败方留档)`。

## 7. 风险与落地

| 风险 | 判断 | 缓解 |
|------|------|------|
| 附加章节模板增殖、低频没人用 | medium | 只提拔高频(执行日志/分歧)、净新只做纪律最清晰的(补强/核实)；维护约定不独立 |
| 与整文件模板尾段重复 | medium | 明确：薄占位留在整文件模板里；**厚版独立成附加章节模板**并被前者 `引用` |
| append-only 纪律没人遵守 | high | 每个模板强制 banner(§5.2)；把"冻结后是否改写主体""执行日志是否甩锅带证据"做成 `docs:check` lint |
| 修订历史列名不统一 | low | 抽 `_revision-history` 单一 snippet |

**落地顺序**：① `action-plan-respond`（体量第一、与 code-review-respond 完全对称，最易做）→ ② `post-freeze-addendum`（纪律最清晰、净新价值最高）→ ③ `qna.md` freeze 尾块 + `design.md` 附录 A 充实 → ④ `verification-matrix` → ⑤ `_revision-history` snippet。每个用 1 份历史实例 dogfood 回填验证。

## 8. 一句话结论与给 owner 的决策问题

**一句话**：`code-review-respond` 是一个**品类**的首个成员；正式文件末尾还反复长出 5 类形状稳定的附加章节，其中执行日志(46% action-plan)和分歧记录(41% design)是两座只有薄占位的金矿，冻结后补强是最强净新。建议确立"附加章节模板"为第三品类，新建 3 + 充实 2 + 标准化 1。

**3 个决策问题**：
1. **是否确立"附加章节模板"为独立品类**，并给所有成员加强制 banner（宿主/挂载位/append-only/作者时机）？
2. **数量档**：采"推荐档(新建 3 + 充实 2 + snippet 1)"，还是最小/最大？（我推荐档）
3. **`action-plan-respond` 是否独立成文件**（像 code-review-respond 那样），还是仅充实 `action-plan.md §9` 留在原文件内？

---

## 附录 A · "附加章节"扫描脚本（可接入 docs:check）

```bash
#!/usr/bin/env bash
cd "$(git rev-parse --show-toplevel)"
dirs="docs/eval docs/design docs/action-plan"
grep -rhE '^#{1,4} ' $dirs --include='*.md' > /tmp/headings.txt
tally(){ printf "%-40s %5s\n" "$1" "$(grep -ciE "$2" /tmp/headings.txt)"; }
tally "执行日志回填(Type1)"       "执行日志|执行回填|实际执行|落地回填"
tally "冻结后补强(Type2)"         "增补|补强|更新章节|补题|价值重审"
tally "业主裁决/冻结声明(Type3)"  "业主裁决|裁决摘要|冻结声明|一致性审查"
tally "碰撞核实矩阵(Type4)"       "碰撞核实|核实矩阵|核验记录|事实核查"
tally "分歧/讨论记录(Type5)"      "分歧记录|讨论记录|讨论摘要"
tally "修订历史(通用)"           "修订历史|版本历史|版本说明"
# 强信号：带日期的标题=事后追加
echo "date-stamped headings(files): $(grep -rlE '^#+ .*20[0-9]{2}-[0-9]{2}-[0-9]{2}' $dirs --include='*.md'|wc -l)"
```

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：6 类附加章节扫描 + "附加章节模板"品类确立 + 推荐(新建3+充实2+snippet1) + 真实骨架 |
