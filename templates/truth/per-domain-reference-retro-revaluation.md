# Assessment 模板簇（truth 子簇）· per-domain-reference-retro-revaluation —— 外参单域「跨时价值重估 + 借鉴映照」

> **模板簇**：`assessment / truth`（真值奠基子簇）· **本文血统 = 三模板 dogfood 组合**（README §3）：
> **主骨架** [[truth/per-domain-analysis]]（measure-first / code-anchored / 反假绿 / reverse-water / verdict）
> **+ 借入** [[eval-retrospective]] 模块（§1 时间线 / §2 根因表 / §3 教训 → 本文重铸为「演进时间线 / 演进驱动力 / 对 nano 启示」）
> **+ 借入** [[eval-reference-anchor]] 模块（§0.1 借鉴 verdict `✅/🔶/⛔/🆕` / §5 substrate-fit·TR 过滤 / §0.2 置信分层 → 本文 §8 参照物台账）。
> **头部写一行**：`结构来源(dogfood): truth/per-domain-analysis 骨架 + eval-retrospective §1-3 + eval-reference-anchor §0.1/§0.2/§5`。
>
> **一句话用途**：对一个**外部参考仓**（如 `context/cf-agents`）的**一个域**，做一次「**母体分析已过时 → 用当前 HEAD 实测重估其价值 → 量化这段时间的演进 Δ → 映照本仓 nano-agent → 产出可落地的 `file:line` 借鉴台账**」的 read-only、git-grounded、code-anchored 分析——**回答「这个域这 `{ELAPSED}` 里做了什么、价值涨没涨、现在还值不值得借、借哪一行」**。
> **何时用**：某份**外参母体分析**（如 `docs/eval/.../cf-agent-analysis/{NN}-*.md`）已存在但**已隔 `{ELAPSED}`**、参考仓 HEAD 已大幅演进、owner 要对该域**重新估值 + 刷新借鉴锚**时；每域一份。
> **何时不用**：① 首次评估外参、**无母体基线可 diff** → 用 [[eval-reference-anchor]]（纯借鉴台账）或 [[eval-gap-study]]；② 评估的是**本仓自己**的真值层（非外参） → 用 [[truth/per-domain-analysis]]；③ 只回看一次**决策失误** → 用 [[eval-retrospective]]；④ 还在切域 / 派活 / 编排 campaign → 用 [[truth/assessment-index]]（可复用为本文的站①）。
>
> **调查纪律（truth 簇共有脊 + 本文跨时/跨仓特化）**：
> 1. **git-grounded measure-first**：一切「现在怎样」以**参考仓 HEAD 实测**为准；一切「Δ / 演进了什么」以**基线 pin commit → HEAD 的 `git log/diff`** 为准，每条带 `commit·PR` **或** `file:line`（双仓锚双写：参考仓锚 + nano 锚）。
> 2. **母体即待证伪（reverse-water 特化）**：母体分析（`{NN}-*.md`）本身是**过时二手叙事**——凡「母体这么说 → HEAD 实测已变」必点名 + 订正留痕（§9）；**禁据母体措辞直接结论**。
> 3. **degraded≠matured / 演进≠价值提升**：`git` 有 diff ≠ 该能力对 nano 的**借鉴价值**上升；experimental→experimental 的重构、被 `Version Packages` 刷版但仍 beta-gated 的能力，**不得**标 `⬆️MATURED`（见 §0.1 Δ-verb 纪律）。
> 4. **机制≠思路（TR 过滤，借鉴闸门）**：每个 `✅/🔶` 借鉴点必过 §8.3 substrate-fit/TR 过滤，与 nano 路线冲突的机制标降级/重映射，**禁把参考仓机制直抄进 nano**。
> 5. **read-only-first + sub-agent 安全**：纯只读双仓；不改参考仓、不改 nano 产品源；真 bug / 真缺口 → surface 成 charter 候选（§10.4），不就地改；**禁 sub-agent 对共享未提交态 git 写**。
> 6. **判据引用不复制**：借鉴 verdict 图例（[[eval-reference-anchor]] §0.1）、置信分层（同 §0.2）、（如启用参考仓成熟度分层）T1-T4（[[truth/assessment-index]] §2.1）**引用章节号**，不另立词表。
>
> **★ 覆盖核对（必全覆盖）**：①演进实测→§2/§4 · ②母体基线→§3 · ③价值 Δ 台账→§5（soul）· ④驱动力+启示→§6 · ⑤nano 映照→§7 · ⑥参照物台账→§8（payload）· ⑦假绿/漂移复核→§9 · ⑧重估 verdict→§10。
> **状态词汇（本簇自有）**：`draft`（sub-agent 初稿）→ `cross-reviewed`（复核 fleet 双仓独立 re-verify 过）→ `attested`（主进程 trust-code 双仓亲验，作上卷源）→ `superseded`（被下一轮重估取代）。
> **占位符约定**：`{UPPER_SNAKE}` backtick 包裹；`[核心]` 必填 / `[可选]` 视域删除。
> **流水线位置**：本文 = **站②·重估变体** · 上游 = [[truth/assessment-index]]（可复用为站①：切 `{N}` 域 + pin 基线 commit）+ `{MOTHER_ANALYSIS_ANCHOR}`（母体，待证伪）· 下游 = [[truth/per-cluster-value-proposition]]（簇级上卷「本簇能借什么」）+ 借鉴锚回灌 [[eval-reference-anchor]] / [[planning-proposed]]（`T-R` 事实源）。

