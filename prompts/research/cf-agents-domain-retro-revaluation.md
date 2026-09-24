我们将利用 .adocs/templates/truth/per-domain-reference-retro-revaluation.md 作为输出模板与内容约束，对参考仓 context/cf-agents 的**指定 domain**发起一次「跨时价值重估 + nano 映照」的深度审查。

本次重估的背景：`docs/eval/backend-next/cf-agent-analysis/` 下的 15 份母体分析成文于 2026-05-16；如今已隔约 1.5 个月，cf-agents 在此期间大幅演进（时窗内 191 commits / 1502 files 变更）。母体已过时，需用当前 HEAD 实测重估每个 domain 的真实价值与借鉴锚。

**与上次的关键差异——本次逐份产出，不一次性输出**：母体 15 份分析是一次 todo-list 串行、连续产出的。本次不同：我们**一个 domain 一个 domain 地做**，每次调用只交付一份重估报告，跑完、亲验、owner 过目后再进下一个 domain。owner 会通过多次调用本 PROMPT（每次指定不同 {DOMAIN}）逐份推进，最终集齐 15 份。

---

本次调查目标（owner 每次调用时指定其一）：
- **{DOMAIN}** —— 例：`07 — MCP Server / MCP Client / x402`（编号对应母体 `docs/eval/backend-next/cf-agent-analysis/{NN}-*.md`）

固定坐标（campaign 常量，agent 须复核后使用）：
- 参考仓：`context/cf-agents`（本身是带 git 历史的 vendored 仓，可硬锚 commit·PR）
- 本仓：`nano-agent`（本工作树）
- **基线 pin（≈5-16，"then"）**：`480d4f36`（2026-05-15，最接近母体日期的 commit）
- **HEAD pin（6-30，"now"）**：`6560a4aa`（2026-06-30，参考仓当前工作树）
- 母体叙事源（"then" 的第二真源，待证伪）：`docs/eval/backend-next/cf-agent-analysis/{NN}-*.md`
- **报告输出目录（本次落地位置，固定）**：`docs/baseline/cf-agents-truth-0630/domain/` —— 所有重估报告都存这里，单份文件名 `D{NN}-{slug}.md`
- **索引回填**：完成后回填 `docs/baseline/cf-agents-truth-0630/value-assessment-index.md` §7 该域行的 4 槽位（`成熟度裁定 / 借鉴 verdict / nano 映照 / 状态`）

---

调查纪律（每次都遵循）：
1. **read-only 双仓**：不改 context/cf-agents、不改 nano 产品源。发现真 bug / 真缺口 → surface 成 charter 候选（报告 §10.4），不就地改。
2. **零 checkout 读双端点**：参考仓工作树已在 HEAD，HEAD 端点直接读文件；**基线端点一律用 `git -C context/cf-agents show 480d4f36:<path>` / `git log` / `git diff` 读取，禁 checkout/stash/reset/worktree**。禁 sub-agent 对任一仓的未提交态做 git 写。
3. **双仓 file:line 双写**：每条承重结论既给参考仓锚（`file:line@6560a4aa` 或 `commit·PR`），又给 nano 对等锚（`file:line@nano-HEAD`）。
4. **母体即待证伪**：母体是过时二手叙事，凡「母体这么说 → HEAD 实测已变」必点名订正（报告 §9），禁据母体措辞直接结论。
5. **演进≠价值提升**：`git` 有 diff ≠ 对 nano 借鉴价值上升；experimental→experimental 的重构、被刷版但仍 beta-gated 的能力，不得标 `⬆️MATURED`（见模板 §0.1 Δ-verb 纪律）。
6. **机制≠思路**：每个 `✅/🔶` 借鉴点必过模板 §8.3 substrate-fit/TR 过滤，与 nano 路线冲突的机制标降级/重映射，禁直抄进 nano。
7. **★ 双端点分别独立深调 + 价值面对比（本模板灵魂）**：0515 与 0630 是**两个独立真相面**，必须**各自做一次完整深度调查**——分别重建结构/能力/成熟度，并**分别产出该端点的"价值面快照"**（这个能力在当时对使用者/对 nano 值多少）；**然后**显式把 0515 价值面 与 0630 价值面**逐能力对比**，得出「涨/平/降/新生/退役」。**禁**只查 HEAD、拿 git diff 反推「then」——那是偷懒，得不到真实的 0515 价值面。
8. **★ sub-agent 必配定制攻击 PROMPT（本次强约束）**：每一路 fan-out 的 sub-agent，都必须由主进程**亲自为它撰写一份专用「攻击 PROMPT」**再派活；**禁**用「去看一下 packages/xxx」式泛化口令。每份 sub-agent PROMPT 是一份**定向攻击简报**（见下「定制契约」），把该 sub-agent 的端点、靶文件、要攻的不变量、取证格式、回传结构全部钉死。

