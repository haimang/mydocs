下面，从 clients/api-docs 作为出发点，作为我们前端拥有的全部接口的 SSOT，请对我们已经定点出来的接口，进行逐接口的审查

1. 从每一个接口出发，追溯这个接口的路由，直到具体的执行代码。判断当前接口的功能性，真实性
2. 从每一个接口出发，追溯这个接口的测试项，判断当前的接口背后的逻辑，是否存在某个测试项进行了逻辑测试覆盖
3. 从每一个接口出发，追溯这个接口的使用条件，包含 auth，请求形状，输出形状，判断这个接口的输入和输出符合我们的整体标准，没有异常形状，也没有缺失的 auth
4. 从每一个接口出发，通过 nacp 协议对沟通链条进行测试，判断当前接口是否可以在双向经受 nacp 协议约束，并符合 nacp 要求

---

由于当前接口较多，我们会分成功能簇，分步骤完成接口的 compliance 分析，接下来，你会分析下面几个文件中约定的接口

clients/api-docs/usage.md
clients/api-docs/wechat-auth.md
clients/api-docs/workspace.md

---

请把上面 3个 功能簇背后的接口，进行逐一分析。注意，每一个接口都需要进过相同的检查。在全部接口检查检查完毕后，你会把文件写入
请把你的调查报告，写入 docs/eval/hero-to-pro/api-compliance/part5-by-deepseek.md
你会使用 docs/templates/api-compliance.md 文件作为输出模板
