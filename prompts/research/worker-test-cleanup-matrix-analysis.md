我希望构建一个新的 HPX1 阶段，这个阶段可以命名为 HPX1-worker-test-cleanup-and-enhance，在本 hero-to-pro 的附加阶段内，我希望

1. 对全部 6-worker 内部的 test 进行分析和整理
  - 判断 当前已无意义 / 冗余 / 失效 / 前置条件已经不复存在的测试项
  - 判断 事实逻辑认知不清 / stale，并当前应该立即补强的测试项

2. 对全部 test/package-e2e 内部的 test 进行分析和整理
 - 判断 6-worker 内部 test 分工不清的测试，也就是不属于 e2e 的测试，将这些测试删除或者转移至对应 worker 的内部，或进行拆分重组
 - 判断 当前已无意义 / 冗余 / 失效 / 前置条件已经不复存在的 包内 e2e 测试项
 - 根据当前的代码结构，对需要新增，补强的测试项进行分析

你会提供专项分析，哪些测试项应该回归到 worker 内部，而哪些应该放在 package-e2e 内
你会提供专项分析，对所有的测试面进行整理，使用列表结构对所有的测试进行matrix评估，判断我们的测试冗余以及缺口

---

你会将你辩证，完全，中文的审查分析，写入 docs/eval/hero-to-pro/HPX1-test-analysis-by-deepseek.md

你在撰写文档的时候必须独立思考，仅使用你自己的reasoning，不会考虑其他同事，比如 Kimi，Deepseek，或 GPT 的分析报告
注意使用 docs/templates/code-review.md 作为输出模板