---

# D`{NN}` — `{DOMAIN_NAME}`（外参跨时价值重估 · reference retro-revaluation）

> **参考仓**：`{REFERENCE_REPO}`（如 `context/cf-agents`）· **本仓**：`{OUR_PROJECT}`（如 `nano-agent`）
> **域 scope-fence**：本文覆盖 `{WHAT_THIS_DOMAIN_COVERS}`；**本域不含**：`{EXPLICIT_OUT_OF_DOMAIN}`（交由 D`{OTHER_NN}`）。
> **母体分析（基线叙事，待证伪）**：`{MOTHER_ANALYSIS_PATH}`（`{MOTHER_DATE}` 快照）
> **时窗**：基线 pin `{BASELINE_COMMIT}`（`{BASELINE_DATE}`，最接近母体日期的参考仓 commit）→ HEAD `{HEAD_COMMIT}`（`{HEAD_DATE}`）· **跨度 `{ELAPSED}`** · **本域触达 `{DOMAIN_COMMIT_COUNT}` commits**
> **日期**：`{DATE}` · **作者**：`{AUTHOR}`（sub-agent / fleet：`{AGENTS_OR_NONE}`）
> **文档性质**：`assessment / truth-domain-revaluation`（外参单域跨时重估；零决策——owner 拍板点列 §10.4 并 MARK）
> **文档状态**：`draft | cross-reviewed | attested | superseded`
> **结构来源(dogfood)**：`truth/per-domain-analysis 骨架 + eval-retrospective §1-3 + eval-reference-anchor §0.1/§0.2/§5`

---

## 0. TL;DR（重估结论先行）`[核心]`

- **headline Δ（一句话：这段时间本域最大的变化）**：`{TOP_EVOLUTION_ONE_LINE}`
- **价值重估 verdict**：`{🟢 go-borrow / 🟡 borrow-with-fence / 🟠 watch-only / 🔴 skip-now}` + `{ONE_LINE}`（详 §10）
- **对 nano 最值得借的净新锚（新增于本时窗）**：`{TOP_NEW_BORROW_ANCHOR — 参考仓 file:line@HEAD → nano 落点}`
- **母体最需订正的过时结论**：`{TOP_STALE_MOTHER_CLAIM_OR_NONE}`（详 §9）

### 0.1 Δ-verb 图例（跨时变化分类 · 本模板自有）★

> 对每条能力按「基线→HEAD」打 **一个** Δ-verb。**纪律**：Δ-verb 描述**代码事实的变化**，不等于**借鉴价值的变化**（后者见 §5「价值变化」列与 §8）。

