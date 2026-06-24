# design 文档的真实定位、实际价值与 potential —— 为 owner 解惑

> 文档对象：`design.md` 在 `charter → design → action-plan` 链条中的真实角色
> 作者：Claude Opus 4.8（3 路并行证据采样：design↔action-plan 消费追踪 / charter-lite 自然实验 / design 章节利用率审计）
> 日期：2026-05-30
> 文档性质：`eval / general-purpose`（辨证分析，冻结零决策）
> 文档状态：`draft — 待 owner 审阅`
> 调查输入：
> - 3 对 design↔action-plan（BSSBD3↔BSSB3 / RH4↔RH4 / MCD3↔MC4）逐项消费追踪
> - charter-lite 自然实验（MIX-wave-1 跳过 design 的 MIX1/MIX5 vs design-backed MI4/MID4）
> - 5 份真实 design 的章节利用率审计（MCD3/BSSBD4/RH2/HP5/PP2）
> 关联：`charter-lite.md`（owner 跳过 design 的现行方案）、`eval-docs-re-design.md`、`design-sketch.md`、`better-planning.md`

---

## 0. 一句话结论（TL;DR）

**owner 的直觉一半是对的，但结论overshoot 了。**

- ✅ **对**：design **确实臃肿**，且其"决策冻结"职责**确实不如 qna**——证据上，design 的 §9（QNA 登记）是每一对 design↔action-plan 里**被消费最少**的一节，action-plan 一律绕过它直接引 qna register。design 的 §4（三方参考对比）也**确已腐烂**（5 份里 4 份把 mini-agent 列留空/N/A）。§10（Value Verdict）是自评仪式。**这三块就是 owner 感受到的"虚"。**
- ❌ **错**：owner 把"design ≈ 定位 reference anchor"当成 design 的**主职**——但证据显示 action-plan **真正逐字消费的是 §7（可验证验收条件）和 §3（架构边界 解耦/聚合点）**，参考对比（§4）反而是最 inert 的一节。owner 把"弱的 §4 外部参考"误当成了 design 的本体，却没看见"强的 §7+§3"才是 design 不可替代的核心。
- 🔑 **真相**：design 的真实定位 = **把已冻结的决策（charter/qna）翻译成"完工长什么样"（§7 验收条件）+"接缝在哪里"（§3 架构边界）的规格层**。qna 冻结的是"做哪个（yes/no）"；design 产出的是"做完的可验证标准 + 落点结构"——**这是 qna 一两句话答案装不下、charter 太粗、action-plan 又必须消费的那一层**。

**给 owner 的核心建议（与你的直觉同向、但纠正 overshoot）**：**不是废除 design，也不是原样保留——而是把 design 砍到只剩不可替代的核心（§7 验收 + §3 边界 + §1.1 术语 + §8 仓内锚），删掉腐烂的 §4/§10、把 §9 降为"只登记本文新生决策 + 指向 register"。** 这恰好落实你"design 太虚"的判断，又不至于把规格层一起扔掉。并把 design 改为**条件触发**（用"模糊度检测"决定走 design 还是 charter-lite）——你的 charter-lite 不是反 design，它本身就是一个"design 必要性探测器"。

---

## 1. 调查方法（三路证据，互相印证）

| 路 | 问题 | 方法 |
|----|------|------|
| A · 消费追踪 | action-plan 究竟从 design **吃**了什么？ | 3 对 design↔action-plan 逐项：design §7 验收条件是否 1:1 落进 action-plan 的收口/测试？哪节从不被引用？ |
| B · charter-lite 自然实验 | design 被**跳过**后，它的活去哪了？ | MIX-wave-1（charter-lite 跳 design）的 MIX1（低模糊）/ MIX5（高模糊·SSRF）vs MI4（有 MID4 design）对照 |
| C · 章节利用率审计 | design.md 哪些节**承重**、哪些**仪式**？ | 5 份真实 design 逐节评级 LOAD-BEARING / THIN / CEREMONIAL |

三路独立采样，结论高度收敛（见 §4–§6）。

## 2. owner 的两个假设，逐一辨证裁定

### 2.1 假设一："design 最重要的功能就是定位 / 确定 reference anchor"

**裁定：作为主职——证伪；但藏着一个被混淆的真问题。**

