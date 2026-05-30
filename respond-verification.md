## 附录 {X}. 代码碰撞核实矩阵（{DATE} · {N} 路并行 sub-agent · 仅读真实代码）

> **用法（respond- 附加章节，append-only）**：
> 1. **宿主**：任何带 finding / 台账 ID 的 `design` / `eval`（盘点、缺口台账、reference-anchor 等）。
> 2. **挂载位置**：append 到宿主末尾，作 `## 附录 {X}`。不改写宿主主体。
> 3. **谁写 / 何时**：由**作者本人**（经扇出 sub-agent）在 **冻结前** 做的对抗性自检；通常是 `draft → frozen` 之间的一次硬化 bump。
> 4. **核实纪律（最硬）**：**只读真实代码、不转抄 closure / docs**——仅读 `workers/**/src`、`clients/web/src`、`migrations`、`test`，**不读 `docs/`、不读 `.tmp`**。
> 5. **回链 item-ID**：每一行键到宿主台账 ID（`A1..An / B1..Bn / 轴 A–N / TR-1..10`）。
> 6. **取证**：每行必带 `file:line` 证据；**凭记忆 / closure 与代码不符的，必须显式标 `修正`**；net-effect 即使"未改变"也要声明。
> 7. **置信分层**：`HEAD 实测（grep/read，高）` / `context/ 锚（sub-agent 报告 ±数行，落地前逐条 re-pin）` / `web（官方 high / vendor-blog low，须二次核验）`。

> 方法：`{N}` 路 Explore agent 碰撞 `{CODE_DIRS}`。
> 状态枚举：`ACTIVE`（债仍真实存在）/ `STALE`（已实现或描述过时·被超越）/ `PARTIAL`（部分）。

### {X}.1 碰撞核实矩阵

| 项（host-ID） | 核实状态 | file:line 证据 | 对台账的影响（含 **修正**） |
|---------------|----------|-----------------|------------------------------|
| `A1` | `ACTIVE` | `{FILE_LINE}` | `{IMPACT}` |
| `A2` | `STALE（已 executed）` | `{FILE_LINE}` | `**修正**：{凭记忆判断与代码不符之处}` |
| `B5` | `PARTIAL` | `{FILE_LINE}` | `{从 must-close 改 must-decide …}` |

### {X}.2 核实结论

- `{N}` 项全部碰撞当前代码；**`{K}` 处修正**（凭记忆 / closure 与代码不符）。
- **净影响**：`{host scope 是否改变；哪些 must-close → must-decide；in-scope 是否不变}`。

### {X}.3 核验记录（substrate / reference 变体，可选）

- ✅ **HEAD（实测 grep/read）**：`{ANCHOR}`（file:line）— 实测命中
- ⏳ **context/ 锚为 sub-agent 报告（±数行）**，action-plan 落地前逐条 re-pin：`{ANCHOR}`

### {X}.4 技术路线适配审查（substrate-fit 变体，可选）

| TR | 公理 | HEAD 锚（本会话实测） | 作废 / 确认 |
|----|------|------------------------|-------------|
| `TR-1` | `{AXIOM}` | `{HEAD_ANCHOR}` | `确认 / 作废` |

被剔除 / 重映射清单（每项给 nano 替代）：

| 原机制 | 为什么无效 / 须重映射 | nano 替代 |
|--------|------------------------|-----------|
| `{ORIGINAL}` | `{WHY}` | `{NANO_REPLACEMENT}` |