| 符号 | 含义 | 判据 |
|---|---|---|
| `🆕 NEW` | 基线时不存在，本时窗净新 | `git log --diff-filter=A` 命中 / 母体无此条 |
| `⬆️ MATURED` | 已存在，且**真的更可用**（出实验、加测试、稳定 API、live 兑现） | 有 `Version Packages` 稳定版跃迁 **或** experimental 标记移除 **或** 测试/覆盖新增，逐锚证 |
| `🔧 REFACTORED` | 重塑但意图不变（拆巨石、换实现、挪模块） | diff 大但对外契约/能力等价 |
| `🔀 RENAMED/MOVED` | 更名 / 迁包 / 换 export 路径 | 路径变、语义同 |
| `➖ REMOVED/RETIRED` | 基线有、HEAD 已删 / 弃用 | `git log --diff-filter=D` / deprecation |
| `⚠️ REGRESSED` | 变得更差 / 更受限 / 引入新围栏 | 能力收窄、依赖更重、新 beta-gate |
| `➡️ UNCHANGED` | 本时窗基本未动 | 无实质 diff |

### 0.2 借鉴 verdict + 置信图例（引用 [[eval-reference-anchor]] §0.1/§0.2，不复制）

- **借鉴 verdict**：`✅ 借` / `🔶 部分借（机制需 TR 改造）` / `⛔ 反例（避坑）` / `🆕 净新（nano 无参考）`。
- **置信分层**：`ref-line`（已落参考仓 `file:line@{HEAD_COMMIT}`，最高）/ `HEAD`（已对 nano HEAD 复核）/ `web-*`。

---

## 1. 本域介绍 + 为什么现在重估 `[核心]`

### 1.1 什么是「`{DOMAIN_NAME}`」（在参考仓中的角色）
`{PLAIN_LANGUAGE_WHAT_THIS_DOMAIN_DOES}`

### 1.2 为什么重估（重估的原因）
`{WHY — 母体已隔 {ELAPSED}；本域本时窗被 {DOMAIN_COMMIT_COUNT} commits 触达；owner 要刷新借鉴锚 / 已知参考仓大改}`

### 1.3 本域重估要回答的关键问题（答案见对应节）
- Q1 这段时间本域**做了什么**（演进 Δ）？ → §2 / §5
- Q2 价值**涨没涨**、涨在哪？ → §5 / §6
- Q3 母体哪些结论**过时了**？ → §9
- Q4 nano **有没有对等物**、差距多大？ → §7
- Q5 现在**该借哪一行**、怎么落地？ → §8 / §10

---

## 2. 演进时间线（git-grounded）`[核心]`  ｜ 借自 eval-retrospective §1

> 基线→HEAD 本域的关键演进事件流。**每行带 `commit·PR`**；来源 = `git log --since={BASELINE_DATE} -- {DOMAIN_PATHS}`（复现见附录 A）。**只记本域相关**，噪音（版本机器人、格式化）折叠。

| 时间 / commit·PR | 发生了什么（本域） | 类型（Δ-verb） | 影响面（`file:line` 或包） |
|---|---|---|---|
| `{DATE} {COMMIT}·#{PR}` | `{WHAT_CHANGED}` | `{Δ-verb}` | `{IMPACT}` |

- **版本跃迁信号（成熟度）**：`{CHANGELOG_OR_VERSION_PACKAGES_BUMPS — 本域相关包的 semver 变化，如 0.0.1→0.2.0}`（`{CHANGELOG_ANCHOR}`）。

---

## 3. 5-16 基线快照（母体怎么说 —— 待证伪的「then」）`[核心]`  ｜ 借自 eval-retrospective §4「错误/旧形态」位

> 忠实转录母体分析对本域的**当时结论**，作 §5 台账的「then」列真源。**不评判、不订正**（订正留到 §9）。

- **母体核心文件判定**：`{MOTHER_CORE_FILES}`（`{MOTHER_ANCHOR}`）
- **母体 DAG / 结构判定**：`{MOTHER_STRUCTURE_ONE_LINE}`
- **母体亮点判定**：`{MOTHER_HIGHLIGHTS}`
- **母体 verdict + 风险判定**：`{MOTHER_VERDICT_AND_RISKS}`
- **母体标注的 experimental / 未成熟点**：`{MOTHER_EXPERIMENTAL_FLAGS}`

---

## 4. 当前结构实测（HEAD@`{HEAD_COMMIT}` · Δ 标注）`[核心]`  ｜ 借自 truth/per-domain-analysis §2-3

