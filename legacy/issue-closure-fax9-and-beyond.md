# Issue Closure Template — FAX9+ Gate Discipline

> Template type: `phase-closure` (FAX9 W3.4 product)
> 来源: `clients/web/docs/action-plan/web-v70/FAX9-cross-layer-correctness-and-evidence-discipline.md` §3 / §4
> 使用对象: FAX9 / FAX10+ / BNX8+ closure 起草人

---

## §0 文档结构（每个 closure 文件必含的章节）

1. **§0 状态总览** —— 维度 × 状态表（立项 / 各 phase / owner-test gate）
2. **§1 Baseline 锚定** —— 触发的 owner-test session uuid + 截图 + D1 dump 引用
3. **§2 Phase 工作清单** —— 每个 P*/W* 工作项的 `状态 + 证据` 单行
4. **§3 UF / 业务问题 collision table** —— 每个 unified finding 的处置 + commit 引用
5. **§4 自动化测试结果** —— typecheck / unit / integration / spike 命令 + 结果
6. **§5 G-A~G-F 6 gate 判定** —— 见 §1 详细规约
7. **§6 §13 helper / §12.9 边界对账** —— 沿用 FAX8 形态
8. **§7 §12.9 不做清单兑现** —— 历史不做项的诚实兑现
9. **§8 收口纪律兑现声明** —— FAX8 §8.4 7 条 + FAX9 §0.4 10 条
10. **§carry-over / handoff** —— 后续 phase 承接的项 + 责任方
11. **§10 Deferred / Carry-over ledger** —— 沿用 FAX8 §10 ID-anchored 台账
12. **§N 一句话总结** —— closure type + key gates pass/partial + critical handoffs

---

## §1 G-A ~ G-F 六道 Gate 详细规约

每个 phase closure 在 §5 必须显式判定下列 6 gate：

### G-A — Cross-Layer Contract Consistency

**判据**:
- ordering contract 在 backend writer / backend reader / frontend comparator / frontend transcript / api docs 全部一致
- 任一处 drift（comparator 优先级 vs docs 描述不符；reader SQL 与 docs ORDER BY 不符等）= G-A fail
- 自动化: `git grep "emit_seq\|global_seq\|event_seq"` 检查每个 reference 是否对齐 W1.1 frozen QnA

**判定**: ✅ PASS / ⚠ PARTIAL / ❌ FAIL（必须给出每个层的具体证据）

### G-B — Evidence Pack Discipline

**判据**:
- owner-test session 应有 raw pack 沉淀到 `.tmp/owner-test/<date>/<session_uuid>/raw/`
- helper inline verdict (W2.3/W2.4) 在 summary 顶部正常出现
- helper source-missing list (W2.5) 真实列出所有缺失 source

**判定**: ✅ PASS（≥ 1 个 owner-test session 自动 sink）/ ⚠ PARTIAL（仅手动 sink）/ ❌ FAIL

### G-C — Deploy Freshness Gate

**判据**:
- `scripts/check-deploy-freshness.mjs` 对所有 6 worker 都 ✅ dist fresh
- `deploy-preview.sh` 的 `pnpm build` guard 在 worker dir 内真实执行（RX-22）
- `/debug/workers/health.commit_marker.sha` === git HEAD short sha（W3.2）
- 不允许 SKIP_BUILD=1 + 未 build dist 的组合

**判定**: ✅ PASS / ❌ FAIL（任一 dist stale 或 commit_marker drift = FAIL）

### G-D — D1 Invariant Smoke

**判据**:
- post-deploy: `scripts/post-deploy-d1-invariant.mjs` 跑过且 exit 0
- mock session 跑通 / `last_global_seq > 0` / assistant text non-empty
- 6 worker health 6/6 + Route A 三 flag unset

**判定**: ✅ PASS / ⚠ PARTIAL（仅 health 过，invariant smoke 未跑）/ ❌ FAIL

### G-E — Multi-Model Smoke

