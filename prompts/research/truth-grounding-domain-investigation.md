我们将根据 clients/truth-grounding/backend-assessment-index.md 的要求，进入到后端真相的 第6簇 内容的调查
我们本次调查的目标为: D17 — OAuth / 连接 / 同意（OAuth / Connections / Consent）
调查结束后，分析报告的输出路径为: clients/truth-grounding/

---

在每次调查的时候，你都会遵循下面的原则

1. 理解当前调查目标的全部背景，然后根据调查内容，将整个调查面切分为几个内聚的调查方向。然后你会为每个调查方向，定制 PROMPT，并发起 sub-agent 对该调查方向进详细的代码检索
2. 你会严格使用我规定的输出目录进行内容的组织
3. 你的调查必须使用 file:line 级别的精度，进行 reference-anchor 的锚定
4. 在输出完成后，你会对文档的内容进行核验，校对，以及断点盲点的核查分析，并对找到的问题进行修正

---

目录结构:

1. 调查目标主体的介绍，调查的原因
2. 主要负责的 worker 以及目标在 nano-agent 中的价值地位
3. 目标的主体逻辑结构的树状代码依赖结构
4a. nacp 协议下，对当前分析目标在 8-worker 拓扑结构的授权，沟通形状的详细约束
4b. nacp 协议下，对当前分析目标在 observebility-plane 下输出的日志体系的完备性测试与分析
5. 该目标在过去 black-spot / auth-ready / skill-grading-performance 阶段后，仍然遗留的技术债务台账
6. 该目标负责的 RPC 接口清单，以及接口连通性现状
7a. 监管该目标的 spike 测试体系与测试用例清单
7b. 监管该目标的 mega-journey 测试体系与测试构件清单
8. 该目标涉及到的的 D1 schema 详细说明
9. 该目标当前的健康状况，后续推荐的更新计划，以及最终的 verdict

---

请理解我们的工作计划后，对当前的目标 D17 发起全面调查，然后输出符合目录结构要求的深度分析报告至 clients/truth-grounding/ 文件夹内。

注意，第 9 章节，必须包含:
9.1 逐能力 T 层热力图 - | 能力 | T 层 | 一句话 |
9.2 reverse-water（订正母体初判）
9.3 推荐更新计划
9.4 最终 verdict