- **§4（三方外部参考对比）确实弱**：5 份审计里，mini-agent 列普遍空/N/A，RH2 干脆把 §4 改写成"当前 schema / 当前 client / 本设计倾向"（纯内部 precedent，零外部代码），HP5 只填 2/3 列，PP2 悄悄删 mini-agent 列。**owner 对"外部参考对比很虚"的感受，证据完全支持。**
- **但 owner 混淆了 §4 与 §8**：§8（**仓内** file:line 借鉴/反例锚）在 5 份里**全部 load-bearing**，而且是 action-plan 真用的——RH4 的 action-plan 重度依赖 §8 的"`artifacts.ts:27-60` 是替换点"、"adapter 已建好别重写"、"`wrangler:43-50` 注释 binding"，**§8 让 action-plan 省掉了重新摸 substrate**。
- **结论**：owner 说的"reference anchor"如果指**外部三方对比（§4）**，那确实是 design 最该砍的部分；但若指**仓内代码锚（§8）**，那是 design 的真价值之一。**把这两者分开，是解惑的第一刀。**

### 2.2 假设二："qna 的作用比 design 还大"

**裁定：在"决策冻结"这件事上——成立；但这不等于 design 是 dead weight。**

- **qna 在决策冻结上完胜 design**：3 对里，冻结决策都活在 qna register（`pre-charter-qna` / `RHX-qna` / `MCX-qna`），**action-plan 一律直接引 qna，绕过 design 的 §9**。MCD3 的 §9 自己都写明"决策不在本设计展开……下表仅为索引"。**owner 对"qna 比 design §9 重要"的判断，证据完全支持。**
- **但 qna 产不出 design 的核心产物**：qna 冻结的是"做哪个（二元/具体结论）"；它**装不下**——
  - **§7 的逐功能可验证验收条件**（"GET /sessions/{id}/audit 返回 redacted、无 r2_key 泄漏"这种"完工长什么样"）；
  - **§3 的架构边界**（解耦点/聚合点——MCD3 的 §3.4 聚合对象直接变成 action-plan 的**新建文件清单** `context-fragments.ts`）。
- **结论**：qna > design **仅限决策冻结**。design 的不可替代价值在**别处**（§7+§3），而那恰恰是 qna 结构上承载不了的。owner 拿 qna 的强项（决策）比 design 的弱项（§9），自然觉得 design 多余——但这是**比错了维度**。

## 3. design 的真实定位：规格层（spec layer）

把整条链按"它各自产出什么、下游消费什么"摆开，分工其实很干净：

| 文档 | 回答 | 产物 | 谁消费 |
|------|------|------|--------|
| charter | 为什么现在做 + 阶段边界 | 粗粒度 scope/phase | design / action-plan |
| **qna** | **做哪个**（owner 二元裁决） | 冻结决策 | design / action-plan **直接引** |
| **design** | **完工长什么样 + 接缝在哪** ★ | **§7 验收条件 + §3 架构边界 + §1.1 术语 + §8 仓内锚** | **action-plan 逐字消费** |
| action-plan | 怎么做 + 何时 + 何序 + 怎么测 | phase 序列 / 文件级工作 / 测试命令 / 执行日志 | 实现 |

**接缝判别法（一句话验证 design vs action-plan 边界）**：
> **改"实现顺序"→ 只动 action-plan；改"完工标准/接缝位置"→ 动 design。** 二者是正交轴：design = WHAT-done-looks-like（稳定规格），action-plan = HOW/WHEN（可变执行）。

design 的一句话定位：**它是把"决策"翻译成"可验收规格 + 落点结构"的那一层——上游 charter/qna 给"做什么/做哪个"，下游 action-plan 要"怎么落、落哪、何算完"，中间这层翻译只有 design 做。**

## 4. 证据 A：action-plan 究竟消费 design 的什么（消费排序）

3 对 design↔action-plan 的消费强度排序高度一致：

> **§7（验收条件）≈ §3（架构边界）＞ §8（仓内代码锚）＞ §4（外部参考）＞ §9（决策索引，qna 做得更好）**

- **§7 逐字落地**：BSSBD3 的 F2"每个 terminal path 都有 reason"→ BSSB3 §8.2 收口"no ended row without reason"；MCD3 与 MC4 **共用同一套 MC4-T01..T10 Test-ID**，验收条件几乎机械搬运。
- **§3 变成新建文件清单**：MCD3 §3.4 聚合对象 → MC4 新建 `context-fragments.ts`；BSSBD3 §3.4 聚合（统一 terminal helper）→ BSSB3 P2-01 工作项。
- **§8 救 action-plan 摸底**：RH4 重度引"替换点 / 已建好别重写 / 注释 binding"。
- **§4/§9 基本 inert**：外部参考除 MCD3 外几乎不传导；§9 每对都被 qna 绕过。
- **action-plan 自己加的**（证明它不是透传）：phase 排序、文件级工作表、测试命令、执行日志，**有时还推翻 design**（RH4 把 design 的 `ArtifactStore` 改名 `SessionFileStore` 并纠正 sync/async 误判）。