> measure-first 复勘参考仓当前结构，**并对每处标 Δ vs §3 母体**。先把「现在的文件树/核心文件/主路径」画准，再高亮变化。

### 4.1 当前文件树 + 核心文件（Δ 标注）
```text
{CURRENT_FILE_TREE — 每个关键文件后标 [🆕/⬆️/🔧/🔀/➖/➡️] vs 母体}
```

### 4.2 当前主调用路径 / 状态机（Δ 标注）
```text
{CURRENT_CALL_PATH_TREE — entry → facade → engine → durable；标出本时窗新增/改道的 hop}
```

### 4.3 核心文件变迁表
| 文件 / 模块 | 母体角色 | HEAD 角色 | Δ-verb | `commit·PR` / `file:line@HEAD` |
|---|---|---|---|---|
| `{FILE}` | `{THEN_ROLE}` | `{NOW_ROLE}` | `{Δ-verb}` | `{ANCHOR}` |

---

## 5. ★ 价值台账对比（跨时 value-delta ledger —— 本模板的灵魂）`[核心]`

> 本节是重估的**承重梁**：逐能力把「基线状态 → HEAD 实测」对齐，判 Δ-verb，并**独立判「借鉴价值变化」**（涨/平/降/不再相关）。每行「HEAD 实测」列必带 `commit·PR` 或 `file:line@{HEAD_COMMIT}`。

### 5.1 逐能力价值 Δ 台账
| # | 能力 | 5-16 状态（母体，§3）| 7-01 实测（HEAD + 锚）| Δ-verb | 借鉴价值变化 | 证据锚 |
|---|---|---|---|---|---|---|
| `V-1` | `{CAPABILITY}` | `{THEN_STATE}` | `{NOW_STATE + commit·PR}` | `{🆕/⬆️/🔧/🔀/➖/⚠️/➡️}` | `{↑提升 / →持平 / ↓降低 / ✗不再相关}` | `{REF_FILE_LINE@HEAD}` |

> **借鉴价值变化纪律**：`↑` 仅当该能力**对 nano 更值得借**了（出实验 / 契约稳定 / 新增可直采的 primitive）；纯内部重构对 nano 借鉴价值常为 `→`。

### 5.2 净新能力（🆕 —— 基线后诞生，母体完全未覆盖）`[核心]`
| 净新能力 | 诞生 `commit·PR` | 现状成熟度 | 对 nano 是否有借鉴潜力 | 锚 |
|---|---|---|---|---|
| `{NEW_CAP}` | `{COMMIT·PR}` | `{stable / experimental / beta-gated}` | `{是→§8 / 否+为什么}` | `{ANCHOR}` |

### 5.3 退役 / 回归 / 收窄（➖ / ⚠️）`[可选]`
| 项 | Δ-verb | 发生了什么 | 对「母体曾推荐借」的影响 | 锚 |
|---|---|---|---|---|
| `{ITEM}` | `{➖/⚠️}` | `{WHAT}` | `{母体曾荐借此→现已退役/收窄，撤回借鉴}` | `{ANCHOR}` |

---

## 6. 演进驱动力 + 对 nano 的启示 `[核心]`  ｜ 借自 eval-retrospective §2 根因表 / §3 教训

### 6.1 演进驱动力（为什么参考仓在本域这样投入 —— 追到机制/方向层）
| 编号 | 驱动力 | 类型 | 揭示的方向 |
|---|---|---|---|
| `DR-1` | `{DRIVER}` | `产品化 / 安全补强 / 巨石拆分 / 平台化 / 外部依赖成熟 / 文档收敛` | `{WHAT_DIRECTION_IT_REVEALS}` |

### 6.2 对 nano-agent 的可迁移启示（写成「nano 若遇 X，应 Y」）
1. `{LESSON_1}`
2. `{LESSON_2}`

> **纪律**：启示要追到「机制/认知」层，不止于「他们加了个 feature」；每条尽量指向 §7 的 nano 现状或 §8 的落点。

---

## 7. ★ nano-agent 映照对比（双仓 parity，measure-first）`[核心]`  ｜ 借自 truth/per-domain-analysis §6（改为跨仓）

> 逐能力把参考仓 HEAD 锚 **映照到 nano 现状锚**。**双仓 file:line 双写**；nano 侧以 nano HEAD 实测为准（不是母体、不是记忆）。

