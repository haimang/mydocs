基于你已经对于所有 action-plan 完成了修复。

现在，我们在进入到 more-intelligence 的 MI1-MI9 全阶段的任务执行
请先通过 .npmrc 的方法，确认我们拥有 packages 的发布权限。并通过 npx wrangler whoami 判断我们拥有必要的 cloudflare 权限。在确认拥有足够权限的基础上，你会执行下面的步骤。

我为你更好地对 MI1-MI9 阶段的代码进行制作，你会严格执行我下面的步骤：

1. 首先重新理解 docs/action-plan/more-intelligence/ 下的 MI1-MI9 action-plan，我们的任务是完成全部代码开发工作
2. 然后创建 todo-list, 对 MI1-MI9 阶段下面的所有工作阶段，为每个阶段创建 2个 todo 锚定，包含 [代码制作] + [代码审查，测试与文档回填] 两部分。
3. 执行 TODO 循环：
    - STEP-1，重新拉取本阶段使用的全部上下文，包括 context/ 下的对照代码，clients/api-docs 下的 api结构文档，以及业主 QNA 文件 docs/design/more-intelligence/MIDX-qna.md
    - STEP-2，按需拉取原始 design 或 eval 文件进行辅助判断
    - STEP-3，在获得全部上下文后，你会按照 action-plan 中的详细要求，进行完整，完全的代码开发
    - STEP-4，在代码开发完毕后，你会进行本阶段的独立代码审查，并设计完成相关的测试。测试修复完毕后，确认本阶段可以收口
    - STEP-5，完成收口后，回填工作日志，append 到当前 action-plan 的底部，使用列表形式记载全部的工作记录。然后你会输出对应阶段的 closure 文件至 docs/issue/more-intelligence/, closure 文件使用 docs/templates/closure.md 作为输出模板

4. 每阶段 两个todo 进行上述循环，直至完成全部的锚定 todo 后，确认完成全部的 action-plan 后，进行完全、完整的 more-intelligence 全阶段代码审查
5. 在代码审查、测试以及修改完毕后，输出 more-intelligence 阶段的 full closure 文件至 docs/issue/more-intelligence/，closure 文件使用 docs/templates/closure.md 作为输出模板

---

基于我的上述要求，请按照 DAG 的设计，串行完成 more-intelligence 阶段的 MI1 → MI9 这 9个 子阶段的工作。在全部工作完毕后，向我报告。
你不得跨阶段工作，一个工作阶段的 TODO 循环完成后，才能进入下一个阶段循环。并且每次执行新的 action-plan 时，你都会按照 todo 循环重新拉取必要的上下文。
注意: 每个 DAG 关键节点结束后，你会提醒暂停下一个 AP 的执行，并提醒我是否先进行上下文压缩，然后再继续 todo-list 的继续工作
我授权你进行全部的 packages 发布与 wrangler 操作权限。