## 5. 证据 B：charter-lite 自然实验——design 被跳过后去哪了

owner 已经亲手做了这个实验。结论：**design 的活不会消失，它会迁移；且存在清晰的"模糊度梯度"。**

- **低模糊（MIX1 行为保持型重构）**：QNA + charter-lite §4.3 工作台账 + §6 测试矩阵**吸收**了 design 的验收角色——charter-lite 因此**变重**（它自己 §0.2 就声明"design 本会做的消除模糊，这里以 QNA 冻结"）。action-plan 的收口标准是**继承/转写**的、薄而干净。**此时 QNA 替代 design 真的成立。**
- **高模糊（MIX5 · SSRF/MCP 跨协议）**：design-grade 内容**泄漏进 action-plan 内联**——P1-01 把 SSRF 威胁模型（localhost/RFC1918/metadata/IPv6→blocked）写进收口标准、P2-03 把信任边界 admission pipeline 写进工作项；并把硬架构**外包给"复用 bash-core network.ts floor"**。对照 MI4：同样的威胁模型/边界/取舍，MID4 用 §3/§6.2/§7.2 **正经承载**。
- **关键洞察**：**charter-lite 的硬闸（§1.2 全部 QNA 必须 frozen，否则回退完整 charter+design）本质是一个"design 必要性探测器"**。它自己的 §8.5 也写：模糊超出 QNA 承载 → 不该用 charter-lite。MIX5 其实**已越界**（安全信任边界），按规则本该触发 design，结果 design 工作散落进了 action-plan——这正是 charter-lite 想防、却在高模糊处防不住的失败模式。

> **所以 charter-lite 不是"证明 design 没用"，而是"证明 design 在低模糊时可省、在高模糊时省不掉（省了就漏进 action-plan）"。**

## 6. 证据 C：design.md 章节利用率审计（承重 vs 仪式）

| 节 | 5 份评级 | 裁定 |
|----|----------|------|
| §1.1 术语对齐 | LB×5 | **核心**（做真实消歧，如 RH2 禁掉不存在的 `tool_use_stop` 枚举）|
| §3 架构边界 | LB×4 | **核心**（解耦/聚合点 → action-plan 新建文件清单）|
| §5 in/out-scope | LB×5 | 承重 |
| §7 验收清单 | LB×5 | **核心**（唯一产出逐功能可验证收口目标 + 待改代码行）|
| §8 仓内代码锚 | LB×5 | **核心**（file:line 借鉴/反例，action-plan 实际 grep）|
| §6 tradeoff | LB×4 | 承重 |
| §2 定位+矩阵 | 多数 THIN | 可瘦身 |
| **§4 三方参考** | **多数腐烂**（mini-agent 列空/N/A）| **该砍/降级**：命名三件套（mini-agent/codex/claude-code）已**过时**，真实参考是 codex/claude-code/cf-agents/gemini |
| §9 QNA 登记 | 半指针半新生 | **降级**：只登记"本文新生决策"，其余指向 register（杜绝与 qna 重复）|
| **§10 Value Verdict** | **CE×4，缺席×1** | **该砍**：自评 4.5–5 的仪式，下游不消费 |

**design.md 的不可替代核心 = §7 + §3 + §1.1 + §8**（charter/qna/reference-anchor/action-plan 都不产这四样）。**最该砍/降级 = §4（外部参考腐烂）、§10（自评仪式）、§9（与 qna 重复）。**

## 7. 推荐：refocus，而非保留或废除

### 7.1 把 design.md 砍到核心（落实 owner "太虚"的判断）
1. **删 §10 Value Verdict**（仪式，下游不消费）。
2. **§4 三方参考 → 降级 + 去陈旧化**：① 把外部深度对比**委派给 reference-anchor 文档**（design 不重做）；② design 内只留一句"gap-vs-当前 + 借鉴指针"，并把命名三件套修正为"可选参考引擎（codex/claude-code/cf-agents/gemini + 内部 precedent）"。**这一刀直接消解 owner"design≈外部参考"的负面观感——把弱的部分搬走，强的 §7+§3 才显出来。**
3. **§9 QNA → 降级为"只登记本文新生决策 + 一行指向 register"**：owner-冻结的决策一律以 qna register 为唯一真源，design 不再镜像。
4. **保留并强化核心**：§7（验收）、§3（边界）、§1.1（术语）、§8（仓内锚）。