---

## ★ sub-agent 攻击 PROMPT 定制契约（主进程派每一路 sub-agent 前必须逐条满足）

主进程为每一路 sub-agent 手写的专用 PROMPT，必须包含以下 7 件，缺一不可：
1. **端点与读法钉死**：本 sub-agent 只在**一个**端点作业——`0515`（全程 `git -C context/cf-agents show 480d4f36:<path>`，禁 checkout）/ `0630`（读工作树）/ `nano-HEAD`（读 nano 工作树）。跨端点混读一律拒绝。
2. **靶文件清单**：给出该 sub-agent 要打的**具体 file:line / 目录**（本域已在下方 scope-fence 列出，主进程据此再切子轴）。
3. **攻击不变量**：列出该 sub-agent 要**证实/证伪**的 3–6 条具体不变量/问题（不是「分析一下」，而是「X 是否真 durable？Y 是 stub 还是真跑？Z 的 export 有没有 caller？」）。
4. **该端点的价值面追问**：要求 sub-agent 不只描述结构，还要判**「这个能力在该端点对使用者/对 nano 值多少、成熟到什么程度」**——产出该端点的价值面快照。
5. **取证格式**：每条结论带 `file:line`（注明端点，如 `@480d4f36` / `@6560a4aa` / `@nano-HEAD`）或 `commit·PR`；禁二手措辞、禁据母体转述。
6. **反假绿指令**：显式要求点名 doc-drift / over-claim / stub 冒充 / 死 export / vacuous，并给证伪锚。
7. **回传结构**：规定 sub-agent 用固定小节回传（如 `结构树 / 能力清单+成熟度 / 价值面快照 / 攻击不变量裁定 / 假绿点 / 承重锚`），便于主进程逐条亲验与拼装。

> 一域至少派 **3 路 cf 攻击 sub-agent（0515 深调 · 0630 深调 · 演进/时间线）+ ≥1 路 nano 映照 sub-agent**；域大则每个端点再按子轴拆多路，每路一份独立定制 PROMPT。

---

执行步骤（step by step）：

**Step 0 · 定标（主进程，fan-out 前）**
- 复核 pin：确认 `480d4f36` 为 ≤ 母体日期的最近 commit、`6560a4aa` 为当前 HEAD（`git -C context/cf-agents log -1`）。
- 用 scope-fence 把本 domain 在**两仓**的涉及路径各列一份（参考仓 `packages/*` 等 + nano 对应区域 + d1 schema + rpc）；显式声明「本域不含」交给哪个相邻 domain。
- 通读本域母体 `{NN}-*.md`，抽出母体的：核心文件判定 / DAG / 亮点 / verdict / experimental 标注 —— 作报告 §3「then」真源。

**Step 1 · cf-agents 双端点 fan-out —— 0515 与 0630 各做一次独立深调，再对比价值面**
> 每一路都按上方「定制契约」由主进程手写专用攻击 PROMPT 再派活。**0515 与 0630 不是「基线 reviewer + HEAD reviewer」的轻量对照，而是两次完整、对等、独立的真相面深调**，各自产出该端点的价值面快照；域大则每个端点再按子轴拆多路。

