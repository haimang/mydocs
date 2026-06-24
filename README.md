# mydocs —— 协调无状态异构 LLM 集群的文档方法论

> 一套从 [nano-agent](https://github.com/) 项目生长出来、并毕业为独立资产的文档方法论。它把"无状态异构 LLM 集群最爱产的假绿与自欺"用一条可追的真相脊系统性地按住，让一群轮换的、互不记忆的模型协同完成从调查、规划、执行到审查收口的全流程开发。

## 两支柱 + 评定

| 目录 | 是什么 | 入口 |
|------|--------|------|
| **`templates/`** | **产出端**：约束"产出物长什么样"的文档模板（eval / planning / qna / design / action-plan / truth / review / closure …），机器接力、可冻结、带真相 ID 互锁 | [`templates/README.md`](templates/README.md) |
| **`prompts/`** | **驱动端**：真正喂给 agent、让它们用上面模板产出文档的 owner 提示词剧本，按主流水线位点分 7 簇；高自由度、人在环、刻意不互锁 | [`prompts/README.md`](prompts/README.md) |
| **`propositions/`** | 对整个 mydocs 体系（含两支柱）的**周期性价值评定**与再设计分析 | [`propositions/`](propositions/) |

## 双面互锁（同仓共生）

- **`prompts/` 驱动 → `templates/` 约束产出**：剧本告诉 agent 做什么、按哪个模板输出；模板约束输出物的结构与纪律。
- 两端**同处一仓、共同版本化**——这是方法论"双面互锁闭环"的物理落地。但互锁只在**支柱层**（驱动端 ↔ 产出端），**不下沉到文件级**：prompts 之间松、templates 之间锁，各按各的纪律。

## 怎么用

- **要产出某类文档** → 读 `templates/README.md` 的决策树，命中模板。
- **要驱动 agent 跑某个阶段** → 到 `prompts/` 对应簇取剧本，按需改具体路径后粘贴给模型。
- **想了解体系价值/演进** → 读 `propositions/`。

---

> 驱动端剧本的日常草稿台在 nano-agent 的 `.anote/`；`prompts/` 是其受版本追踪的 curated 蒸馏副本。
