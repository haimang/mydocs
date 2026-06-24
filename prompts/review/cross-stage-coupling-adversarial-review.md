我们刚刚合并了从 dev 分支过来的 skill-performance-grading 阶段代码
我们本地 main 分支完成了 auth-ready 阶段的代码

下面，我们将对合并后的两个阶段，进行联合代码审查工作。首先请理解两个阶段的工作目标
docs/eval/auth-ready/final-execution-plan-by-opus.md
docs/eval/skill-performance-grading/final-execution-planning.md

然后，在理解了工作目标的基础上，通过 closure 文件理解当前 SPG 与 AR 阶段的执行终态
docs/issue/auth-ready/AR-full-closure.md
docs/issue/skill-performance-grading/SPG-full-closure.md

同时，理解两个阶段各自的 deferred-items
docs/issue/auth-ready/deferred-items-ledger.md
docs/issue/skill-performance-grading/deferred-items-ledger.md
docs/issue/auth-ready/unified/AR-SPG-deferred-items-ledger.md

---

在理解上面全部文件的基础上。我们将进行两个阶段代码的合并审查工作，将两个阶段合并成为同一个阶段，进行功能耦合审查
下面我们进入 AR+SPG 的 第2轮 审核，你会重点审查下面的内容:

1. 理解我们 AR+SPG 的全部工作，确定所有的的功能耦合位置，并对这些位置展开进攻性的对抗审查，判定这些耦合点是否牢固，是否存在逻辑错误
2. 重点核查 实现者在 第1轮 修复中的工作 [docs/code-review/auth-ready/unified-AR-SPG-review-VF-ledger.md] 中做出的修复，是否已经真实落盘，修复是否到位，是否修复正确
3. 重点核查 D1 数据库在两个阶段的运用，以及与 session.do 和 user.do 在不同数据库之间数据流转的逻辑是否正确，是否存在盲点，断点或逻辑错误
4. 重点核查 两阶段的合并后，联合作用下的 clients/api-docs 文件是否存在过期，是否存在事实错误，是否存在欠更新

你构建完整的 todo-list，构建合理的代码审查 DAG 执行计划。然后利用 sub-agent，对每一个内聚的业务簇审查话题，发起并行检查，最后将结论同步后，进行完整，完全的审查分析
你会将你辩证，完全，中文，对于代码的静态审查分析，写入 docs/code-review/auth-ready/unified-AR-SPG-2nd-pass-reviewed-by-opus.md

你在撰写文档的时候必须独立思考，仅使用你自己的 reasoning，不会考虑其他同事，比如 Kimi，Deepseek，或 GPT 的分析报告，也不会考虑已经存在的分析报告
注意使用 docs/templates/code-review.md 作为输出模板
