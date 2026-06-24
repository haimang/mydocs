下面，我希望基于 docs/eval/backend-next/cf-agent-analysis-index-0516-by-GPT.md 这份分析，对 cf-agents 做更深度的探索
你会根据我的指令，创建对应的 TODO-LIST 然后进行工作，我们审查的主题范围如下：

---

1. **Agent 基础运行时**
2. **浏览器/客户端接入**
3. **共享聊天协议与聊天底座**
4. **AI 聊天代理层**
5. **Opinionated agentic runtime（Think）**
6. **子 Agent / Agent Tool 编排**
7. **MCP Server / MCP Client / x402**
8. **Email / Workflow / Schedule / Retry / Observability**
9. **CLI 与工程入口**
10. **Browser Tools / WebMCP / Browser-side Agent 能力**
11. **Code Mode：让 LLM 写代码而不是逐个调工具**
12. **Sandboxed state / filesystem / workspace / git**
13. **Voice Agent Runtime**
14. **第三方 Voice Provider 扩展**
15. **运行时 Worker 构建与动态加载**

---

你为上面每一个主题，创建一个 todo，然后构建成为完整的 todo-list。对于每一个 todo，你会执行下面的循环

- 首先，分析当前主题下，设计到的全部文件和文档位置，并形成树状目录结构，以及拓扑依赖关系
- 然后，你会对当前主题下的功能，基于实际的代码审查，做出更详细的分析。分析的粒度是文件级的。你会对重点文件和文件夹的用途，进行更详细的分析
- 接下来，你会基于当前的主题，基于实际代码，创建逻辑 DAG 执行层级分析，主动分析该主题下的业务逻辑是如何进行流转，拥有什么样的依赖
- 接着，你会对于主题下的关键文件，进行文件内逻辑模块级的分析，重点分析当前文件为什么是该主题内的核心文件
- 然后，进行亮点分析，分析当前主题下的逻辑，是如何为 cf-agents 项目提供了足够的价值支撑。
- 最后，你会对这个主题的实现，执行，提供辨证，完整的 verdict

你会对上面 15 个 主题，构建可串行执行的 todo，你不得同时进行多个主题的调查。每个 todo 必须独立调查，构建其独立的上下文线索
你会从 Agent 基础运行时 开始，到 运行时 Worker 构建与动态加载 结束，进行全面的分析。每个分析，创建独立的分析文件。

你会把每一个主题的分析，作为独立文件，写入 docs/eval/backend-next/cf-agent-analysis/{数字编号}-{英文主题}-by-GPT.md
你会串行分析，并写入 15 个独立的分析文件。