**判据**:
- `test/spike/journey-multi-model-text-return.spike.test.mjs` 对每个注册 model（FAX9 锁定的 gemma-4 + kimi-k2.6）至少 1 个 prompt 跑通
- 每个 (model, prompt) 组合都得到 ≥ 5 chars 真实 text return
- 任一 model 0 text 输出 → alert + block deploy (防 0515-0520 llama-4-scout silent regression)
- **FAX9 closure-evening 2026-05-20 新增 sub-gate**: `test/spike/journey-fax9-curl-end-to-end.spike.test.mjs` 用 kimi-k2.6 验证 **tool-use end-to-end** 链路 — confirmation tool_input 完整 + tool.call.result 200 OK + 真实 HTTP fetch return；防 workers-ai parser 嵌套 `choices[0].delta.tool_calls` 漏读 / streaming args 碎片不累积 silent-drop (RX-30/RX-31)

**判定**: ✅ PASS / ⚠ PARTIAL（部分 model 跑通 OR tool-use sub-gate pending owner-tier auth）/ ❌ FAIL

### G-F — Owner-Test Gate ②

**判据**:
- owner 在 preview 真实复测过近一轮的 owner-test 截图矩阵
- 逐行 diff 表：baseline / 复测 / 结果（PASS / FAIL / carry-over）
- 任一行 owner-reported FAIL 必须有显式 handoff（不允许 "我修了"未经 owner 复测）

**判定**: ✅ PASS / ⚠ PARTIAL（仅部分场景复测）/ ❌ FAIL / ⏸ PENDING

---

## §2 闭环纪律（FAX8 §8.4 沿用 + FAX9 §0.4 新加）

每个 closure 在 §8 显式声明下列 10 条兑现状况：

| # | 纪律 | 兑现声明 |
|---|------|----------|
| 1 | 逐项 red→green 证据 | ✅/⚠/❌ |
| 2 | 反向收口判据 | ✅/⚠/❌ |
| 3 | closure 证据结构 = collision table 逐行带证据 | ✅/⚠/❌ |
| 4 | baseline ↔ 复测逐行 diff | ✅/⚠/❌ |
| 5 | 冷加载颜色锚定 | ✅/⚠/❌（仅 frontend phase 适用）|
| 6 | scope diff 守卫（git diff --stat 与 in-scope 一致）| ✅/⚠/❌ |
| 7 | canary 失败归因协议 | ✅/⚠/❌ |
| 8 | 跨 worker contract spike 覆盖 | ✅/⚠/❌（FAX9 新加）|
| 9 | session.do is sole buffer | ✅/⚠/❌（FAX9 新加）|
| 10 | Dev-phase 诚实收口 | ✅/⚠/❌（FAX9 新加）|

---

## §3 ✅ Footnote 四元组规约（FAX9 新加）

任何 ✅ 标记在 closure 中必须 footnote 四元组：

```
| P1-01 UF-1.B phantom bootstrap | ✅ | (commit `abc1234` + D1 query `SELECT * FROM ...` + spike `journey-foo.spike.test.mjs` + 运行时间 `2026-MM-DD HH:MM:SS UTC`) |
```

不允许仅 file:line 引用。如果某 ✅ 因为 dev-phase 时间约束无法取四元组，必须显式归类为 5 态之一（见 §4）。

---

## §4 诚实收口 5 态（FAX9 W5 / 纪律 #10）

每个 ✅ 必须显式归类为下列 5 态之一：

1. **verified** — closure 时刻 D1 + spike + journey evidence 全有，commit + query + spike name + run time 四元组完整
2. **observed-OK-at-closure** — closure 时刻 snapshot 显示正常，但未做 long-run soak（dev-phase 允许）
3. **partial** — A 级证据不全；显式列出缺什么 + handoff 给谁
4. **未观察** — closure 时刻没机会触发（如 long-outage / multi-tab race 等无法主动 reproduce 的场景）；显式记录"未观察 due to..."
5. **deferred** — carry-over 到后续 phase；显式列出后续承接位置

不允许任何 ✅ 无归类。
