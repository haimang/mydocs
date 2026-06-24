我们的同事，已经根据我们 web-v90 real-workspace 章节 RWX12-RWX14 的 action-plan，完成了RWX12-RWX14 的预定的工作

而且，已经在前序工作里，完成了2轮的代码审查和修复循环
第一轮审查为 RWX7-RWX11，第二轮审查为 RWX5-RWX11，这些审查统一的 BUG 与回复日志位于
clients/web/docs/code-review/web-v90/RWX7-RWX11-reviewed-by-opus.md
clients/web/docs/code-review/web-v90/RWX5-RWX11-reviewed-by-opus.md

同时，我们的 opus 还诚实的记录了全部的 deferred items，文件位于
clients/web/docs/eval/web-v90/bug-fixes-04/deferred-items-analysis-after-RWX11-by-opus.md

请在理解上述两次审查的基础上，对 Opus 的全部修复内容进行完整，完全的第三轮审查工作，审查范围是：

1. Opus claim 已经完成的工作，你会 fan-out 子代理，通过内聚的业务簇，进行深度审查
2. 对线上 d1 schema 与代码进行大规模 live schema 审查
3. 对所有的 前端 spike + playwright，后端的 spike + mega journey 发起审查，判断这些测试项是否具备实际意义，是否存在盲点，断点，是否可以真实的做到其预定价值的工作，起到门禁作用
4. 你会对前后端多个 worker 在更新后的 nacp.core 与 nacp.session 协议遵守程度发起审核，判断我们的通信使用是否符合标准

对于已经宣告 deferred items，请你不用进行报告

本轮测试为动态代码审查，意味着，你需要连接线上 d1 数据库，发起真实的 e2e spike 测试。注意，你已经拥有全部的 wrangler 权限，你不得阻值你自己因为任何原因而放弃 e2e 测试的行为。

你会将你辩证，完全，中文，对于代码的静态审查分析，写入
clients/web/docs/code-review/web-v90/RWX5-RWX11-2nd-pass-reviewed-by-GPT.md

你在撰写文档的时候必须独立思考，仅使用你自己的reasoning，不会考虑其他同事，比如 Kimi，Deepseek，或 GPT 的分析报告，也不会考虑已经存在的分析报告
严格使用 docs/templates/code-review.md 作为输出模板
