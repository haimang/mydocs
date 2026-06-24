# Nano-Agent Bug 分析报告模板（owner-test → bug-report）

> 批次: `{BATCH_ID}`（例 `0524-batch-01`）
> 调查时间: `{DATE}`
> 调查者: `{ANALYST}`（例 `Opus 4.7`）
> 文档状态: `draft | reviewed | superseded`
> 部署基线: `后端 6-worker + 前端 clients/web 于 commit {SHA}（{ENV}，{FRONTEND_URL} + {BACKEND_URL}，health {N}/6 live、seams unset）`
>
> 截图对象（`.tmp/bug-report/{BATCH_ID}/`）:
> - `{fact-NN-xxx.png}` — `{一句话现象}`
> - `{bug-NN-xxx.png}` — `{一句话现象}`
>
> D1 取证（`scripts/message-debug-helper.mjs <session_uuid> --remote`）:
> - `{老/新聊天 session_uuid}` → `debug-{old|new}-session/`（标注哪个是本批主体）
>
> 代码调查: `{N}` 路 sub-agent 并行 / 单线；全部结论必须 `file:line` grounded。

> **使用说明（删除本块再发布）**：本模板是 owner-test 回来后、动手写 charter/action-plan **之前**的诊断产物。
> 铁律：先有 **D1 live 真相**（§1–§2）才有结论；先做**业务簇归类**（§3）再逐簇深挖（§4）；
> §6–§10 是本模板的灵魂（架构定性 / DAG / 测试归责 / 执行顺序 / 测试方案），不可省。
> 末尾「附录 Z 原则清单」是**刻死的长期记忆**，每次写报告前通读一遍，违反即返工。

---

## 0. 一句话 Verdict + owner 最关心的问题

> 先给 verdict，再列 owner 本批最关心的 1–3 个问题（用 owner 的原话或直接转述）。
> verdict 要点名：这是几个业务簇？有没有 **release-blocker**？最致命的是哪个？

- **一句话结论**：`{N 个 bug 实为 M 个业务簇；其中 {X} 是 release-blocker；最致命 = {…}}`
- **结论等级**：`healthy | fixable | changes-required | release-blocked`
- **owner 最关心的问题**：
  1. `{OWNER_Q1}`
  2. `{OWNER_Q2}`
  3. `{OWNER_Q3}`

| 簇 | 主题 | 严重度 | 责任层 | 截图 |
|----|------|--------|--------|------|
| **A** | `{…}` | `CRITICAL(blocker) / HIGH / MEDIUM / LOW` | `后端 / 前端 / 前后端` | `{bug-NN}` |
| **B** | `{…}` | … | … | … |

> 若存在贯穿多簇的**跨簇基础设施缺陷**（例：某 ledger 字段全 NULL），在此单列一行点名。

---

## 1. 调查方法与证据基线

> 只写事实，不写结论。明确：部署基线、看了哪些截图、导了哪些 session、跑了哪些命令、用了哪些 sub-agent。

- **部署基线核对**：`{commit / health 6/6 / commit_marker 对齐 / seams unset}`
- **截图**：`{清单}`
- **D1 取证命令**：`node scripts/message-debug-helper.mjs {uuid} --out .tmp/bug-report/{BATCH_ID}/debug-…/ --remote`
- **关键取证表**：标出本批**最重要的一张原始表**（常是 `llm_request_log.messages_summary` / `conversation_messages` / `audit_log`）。
- **代码调查**：`{sub-agent 数量与分工，每路一个业务簇}`

---

## 2. 截图真相 → D1 / 证据 对照

> 这是整篇报告的**证据底座**。每行：owner 看到的 → D1 实证 → 指向哪个簇。
> 不允许「我觉得」；每条 D1 实证必须能从 `debug-*/` 复现。

| 截图 | owner 看到的 | D1 / 代码实证 | 指向簇 |
|------|-------------|---------------|--------|
| `{fact/bug-NN}` | `{现象}` | `{D1 字段/行 + helper invariant 结论}` | `{A/B/…}` |