| # | 参考仓能力 | 参考仓锚（`file:line@{HEAD_COMMIT}`）| nano 对等物（`file:line@nano-HEAD`）| parity | gap 一句话 |
|---|---|---|---|---|---|
| `M-1` | `{REF_CAP}` | `{REF_ANCHOR}` | `{NANO_ANCHOR_OR_NONE}` | `{✅已有对等 / 🔶部分对等 / ❌缺失 / ➖不适用}` | `{GAP_ONE_LINE}` |

- **parity 总览**：`{HOW_MANY_HAVE / PARTIAL / MISSING}`——nano 在本域整体处于 `{领先 / 持平 / 落后 / 路线不同}`。
- **路线差异声明（防误抄）**：`{WHERE_NANO_ROUTE_DIVERGES — 参考仓走 X、nano 走 Y，故某些能力「不适用」而非「缺失」}`。

---

## 8. ★ 推荐参照物台账（借鉴 payload —— 给 nano 的 `file:line`）`[核心]`  ｜ 借自 eval-reference-anchor §1/§2/§3/§5

> 本节是本文的**交付载荷**：把「值得借」的参考仓锚，过 TR 过滤，落成 nano 可消费的借鉴条目。**只收 §5 判为 `↑/→` 且当前成熟度足够的能力**；`✗不再相关 / ➖退役` 的不进本表（进 §8.2 反例或直接略）。

### 8.1 借鉴锚定矩阵（✅ / 🔶）
| 借鉴点 | 参考仓来源（`file:line@{HEAD_COMMIT}`）| 本时窗 Δ | Verdict | 置信 | 借什么 / 不借什么 |
|---|---|---|---|---|---|
| `{POINT}` | `{REF_ANCHOR}` | `{🆕/⬆️/🔧}` | `{✅/🔶}` | `{ref-line/HEAD}` | `{WHAT_TO_BORROW}` |

### 8.2 反例坑表（⛔ —— 本时窗新暴露的「别学」）`[可选]`
| 反例 | 参考仓来源 | 为什么不可借（尤其本时窗才暴露的） | nano 怎么做 |
|---|---|---|---|
| `{ANTI_PATTERN}` | `{SOURCE}` | `{WHY_NOT}` | `{OUR_APPROACH}` |

### 8.3 substrate-fit / TR 过滤复核（借鉴闸门 · 引用 [[eval-reference-anchor]] §5）`[核心]`
> 对每个 ✅/🔶 点：机制与 nano substrate 是否适配？冲突的降级/重映射成什么？**这是阻止把参考仓机制直抄进 nano 的闸门。**

| 借鉴点 | 参考仓原机制 | 与 nano 路线（TR-x）冲突? | 过滤后 nano 落地形态（降级/重映射/直采）| 落点（nano `file:line` / 相位）|
|---|---|---|---|---|
| `{POINT}` | `{ORIGINAL_MECHANISM}` | `TR-{x}: 冲突/兼容` | `{ADAPTED_FORM}` | `{NANO_LANDING}` |

- **substrate-fit 总结（对 nano HEAD）**：`{SUBSTRATE_FIT_SUMMARY}`

### 8.4 净新表（🆕 —— nano 无参考、须净新）`[可选]`
| 净新点 | 为什么无参考可借 | 建议落点（哪个 design/相位）|
|---|---|---|
| `{NET_NEW}` | `{WHY_NO_REF}` | `{WHERE}` |

---

## 9. 假绿 / 漂移复核（reverse-water —— 订正过时母体 + 参考仓自身漂移）`[核心]`  ｜ 借自 truth/per-domain-analysis §9.2

> **本节是反假绿在跨时语境的留痕**：母体（`{MOTHER_ANALYSIS_PATH}`）是过时二手叙事，参考仓自己的 docs 也可能进一步漂移。逐条：**谁怎么说 → HEAD 实测怎样 → 订正成什么**（带锚）。