- **1A · 0515 真相面深调（@480d4f36，独立完整）**：为其手写攻击 PROMPT，全程 `git show 480d4f36:<path>`。要求 sub-agent **当作 cf-agents 只存在 0515 这一版**来审——重建结构树/核心文件/能力清单/成熟度(稳定·experimental·beta-gated)，并产出**「0515 价值面快照」**（这些能力在 5-15 时对使用者/对 nano 值多少）。顺带核对**母体在基线时是否就已说错**。取证注明 `@480d4f36`。
- **1B · 0630 真相面深调（@6560a4aa，独立完整）**：为其手写攻击 PROMPT，读工作树。要求 sub-agent **当作全新对象**独立重审 0630 版——结构/DAG/能力/成熟度/对外依赖，并产出**「0630 价值面快照」**。**不得**让它「读 0515 结论再看看变化」——要它独立成像，避免锚定偏差。取证注明 `@6560a4aa`。
- **1C · 演进/时间线深调（BASE..HEAD diff）**：手写攻击 PROMPT，跑 `git log --since=2026-05-15 -- <域路径>`、`git diff --diff-filter=A/D BASE HEAD -- <域路径>`、相关包 `CHANGELOG.md`/`Version Packages` semver 跃迁；逐变更打 Δ-verb（🆕/⬆️/🔧/🔀/➖/⚠️/➡️），识别净新/退役。输出带 `commit·PR` 的时间线。
- **1D · 0515↔0630 价值面对比（主进程亲做，不外包）**：拿回 1A 的「0515 价值面快照」与 1B 的「0630 价值面快照」，**逐能力两列并置对比**——该能力值不值得借这 1.5 月是**涨/平/降/新生/退役**？涨在哪、降在哪？1C 的 Δ-verb 只解释「代码怎么变」，本步回答「**价值怎么变**」。此即 §5 价值台账的直接原料，**禁**由单一 sub-agent 顺手带出。

**Step 2 · nano-agent fan-out（可与 Step 1 并行，同样配定制攻击 PROMPT）**
- **B1 nano 映照深调（@nano-HEAD）**：为其手写攻击 PROMPT，对**同一功能区域**在 nano 现状做深度审查（相关代码 / d1 schema / rpc）；以母体 + 1B 的 0630 能力清单为核对表，逐能力判 nano 侧 `已有对等 / 部分对等 / 缺失 / 不适用`，给 `file:line@nano-HEAD`，并标 nano 与 cf 的**路线差异**（防「缺失」误判为实为「不适用」）。产报告 §7 原料。

**Step 3 · 汇聚 + 双仓 trust-code 亲验 + reverse-water（主进程）**
- 回收 1A/1B/1C/B1，主进程**亲手复核每条承重锚**（双仓各打开 file:line 或跑 git 核对），禁据 sub-agent 二手措辞。
- reverse-water：用 1A（母体 vs code@0515）+ 1B（code@0630）对齐，得出「母体当时就错了什么」+「这 1.5 个月又漂移了什么」→ 报告 §9。
- 把 Step 1D 的价值对比 + B1 的 nano 映照，对每个候选借鉴点过 substrate-fit/TR 过滤（结合 nano 路线），落成 §8 台账。

**Step 4 · 按模板撰写报告**
- 严格按 `.adocs/templates/truth/per-domain-reference-retro-revaluation.md` 骨架，写入 `docs/baseline/cf-agents-truth-0630/domain/D{NN}-{slug}.md`。头部填 pin 时窗、母体锚、`结构来源(dogfood)` 行；文档状态起始 `draft`。
- **必须写足两个承重段**：§5 价值台账对比（soul，逐能力 **0515 价值面 vs 0630 价值面**两列并置 + Δ-verb + 独立判「借鉴价值变化 ↑/→/↓/✗」+ 证据锚 —— 直接落 Step 1D 的对比结果）；§8 推荐参照物台账（payload，借鉴矩阵 + TR 过滤 + 落到 nano 哪个 file:line/相位）。
- §7 双仓 parity 表、§9 reverse-water、§10 重估 verdict（go-borrow / borrow-with-fence / watch-only / skip-now）+ 母体订正回填指令，一并写全。
- **回填索引**：报告 attested 后，回填 `docs/baseline/cf-agents-truth-0630/value-assessment-index.md` §7 该域行的 4 槽位。

**Step 5 · 自检（断点盲点核查）**
- 复核每条锚是否真实存在（双仓、注明端点）；Δ-verb 是否与「借鉴价值变化」误合并；是否有母体过时结论漏订正；§8 每个 `✅/🔶` 是否都过了 TR 过滤且给了 nano 落点。发现问题当场修正。

---

请在全面理解工作目标后，对指定的 {DOMAIN}：先为每一路 sub-agent **手写专用攻击 PROMPT**（依「定制契约」），再发起 **0515 独立深调 / 0630 独立深调 / 演进时间线 / nano 映照** 的 fan-out，主进程亲做 **0515↔0630 价值面对比** 并双仓亲验，最后按模板输出深度重估报告至 `docs/baseline/cf-agents-truth-0630/domain/`。**本次只做这一个 domain**：构建独立上下文、单份交付、亲验自检 + 回填索引后即停，等 owner 过目再进下一个 —— 不要顺手把其它 domain 一起做了。19 份将由 owner 多次调用逐份集齐。
