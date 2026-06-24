现在，我们在进入到 more-capabilities 的 design 文件制作，你会详细阅读 docs/charter/plan-more-capabilities.md 阶段基石文件

并且，你会阅读并锚定下面几份重要的 eval 文件
docs/eval/more-capabilities/proposed-execution-plan-by-opus.md
docs/eval/more-capabilities/mc-investigation-01-filesystem.md
docs/eval/more-capabilities/mc-investigation-02-context.md
docs/eval/more-capabilities/mc-investigation-03-hooks.md
docs/eval/more-capabilities/debt-repayment-analysis-by-opus.md

你会严格执行我下面的步骤：

1. 首先理解基石文件中要求制作的全部 design 文件，以及 qna 文件
2. 然后创建 todo-list, 对 more-capabilities 下面的所有 design 文件的设计，给每一个 design 文件创建一个 todo 锚定。然后我们后续按照 todo 构成的计划，完成全部 design 文件的设计与制作。
3. 执行 TODO 循环：
    - 首先，你会核对每一个 design 文件的真实需求，理解当前 design 文件在整个阶段内的定位与服务目标
    - 然后，在理解 design 文件的设计目标后，请从 clients/api-docs/ 取回 api 接口的认知，取回基石文件中相关文件，取回相应 eval 文件中的分析章节，作为上下文认知
    - 另外，除了上面的上下文，你还需要使用 sub-agent 专门回到 context/cf-agents/, context/smind-console/, context/codex/, context/claude-code/ 中，寻找对应话题下的的解法，并把可参考的部分，作为真实链接锚定，拉回我们的设计文件内
    - 接着，在得到全部上下文支持后，你会进行独立的 reasoning，判断我们当前话题下的功能要求，应该如何设计。
    - 最后，你会按照 docs/templates/design.md 模板的要求，输出当前 todo 约定的设计文件
4. 按照上面的循环，完成全部的锚定 todo 后，你会对全部的 design 文件进行一次 coherence and consistency 核查，确保所有 design 文件符合基石文件的要求，符合 owner direction，符合 eval 中表达的价值
5. 在审核完全部 design 文件后，你会使用 docs/templates/qna.md 作为模板，输出本阶段的 owner qna 合集文件 MCX-qna.md

---

基于我的上述要求，请串行完成 more-capabilities 阶段的 MCD1 → MCD6 这 6个 设计文件的制作，以及 MCX-qna.md。在全部工作完毕后，制作 design 部分的 README.md。
你不得跨阶段工作，一个 design 阶段的 TODO 循环完成后，才能进入下一个设计循环。并且每次进行新的 design 设计时，你都会按照 todo 循环重新拉取必要的上下文。
所有文件均输出至 docs/design/more-capabilities/ 目录下。