> 若本批根因藏在「发给 LLM 的实际 messages[]」「seq 顺序」「lifecycle 状态机」等不可肉眼看的地方，
> 把**关键原始片段**（如 `messages_summary` 摘录、emit_seq vs global_seq 对照）直接贴进来。

---

## 3. Bug 平铺与业务簇归类

> 先把所有 bug **平铺**，再**合并同类、归入业务簇**。一个业务簇 = 一个根因家族，不是按截图编号。
> 归类原则：按「同一根因 / 同一代码缝隙」聚合，跨截图也要并簇（横向思维）。

| 原始 bug | 现象 | 归入簇 | 是否同根因 |
|----------|------|--------|-----------|
| `{bug-NN}` | `{…}` | `{A}` | `{是/否，为何}` |

---

## 4. 逐业务簇深度分析（含代码级证据）

> 每个簇用下面的固定小结构。**root-cause 必须 file:line**，且区分「真元凶」与「被排除的疑似元凶」。

### 4.A 簇 A — `{标题}` 【`{严重度}`】

- **现象与 D1 铁证**：`{owner 看到的 + 取证片段}`
- **Root cause（file:line）**：`{在哪个文件哪一行，哪个函数；几个独立缺陷分别列}`
- **为何只在 `{某 provider/路径/时序}` 触发**：`{说明分叉点——例：严格 adapter vs 宽松网关}`
- **守卫为何没拦**：`{现有 invariant/测试为何放过——常是没有该规则 or 假夹具}`
- **被排除项**：`{看过但确认不是元凶的路径，避免误导}`
- **修复建议（落点 seam）**：`{具体改哪个文件/函数；首选热修 + 长治落点}`

> （B、C… 重复同结构。）

---

## 5. 横向交叉分析（本批多 bug 共因）

> 把多个簇连起来：有没有一个共同根因 / 一个被反复踩的缝隙 / 一个基础设施债贯穿全批？
> 历史经验：很多批次「看似 N 个独立 bug」其实是 1 个共因 + 几个独立（0514/0515/0518）。

| 共因 / 跨簇债 | 证据 | 影响簇 |
|--------------|------|--------|
| `{…}` | `{file:line / D1}` | `{A,B,…}` |

---

## 6. 架构判定 + 「带债 hot-fix」 vs 「长治修复」（逐簇定性）

> **本节是防 FAX 复发的核心。** 判据：
> - **带债 hot-fix**：只改一个表面调用点、绕过真正的契约/真相缝隙 → 换个入口/provider 又复发。
> - **长治修复**：落在 canonical 缝隙（normalize / 契约 wire-shape / 真相派生 / 单一权威决策点）并配契约守卫。

| 簇 | 是否架构层 | 初版修法定性 | **裁定后的长治落点（seam）** |
|----|-----------|-------------|------------------------------|
| `{A}` | `是/半/否` | `{带债 hot-fix / 可接受 / 低债}` | `{canonical 缝隙 + 契约守卫}` |

> 结论：点名哪几个是**架构层、必须落 canonical 缝隙否则就是 FAX 式带债补丁**；
> 哪几个是半架构（补契约而非绕过）；哪几个是纯交付/展示（低债）。
> 若多个簇的长治落点收敛到同一个 frozen design（例 MID7），明确指出「本批是该 design 的真实 driver」。

---

## 7. 完整 DAG 修复结构（前端修什么 / 后端修什么 / 依赖边）

> 把修复拆成**带层标签的节点**，画出依赖边与执行波次。**铁律：后端真相先落+部署+验证，再修前端。**

### 7.1 节点（按层划清）
- **后端节点（workers/）**：`BE-x {一句话}` — 簇 `{…}`【标 P0 blocker 者】
- **前端节点（clients/web/）**：`FE-x {一句话}` — 簇 `{…}`

