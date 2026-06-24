我们下面会对内部的 http / rpc / ws / http 接口进行全面的审查工作，请你执行下面的步骤

- 首先，请你对整个 workers/ 下的真实 6-worker 进行代码审查。你会把目标放在沟通矩阵上。你会理解沟通的拓扑关系，安全边界
- 其次，你会对内部安全边界内仍然存在的 http 协议进行调查，并判断 rpc 化的进程
- 然后，你会对内部 rpc 请求/返回的 api 请求格式，响应格式进行调查，判断是否存在碎片，是否在 6-worker 结构下完全统一
- 接下来，你会查看 context/claude-code 与 context/codex 以及 context/gemini-cli 来判断我们对于 orchstrator-core 还需要提供什么接口
- 最后，你会查看 clients/api-docs/ 下的文档，判断，我们还需要什么样的对外 http 和 ws 接口，来丰富我们前端的功能

---

我们本次的工作，主要在于接口的调查。我们调查了接口的权限边界是否正确，内部 http 退役的当前进度，内部 rpc 的接口形状是否同意，以及我们需要补充的对外 ws / http 接口，以及这些接口的形状是否和 rpc 接口的请求和响应格式统一，是否存在碎片

---

请你制定一个 todo-list，完成上面的审查与报告制作。在审查的过程中，对于重要的发现，你会写子md文件到 .tmp/ 文件夹进行持久化，并服务于最终的调查报告撰写
请把你上面的详细调查，写入 docs/eval/zero-to-real/state-of-transportation-by-kimi.md
