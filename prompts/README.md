# prompts —— 驱动端剧本库（簇索引）

> **这是 mydocs 的「驱动端」**：真正喂给异构 LLM 集群、让它们用 `../templates/` 里的模板产出文档的 owner 提示词剧本（prompt 剧本）。templates 是"产出物长什么样"，prompts 是"怎么驱动 agent 去产出"。
>
> **纪律（与 templates 相反，刻意保持"松"）**：
> - **不互锁、不锁内链**：PROMPT 自由度高，且当前是人在环里手工粘贴（非自动化）。文件之间无需互锁——互锁只会在人机交互时增加成本。
> - **不过度改写**：PROMPT 够用即可，保持生料，不加多余 markdown 仪式。分簇的价值来自**目录组织 + git 追踪**，不来自格式化。
> - **簇 = 阶段关联**：每簇对应主流水线的一个位点，已隐含"驱动哪类模板"，无需文件级链接。
>
> **来源**：从 `.anote/`（owner 日常生料草稿 `1-temp` / `2-plan` / `3-exec`）周期性蒸馏而来。`.anote/` 仍是 owner 写新剧本的草稿台，本目录是受版本追踪的 curated 副本。

---

## 7 簇（按主流水线位点）

| 簇 | 阶段 / 意图 | 典型剧本 | 大致驱动的模板族 |
|----|------------|----------|------------------|
| `research/` | 取真 · 调查（规划前建立代码真值与上下文）| reference-anchor 锚定 · 现状/接口审计 · 真值勘察 | eval · assessment · truth · reference-anchor |
| `design/` | 规划 · 设计（蓝图与决策定调）| design TODO 循环 · design 审查 · qna 产出 | planning 三态 · design · qna |
| `authoring/` | 产出执行计划（把设计落成 action-plan）| action-plan TODO 循环 · `/workflows` fleet 编排 | action-plan · code-execution-log |
| `execution/` | 代码执行（按 ap 开发 + 测试 + 收口）| 全阶段串行执行 · 权限前检 · 双 todo（制作 + 审查回填）| action-plan(executing) · closure |
| `review/` | 审查 · 合并（单 / 多 reviewer / 质量评估）| review-by-opus · 多 reviewer → VF-ledger · review-eval | code-review · code-review-findings-ledger · respond |
| `closure/` | 收口 · 复盘 | 阶段 closure · 交付现状对账 | closure · eval-state-analysis · eval-retrospective |
| `diagnosis/` | 缺陷诊断（owner-test → 根因 → 修复结构）| bug 截图 + session 导出分析 | report/bug-analysis |

> 簇内文件即一条条剧本（`.md`，内容生料）。**文件名一律纯英文**（小写连字符、按"阶段-主题"自描述，不中英混杂）；文件内容保持原文生料。
