现在，我们在进入到 more-intelligence 的 MIS2 附加阶段的任务执行
请先通过 .npmrc 的方法，确认我们拥有 packages 的发布权限。并通过 npx wrangler whoami 判断我们拥有必要的 cloudflare 权限。在确认拥有足够权限的基础上，你会执行下面的步骤。

我为你更好地对 MIS2 阶段的代码进行制作，你会严格执行我下面的步骤：

1. 首先理解 docs/action-plan/more-intelligence/MIS2-fake-bash-extended.md 执行计划中的全部 Phase，并理解其中的 Owner QNA → docs/eval/more-intelligence/MIS2-qna.md 冻结内容。
2. 然后创建 todo-list, 对 MIS2 阶段下面的所有工作阶段，为每个 Phase 阶段创建 2个 todo 锚定，包含 [代码制作] + [代码审查，测试与文档回填] 两部分。
3. 执行 TODO 循环：
    - STEP-1，重新拉取本阶段使用的全部上下文，包括 context/ 下的对照代码，clients/api-docs 下的 api结构文档，以及业主 QNA 部分冻结的原则和方向
    - STEP-2，重新拉取 workers/bash-core/docs/RWG-0523-by-opus.md 作为背景知识
    - STEP-3，在获得全部上下文后，你会按照 action-plan 中的详细要求，进行完整，完全的代码开发
    - STEP-4，在代码开发完毕后，你会进行本阶段的独立代码审查，并设计完成相关的测试。测试修复完毕后，确认本 Phase 可以收口

4. 每阶段 两个todo 进行上述循环，直至完成全部的锚定 todo 后，确认完成全部的 Phase 后，进行完全、完整的 MIS2 全阶段代码审查
5. 代码审查完毕后，更新必要的 clients/api-docs 下的 API 文档
6. 在全部工作完成后，输出 MIS2 阶段的 closure 文件至 docs/issue/more-intelligence/

---

基于我的上述要求，请按照执行文件内的 DAG 的设计，串行完成 MIS2-fake-bash-extended 全部设定的 Phase 阶段的工作。
你不得跨阶段工作，一个工作阶段的 TODO 循环完成后，才能进入下一个阶段循环。并且每次执行新的 Phase 时，你都会按照 todo 循环重新拉取必要的上下文。
注意: 每个 DAG 关键节点结束后，你会提醒暂停下一个 AP 的执行，并提醒我是否先进行上下文压缩，然后再继续 todo-list 的继续工作
我授权你进行全部的 packages 发布与 wrangler 操作权限。