1. **母体过时**：母体称 `{母体声称}` → HEAD 实测 `{实测}` → 订正为 `{CORRECTION}`（`{ANCHOR}`）。
2. **参考仓文档漂移（本时窗新增/仍存）**：`{REPO_DOC_DRIFT — 如 README publish 状态、design doc 非事实源、CHANGELOG 与代码不符}`（`{ANCHOR}`）。
3. **母体曾荐借、现已失效**：`{母体 §x 荐借的锚}` 现已 `{移动/删除/收窄}` → 撤回或改锚为 `{NEW_ANCHOR}`。

---

## 10. 最终 verdict + 价值重估 `[核心]`  ｜ 借自 truth/per-domain-analysis §9.4 + eval-reference-anchor verdict

### 10.1 价值重估热力图（母体 → 现在）
| 维度 | 母体判定 | 现重估 | 一句话 |
|---|---|---|---|
| 成熟度 | `{THEN}` | `{NOW}` | `{ONE_LINE}` |
| 对 nano 借鉴价值 | `{THEN}` | `{NOW ↑/→/↓}` | `{ONE_LINE}` |

### 10.2 最终 verdict
**`{🟢 go-borrow / 🟡 borrow-with-fence / 🟠 watch-only / 🔴 skip-now}`（`{置信度}`）。**

- **nano 今天能放心借（go-borrow）**：`{WHAT + 指向 §8 条目}`
- **须围栏借（fence）**：`{WHAT_TO_FENCE + WHY — 如仍 experimental / 依赖 beta / TR 需改造}`
- **只观察不借（watch）/ 现在别碰（skip）**：`{WHAT + reopen 触发器}`
- **置信度依据**：`{哪些 ref-line 亲验 / 哪些仅 web / 哪些 nano 侧未复核}`

### 10.3 母体订正回填指令
- **回填母体 `{NN}-*.md`**：`{WHICH_CLAIMS_TO_MARK_STALE — 或建议整份标 superseded-by 本文}`。

### 10.4 推荐后续（owner 裁，read-only 阶段不就地改）
| 优先 | 项 | 动作 | 触发 charter / design | 锚 |
|---|---|---|---|---|
| `{P0/P1/P2}` | `{ITEM}` | `{ACTION — 如「把 §8.1 X 借入 nano Y 相位」}` | `{CHARTER}` | `{ANCHOR}` |

> **一句话**：`{PLAIN_LANGUAGE_REVALUATION_FOR_OWNER}`

---

## 附录 A · 双仓复现命令（git-grounded 锚点复现）

```bash
# —— 时窗与基线 pin（参考仓）——
REF={REFERENCE_REPO}            # 如 context/cf-agents
BASE={BASELINE_COMMIT}         # 最接近母体日期的 commit
HEAD={HEAD_COMMIT}
PATHS="{DOMAIN_PATHS}"          # 本域涉及的参考仓路径（空格分隔）

# 1. 本域演进时间线（§2）：只看本域路径的 commit + PR
git -C $REF log --since="{BASELINE_DATE}" --until="{HEAD_DATE}" --oneline -- $PATHS

# 2. 本域净新/删除文件（§5.2 / §5.3）
git -C $REF diff --stat --diff-filter=A $BASE $HEAD -- $PATHS   # 新增
git -C $REF diff --stat --diff-filter=D $BASE $HEAD -- $PATHS   # 删除

# 3. 成熟度信号（§2 版本跃迁）：本域相关包的 CHANGELOG / semver
git -C $REF log --oneline $BASE..$HEAD -- {PACKAGE_CHANGELOG_PATHS}

# 4. 核心文件当前锚（§4 / §8，参考仓 HEAD）
{REF_HEAD_GREP_COMMANDS — sed/grep 钉每条承重借鉴锚@HEAD}

# —— nano 侧映照（§7 / §8.3）——
{NANO_HEAD_GREP_COMMANDS — 钉每条 nano 对等物/落点锚@nano-HEAD}
```

- **{K} 路 read-only sub-agent 分轴建议**：A 演进时间线+版本（§2）· B 结构实测 Δ（§4）· C 价值台账（§5，soul）· D nano 映照+参照物（§7/§8）· E 假绿/漂移复核（§9）。主进程双仓 trust-code 亲验汇总。

## 附录 B · 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿（Δ-verb rubric + git-grounded 时间线 + 价值台账对比 soul + nano 映照 + 参照物台账 + reverse-water 订正母体 + 重估 verdict） |