### 7.2 依赖边（`→` = 依赖、必须先完成且**部署**）
```
{BE-A} ─────────────────►（无前端依赖：后端修好即通）
{BE-C} ──► {FE-C}        （前端展示/自愈依赖后端真相先落，否则又变 band-aid）
{FE-x} ──► {BE-x}        （注明可断边的二选一方案）
```

### 7.3 波次（anti-FAX：杜绝「前端迁就坏后端」）
| 波次 | 内容 | 部署 + 验证门 |
|------|------|--------------|
| **Wave 0（后端）** | `{blocker 优先 + 其余后端}` | 后端 unit 全绿 → `deploy-preview.sh` 6-worker → health 6/6 + commit_marker → **live spike 验证** |
| **Wave 1（前端，针对已部署后端）** | `{FE 节点}` | short 全绿（**真实 shape 夹具**）→ pages deploy → journey 验证 |
| **Wave 2（回归 + 台账）** | `{回填 live-evidence-ledger / retire 假夹具 / owner-test 复测}` | 复测 P0/P1 |

> blocker 单独成最小热修 PR 先行止血。

---

## 8. 测试体系归责（为什么没发现 + 该不该由前端体系负责）

> **这是几乎每一批都要回答的问题**（0513-b03 §4/§6、0514 §7、0515 §8、0518-b02 §4/§5、0518-b03 §2.6、0524 §12）。
> 不许甩锅，也不许过度自责——按下面三类裁定。

### 8.1 逐簇归责（谁的责任 / 该哪层抓 / 为何漏 + 证据）
| 簇 | 责任方 | 本应由哪层抓 | 为何漏（file 证据） |
|----|--------|-------------|---------------------|
| `{A}` | `后端/前端` | `short / spike(live) / journey / 后端 unit / owner-test` | `{假夹具 / 孤儿 / 缺断言 / 无 live / 协议真相}` |

### 8.2 三类裁定
- **(i) 确定性前端真相 → short 必须抓，不该甩给 owner-test**：`{列簇}`。漏因常是体系三老毛病：**①合成夹具与真实 wire-shape 漂移（假绿）②孤儿组件无消费测试 ③缺关键断言**。
- **(ii) 契约/集成真相（前端 client × 真后端 × 真模型/重连）→ spike/contract 层应抓，是前端的 harness 责任但需 live**：`{列簇}`。
- **(iii) 合法 live-only / 后端协议真相 → owner-test 或后端 unit**：`{列簇}`。
- **一句话**：本批 `{哪些}` 前端体系应负责且本应抓到（旧债兑现）；`{哪些}` 合法属后端/owner-test。**owner-test 不该兜底本可确定性测试的缺口**。

---

## 9. 修复执行顺序确认

> 以 §7 DAG 波次为准。**架构层 P0 先行**（历史教训：初版优先级常把架构 P0 埋在表面修复之后，必须重排——见 0514 §15）。

1. **P0 / Wave-0 起步**：`{blocker，按 §6 落 canonical 缝隙，不做带债补丁}`。
2. **Wave-0 其余后端并行** → 部署 → live 验证。
3. **Wave-1 前端**（针对已部署后端，标出无依赖可最早做的节点）→ short 真实夹具 → 部署 → journey。
4. **Wave-2**：回填台账、retire 假夹具、owner-test 复测。

---

## 10. 修复后测试方案（每簇映射到层 + 保真硬要求）

> **保真硬要求（防假绿）**：① 每个修复在「本应抓到它的那一层」补 test；② **夹具必须是真实 wire-shape**（禁止顶层 hoist 式假夹具）；③ live-executed 证据落 `clients/web/docs/eval/.../live-evidence-ledger.md`，anchor-covered 与 live-executed **双口径分列**。