### 7.2 design 可以承担的"其他工作"（potential）
- **把 §7 升级为"验收格栅（acceptance lattice）"**：`功能 F → 一句话收口目标 → Test-ID` 的三联映射（MCD3↔MC4 已自发这么做，且 action-plan 与测试套件**双双消费**）。这是 design **唯一能产、且下游全要**的东西——应明确为 design 的**首要交付物**。
- **§3 升级为"落点结构契约"**：解耦/聚合点直接以"将生成的新建文件清单"形式写出，让 action-plan 的新建文件表 = design §3 的机械展开。

### 7.3 design 应在 action-plan 前完成什么
**必须完成（不可下放给 action-plan）**：① 验收格栅（§7）；② 架构边界/落点结构（§3）；③ 术语对齐（§1.1）；④ 仓内借鉴/反例锚（§8）。
**不应由 design 做（委派出去）**：外部参考深析（→ reference-anchor）、决策冻结（→ qna register）、自评打分（删）。

### 7.4 把 design 改为条件触发（统一 charter-lite 与 design 的关系）
把 charter-lite 隐含的硬闸**显式化为"design 必要性测试"**——满足**任一**即需要 design（否则 charter-lite + qna 足矣）：
1. 新增对外 contract surface；
2. 新增架构接缝（解耦/聚合点）；
3. 跨 worker 不变量；
4. 验收条件是"多字段/非显然"的（一两句 QNA 答不清）；
5. **涉及安全信任边界**（MIX5 本该被这条拦下）。

> 这条测试同时**validate 了 charter-lite**（低模糊确实可跳 design）**又 bound 了它**（高模糊跳 design = 把 design 工作漏进 action-plan）。

## 8. design 与 action-plan 应如何产生**不同**的价值

| 维度 | design（规格层） | action-plan（执行层） |
|------|------------------|------------------------|
| 回答 | 完工长什么样 + 接缝在哪 | 怎么做 + 何时 + 何序 + 怎么测 |
| 稳定性 | 稳定（改它=改"完工定义"）| 易变（改它=改"实现顺序"）|
| 产物 | §7 验收格栅 + §3 落点结构 | phase 序列 + 文件级工作 + 测试命令 + 执行日志 |
| 与对方关系 | action-plan 逐字**消费**它 | 可**推翻/细化** design（并回标）|
| 接缝判别 | 改完工标准/接缝 → 动 design | 改实现顺序 → 动 action-plan |

**一句话**：design 给"不变的可验收规格"，action-plan 给"可变的有序执行"——二者**正交**，不是"详略不同的同一份东西"。owner 觉得 design 多余，正因为现行 design.md 把大量篇幅花在 §4/§9/§10（与 qna/reference-anchor 重叠或纯仪式），**把正交价值（§7+§3）淹没在重叠价值里**。砍掉重叠，正交价值自现。

## 9. 一句话结论与给 owner 的决策问题

**一句话**：design 不是"定位 reference anchor"（那是它最该砍的 §4），也不弱于 qna（qna 只赢在决策冻结）——design 的**不可替代真身**是"把决策翻译成**可验证验收格栅（§7）+ 架构落点结构（§3）**"的规格层；现行 design.md 的"虚"来自 §4/§9/§10 的重叠与仪式。建议**refocus 到核心 + 条件触发**，而非保留或废除；charter-lite 是合法的"低模糊免 design"通道，但需用"design 必要性测试"把高模糊（尤其安全边界）挡回 design。

**3 个决策问题**：
1. **是否按 §7.1 refocus design.md**（删 §10、§4 降级委派给 reference-anchor、§9 降级为指针、强化 §7+§3+§1.1+§8）？
2. **是否把 design 改为条件触发**（§7.4 的 5 条"design 必要性测试"决定走 design 还是 charter-lite），把 charter-lite 正式纳入"design 的轻量替代"而非"反 design"？
3. **是否把"验收格栅（F→收口目标→Test-ID）"立为 design 的首要交付物**，并要求 action-plan 与测试套件都引用它？

---

## 附录 A · design.md 章节裁定速查

| 节 | 裁定 | 动作 |
|----|------|------|
| §1.1 术语 / §3 边界 / §7 验收 / §8 仓内锚 | **不可替代核心** | 保留 + 强化（§7→验收格栅，§3→落点结构）|
| §5 scope / §6 tradeoff / §0 背景 | 承重 | 保留 |
| §2 定位+矩阵 | 多数 thin | 瘦身 |
| §4 三方参考 | 腐烂 | 委派 reference-anchor + 去陈旧化（codex/cc/cf-agents/gemini）|
| §9 QNA 登记 | 与 qna 重复 | 降级为"新生决策 + 指针"|
| §10 Value Verdict | 仪式 | 删 |

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-30 | Opus 4.8 | 初稿：3 路证据辨证裁定 owner 两假设 + design=规格层定位 + refocus/条件触发推荐 |
