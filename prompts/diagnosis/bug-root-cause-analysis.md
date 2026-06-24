下面，请你使用内建工具，阅读 .tmp/bug-report/0525-batch-01/ 文件夹内 owner 报告过来的最新 bug 截图
图中涉及到的 Session UUID 为

deepseek 传文件 = a3548e5d-a55e-4ba6-b3b4-ee4c4da5245f
deepseek curl = 2dd73f5a-0d8a-4d24-9848-d7b9e8280f5a

请使用 message debug helper 导出聊天记录后，做详细的分析

---

owner 人工 bug 报告如下：

1. 末日级bug: 可以通过 deepseek 传文件这个 session 判断出来。我们在 tool-use 或者提交 llm 请求生成的时候，没有完整的把聊天内容传递到 llm。导致 llm 在中途失去完整的聊天记录。具体体现在，当前一个 turn，deepseek 还在问要不要把文件写入，后面 owner 授权写入，deepseek 就已经遗忘自己在说什么
2. turn 和 turn 之间，tool-use 的渲染，message bubble 出现的位置，还是有很大的问题
3. deepseek curl 这个 session 里面，所有的 bubble 似乎都错乱了。另外就是，用户尝试了 2 次让 deepseek 输出结果。最后都断掉了
4. tool-use 在 chat-interface 里面，如果页面刷新，tool-use 的 UI 就立刻回到我们改进之前的 UI 了
5. 上传文件的状态仍然不统一，和上面第四点一起，这些问题已经 owner 提过很多次了
6. deepseek curl 中，可能是碰到生成失败的情况。前端或后端似乎静默失败，然后前端 chat interface 里面，用户也没有得到什么提醒，就显示"可能已断开"，然后让我刷新页面。这个需要通过聊天记录进行详细诊断
7. 页面刷新后，前端还是会出现 agent message 被吞的情况。这个还需要和前端 markdown 渲染结合起来看。
8. message bubble 里面要注意可能出现文字超出的情况

---

请根据截图中的 bug，owner 的文字反馈，以及 session uuid 的具体导出结果，进行完整的前后端代码分析
你会把 owner 报告过来的错误进行平铺，然后进行 reasoning，判断出 bug 分别属于什么业务簇，然后针对于每一个业务簇中涉及到的 bug，你会发起 sub-agent 进行代码审查与碰撞，D1 schema 结构反省等工作，用于定位 bug 在全局结构上，在微观逻辑中存在的位置
你会考虑到我们上一个阶段的 bug-fixes 的执行计划为：clients/web/docs/action-plan/web-v80/FEX8-owner-test-batch04-fs-bridge-turn-uuid-resume.md

最后，你会使用 docs/templates/bug-analysis-report.md 中的工作原则，并将其作为输出模板，对本次报告过来的内容，提供完整的分析报告
你会把你深度 reasoning，客观辨证的分析报告输出为 .tmp/bug-report/0525-batch-01/analysis-report-by-GPT.md