| 簇 | short（jsdom 确定性） | spike（前端 client × 真后端 live） | journey（preview） | 后端 unit | owner-test |
|----|----------------------|-----------------------------------|--------------------|-----------|-----------|
| `{A}` | … | `{live 硬门?}` | … | … | … |

> 点名哪些簇的 **live spike 是验收硬门**（确定性单测之外唯一能证明「真后端真模型」修好的层）；
> 点名本批最重要的**测试体系欠债清偿**（例：retire 某个假夹具 + 补真实 shape 夹具）。

---

## 11. 诚实边界 / 重大更正声明

> 若复盘中发现**自己之前判断错了 / owner 是对的**，在此**先认错**（0518-b02 §0、0518-b03 §2.5 的文化）。
> 同时声明本报告的诚实边界：哪些是 D1 实证、哪些是代码推断、哪些是 live-only 未证。

- **更正**：`{有则写，无则注明「本批无需更正」}`
- **诚实边界**：`{区分 实证 / 推断 / 待 live；不 hedge，待证项明确标 owner-test 靶}`

---

## 12. owner 问题逐条回答

> 把 §0 列出的 owner 问题逐条直答，每条带证据指针。

1. **`{OWNER_Q1}`** → `{直答 + 证据}`

---

## 13. 与历史阶段的关系 / carry-over

> 本批根因与哪个 charter / 阶段 / 已知 KI/WK / frozen design 相关？是不是某个 deferred 风险的兑现？
> 哪些不在本批范围（明确 OOS），承接到哪里。

| 项 | 关系 | 承接位置 |
|----|------|----------|
| `{…}` | `{根因属 / 回归自 / deferred 兑现}` | `{charter / KI / design}` |

---

## 14. 附录:复核命令 + 取证产物清单

> owner 可直接 paste 的 wrangler / curl / helper 命令；以及本批产物清单。

```bash
# (1) session 真实状态
node scripts/message-debug-helper.mjs {uuid} --remote
# (2) {本批关键复核点}
```

