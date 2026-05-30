# 代码 megafile 顶部 docblock 模板(MCX1 纪律)

> 适用对象:`workers/**/src/**/*.ts` 中接近或承载 megafile 阈值的 owner 文件(主文件 ~280 行 / sibling ~350 行)
> 来源:`docs/eval/more-capabilities/megafile-after-MC4-analysis-by-opus.md` §2.2
> 配套 lint:`scripts/check-comment-phase-tag-duplication.mjs`

---

## 0. 立场

`session-truth/messages.ts` 在 MCX1 之前的状态:同一 phase tag(如 `FAX8 P3-05`)在文件内多次出现,每次重复完整事故复盘段落。读者要在 1100 行里 grep 多次才能找到真值;新人完全无法快速判断"为什么这段代码长这样"。

本模板的目标是把"事故复盘 / 不变量 / 公共 API 表 / 跨文件接缝"集中到**顶部 docblock 一次**,函数内部仅保留 1-2 行 cross-ref(`// see top docblock §X`),不再重复完整 narrative。

---

## 1. 适用条件

| 条件 | 是否适用本模板 |
|------|----------------|
| owner 文件 ≥ 280 行 | ✅ 必须套用 |
| barrel re-export 文件 ≤ 60 行 | ❌ 不需要 docblock,只需 1 行 `// barrel for …` |
| 跨多个 capability seam 的 facade(filesystem-core/index.ts 拆分后) | ✅ 必须套用 |
| 单一 RPC group 内部 sibling(rpc/artifact.ts 等) | ✅ 推荐套用 |
| 历史 phase narrative ≥ 3 处的旧文件 | ✅ 必须套用 + 收敛 |

---

## 2. 完整范例

```ts
/**
 * {Module 一句话职责}
 *
 * Owner: `{worker}` · Public API surface in §3.
 *
 * §1 · 历史 phase narrative(按 tag 收敛)
 * ──────────────────────────────────────
 *
 * - **FAX8 P3-05 (UF-10)** — tool.call.result OR-shaped dedup probe.
 *   Pre-fix: AND-shape probe required BOTH `request_uuid` AND
 *   `tool_call_id` non-null on adapter / kernel-runner emit paths;
 *   evidence session `1aaa218d` showed disjoint identifier keys per
 *   path → 4 result rows persisted for 2 logical calls. Post-fix: OR
 *   match on either key, scoped by tool_name. Living in
 *   `messages-forwarded.ts::appendForwardedFrame`.
 *
 * - **FAX9 W1.2-fix-3** — llm.delta `(turn_uuid, emit_seq)` dedup probe.
 *   Pre-fix: every delta written twice (evidence session `22121900`).
 *   Post-fix: belt-and-suspenders skip second INSERT. Living in
 *   `messages-stream.ts::appendStreamEvent` + `messages-forwarded.ts`.
 *
 * - **0515 batch-02 P1-01 (RC-2)** — turn.begin idempotency shared probe.
 *   Both local-emit (`appendStreamEvent`) and forwarded
 *   (`appendForwardedFrame`) call `selectExistingTurnBegin`.
 *
 * - **MIX7 closure hardening** — local-emit `turn.end` MUST trigger
 *   canonical assistant.message synthesis (parity with forwarded sink).
 *
 * §2 · 不变量(MCX1 保护)
 * ─────────────────────
 *
 * 1. Public API 列表(see §3)不允许改名/改签名 — 任何漂移触发
 *    `scripts/check-rpc-method-surface-freeze.mjs`。
 * 2. dedup probe 必须在 `db.batch` 之前执行;atomicity 由 batch 保证。
 * 3. emit_seq 序由调用方负责;本模块不重排。
 *
 * §3 · Public API
 * ───────────────
 *
 * - `appendUserMessage(db, input)` — see messages-append.ts
 * - `appendStreamEvent(db, input)` — see messages-stream.ts
 * - `appendForwardedFrame(db, input)` — see messages-forwarded.ts
 * - `appendSpineEvent(db, input)` — see messages-spine.ts
 * - `captureContextSnapshot(db, input)` — see messages-context.ts
 *
 * §4 · 跨文件接缝
 * ──────────────
 *
 * - 上游:`workers/orchestrator-core/src/user-do/runtime.ts` 调
 *   `appendForwardedFrame`(forwarded path)
 * - 上游:`workers/orchestrator-core/src/user-do/session-flow/start.ts`
 *   调 `appendUserMessage`(local-emit path)
 * - 下游:`workers/orchestrator-core/src/control-plane/context-control-plane.ts`
 *   调 `captureContextSnapshot`(compact commit path)
 */
```

---

## 3. 函数内 in-line 注释纪律

| 旧风格(MCX1 之前) | 新风格(MCX1 起) |
|--------------------|--------------------|
| `// FAX8 P3-05 (UF-10) — tool.call.result dedup probe.\n  // Pre-fix: AND-shape probe required BOTH ...\n  // Post-fix: OR match on either key.` 在 4 处函数重复 | `// FAX8 P3-05 — see top docblock §1` 1 行 cross-ref |
| `// FAX9 W1.2-fix-3 (post-diagnostic session 22121900): llm.delta dedup probe ...` 3 行复述 | `// FAX9 W1.2 — see top docblock §1` 1 行 cross-ref |
| `// 0515 batch-02 P1-01 (RC-2) — turn.begin idempotency on the local-emit path. The forwarded-frame path was already covered by 0515 batch-01 P1-03 ...` 多行重复 | `// 0515 batch-02 P1-01 — see top docblock §1` 1 行 cross-ref |

---

## 4. 例外:必须保留 in-place 完整 narrative 的情况

| 场景 | 理由 |
|------|------|
| interface 字段的 jsdoc(如 `OrchestrationDeps.probeCompactRequired` 的 HP3-D2 说明) | jsdoc 对应 LSP hover 文档,必须独立可读 |
| 函数局部 invariant 的 1-2 行 narrative | 不属于 phase 复盘,属于代码"为什么这样写"的 why |
| MCX-qna ruling 引用(`// MCD3-Q7 ruling: R2 失败保留 inline summary_text`) | 这是 owner 裁决引用,不是事故复盘;但仍要 tag 一致 |

---

## 5. 自检 checklist

- [ ] 文件顶部 docblock 包含 §1 phase narrative / §2 invariants / §3 public API / §4 cross-seam 四节
- [ ] 同一 phase tag 在文件内出现 ≤ 2 次(jsdoc 例外)
- [ ] `node scripts/check-comment-phase-tag-duplication.mjs` 对本文件 0 warn
- [ ] 函数内 narrative 不重复(`// see top docblock §X` 替代)
- [ ] Public API 表与实际 export 一致(`scripts/check-rpc-method-surface-freeze.mjs` baseline 不漂移)
