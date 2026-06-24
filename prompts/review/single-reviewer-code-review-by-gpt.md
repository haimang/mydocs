我们的同事，已经根据我们 grounding-truth / 1st-wave 的 GTF1-GTF8 的全部工作
除了每个阶段各自的收尾，共计 8 份文件: docs/issue/grounding-truth/

本阶段总执行索引: docs/eval/grounding-truth/1st-wave/final-execution-plan.md
本阶段业主 QNA: docs/eval/grounding-truth/1st-wave/pre-charter-qna.md

---

在理解上面全部文件的基础上。本轮审查的目标，是我们 grounding-truth / 1st-wave 阶段的完整目标，即: 
- 使用长治型修复手段，在进入到前端下一轮开发前，修复 context 部分的 P0 级别的 blocker
- 在下一轮前端开发前，提供更多的可观测，在未来前端开发需要 debug 的时候，提供充分的数据和接口支持

下面，你将展开 第1轮 代码审查工作:

1. 理解我们 grounding-truth / 1st-wave 的 GTF1-GTF8 的全部工作内容，对于实现者声明的完工内容，进行深度的审查工作
2. 重点核查 我们在本次，由 docs/eval/grounding-truth/1st-wave/pre-charter-qna.md 定义的方向，是否真实存在推进，是否 owner-gated 价值得到了充分的执行和尊重
3. 重点核查 我们的 nacp 协议，在跨 worker 沟通的时候，尤其是 observability-plane 在上下文压缩，hooks 使用，以及其他方向上的可观测性是否实质性加强

你构建完整的 todo-list，构建合理的代码审查 DAG 执行计划。然后利用 sub-agent，对每一个内聚的业务簇审查话题，发起并行检查，最后将结论同步后，进行完整，完全的审查分析
你会将你辩证，完全，中文，对于代码的静态审查分析，写入 docs/code-review/grounding-truth/GTF1-GTF8-reviewed-by-GPT.md

你在撰写文档的时候必须独立思考，仅使用你自己的 reasoning，不会考虑其他同事，比如 Kimi，Deepseek，或 GPT 的分析报告，也不会考虑已经存在的分析报告
注意使用 docs/templates/code-review.md 作为输出模板