- 取证产物：`debug-{old|new}-session/`（summary.md + raw/*.json + H1-H11）、本报告、`{关键摘录}`。

---
---

# 附录 Z — FAX5–FAX9 与历史阶段的经验、教训（**刻死的长期原则清单**）

> 这一节不是 placeholder，是**写进模板的硬记忆**。每次写 bug 分析、定优先级、设计修复、评估测试时，逐条对照。
> 来源：FAX5–FAX9 血债阶段 + 0513–0524 全部 owner-test 批次 + FEX 审查 + testing-state 调查的真实代价。

## Z.1 证据纪律（先有真相，才有结论）
1. **D1 是唯一真相**。任何 yes/no 必须有 `message-debug-helper` live dump 佐证；**不许「大概率 YES」式 hedging**。tool-use 链路的每个 anchor 必须逐一 verify。
2. **先认错文化**。owner 的体感往往是对的；与 D1 冲突时，先怀疑自己的结论，不要怀疑 owner（0518-b02「先认错」、0518-b03「重大更正：owner 是对的」）。
3. **观测不能在关键事件上是盲的**。如果某个根因「无法从现有 inspection/日志看到」，那是观测缺口本身要修（0514「关键事件盲」、0515「inspection 全面没用」）。
4. **截图 → D1 → 代码** 三段必须闭环；缺任一段的结论不成立。

## Z.2 执行顺序（架构先行，后端先落）
5. **架构层 P0 先行**。初版凭直觉排的优先级，几乎总把架构缺陷埋在表面修复之后；**必须重排，架构层摆最前**（0514 §15「替代 §8，把架构层 P0 摆在前面」）。
6. **后端真相先落 + 部署 + 验证，再修前端**。**禁止用前端 workaround 去糊一个未修好的后端**——这会制造部署竞态与互相迁就，是 FAX 反模式的核心。
7. **blocker 单独最小热修先行止血**，但热修也要落在正确缝隙（见 Z.3）。
8. **stale dist 必死**。部署前 `pnpm build`（FAX8 batch-02 血案：deploy 了 4 小时前的 dist，D1 全程 `last_global_seq=0`）；deploy 后核 `commit_marker.sha == HEAD`。

## Z.3 修复定性（hot-fix 不许带债）
9. **hot-fix 必须落在 canonical 缝隙**，否则换个入口/provider 必复发（0524：runner 单点 coalesce 若绕过 normalize 层 + invariant 就是带债）。能收敛到 frozen design（如 MID7）的，就落在那里。
10. **问题常在「叠加方式」而非单层子目标**。每一层都「对」，但耦合/前置/自循环的叠加是错的（0520-b04「问题不在每层子目标，而在叠加方式」）。修复要拆耦合，不是再加一层。
11. **owner 心智模型 vs 真实架构 mismatch 要显式对账**（0514「tmux 体验 vs per-用户 DO」）。先对齐心智模型，再谈修复。
12. **回归要专门防**。有机会关掉一个 WK/KI 时要真关到底，否则它会以回归形式回来（0518-b03：FA-9 有机会关 WK-159 却没关）。

## Z.4 测试保真（假绿是头号敌人）
13. **假绿是头号敌人**：**合成夹具与真实 wire-shape 漂移 → 测试绿、生产挂**。教科书案例：`transcript-ordering.spec.ts` 把 `emit_seq` 放在 item 顶层，而真后端只在 `body.emit_seq`，于是绿测放过了生产乱序。**夹具必须是真实 wire-shape**。
14. **「前端不许 mock」原则不得稀释**。一旦发现某层在用 mock/合成数据冒充真实后端，那层等于不存在（0518-b03「前端不许 mock 原则何时被稀释」）。
15. **live spike 必须真 live + 带最基本守卫**。`skip-when-E2E` 的 no-op spike、只断合成 fixture 形状的 capture spike，都是假 live，等于零覆盖（FEX2、0518-b02「我的 live spike 连最基本守卫都没做到」）。**关键修复的 live spike 是验收硬门**。
16. **孤儿组件 = 未交付**。建了组件却无任何 journey/short 消费它，就是孤儿 prework，迟早成 bug（C1 组件孤儿；0524 工具卡分组）。
17. **owner-test 不兜底本可确定性测试的缺口**。能用 jsdom short 确定性抓的（顺序、状态一致、usage 存活、分组），不许甩给 owner-test；否则就是把假绿循环再走一遍。
18. **每个修复反哺 anchor**：在「本应抓到它的那层」补 test，并把 live-executed 证据回填 `live-evidence-ledger`，把 live 列从 ~0 真正推起来。

## Z.5 收口诚实（计数不等于价值）
19. **「已 close」≠ 价值交付**。用「测试计数通过」冒充「设计价值交付」是 FAX/FEX 反复出现的病（0515「已 close 的 BSS 一个用户问题都没改善」、0518-b02「FAX5 没实现任何价值」、FEX「closure 用计数冒充交付」）。closure 必须名实相符。
20. **区分 `fixed`（有代码+测试）vs `verified-still-open`（仅确认现状）**，不得混淆；劣质半修不许标 fixed。
21. **anchor-covered vs live-executed 双口径**：UI 能力锚覆盖 ≠ 真 live 跑过；台账两列分列，不得用「9→0」式 overclaim。
22. **deferred 必须三分类（A/B/C）且每项有承接位置**；owner-test 项未复测的标 ⏸，不伪宣称已 live。
23. **修了好几轮、老问题没解决又冒新 bug**——若出现这个体感，停下来做横向共因分析（§5）和架构定性（§6），不要再加补丁（0518-b01 §4）。

> **一句话刻死**：先用 D1 证伪自己 → 架构层先修、后端先落 → hot-fix 落在 canonical 缝隙 → 用真实 wire-shape 的测试在「本该抓到的那层」补上 → 名实相符地收口。违反其一，就是在重走 FAX5–FAX9 的血债路。
