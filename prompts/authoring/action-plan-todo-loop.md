现在，我们在进入到 more-intelligence 的 action-plan 文件制作，你会详细阅读更新后的 docs/design/more-intelligence/ 下的全部设计文件
并且，你会详细平铺全部的 业主QNA docs/design/more-intelligence/MIDX-qna.md 作为上下文的重要参考

你会严格执行我下面的步骤：

1. 首先理解 docs/charter/plan-more-intelligence.md 基石文件中要求制作的全部 action-plan 文件
2. 然后创建 todo-list, 对 more-intelligence 下面的所有 action-plan 文件的设计，给每一个 action-plan 文件创建一个 todo 锚定。然后我们后续按照 todo 构成的计划，完全全部 action-plan 文件的设计与制作。
3. 执行 TODO 循环：
    - STEP-1，你会核对每一个 action-plan 文件的真实需求，理解当前 action-plan 文件在整个阶段内的定位与服务目标
    - STEP-2，在理解 action-plan 文件的设计目标后，请从 clients/api-docs/ 取回 api 接口的认知，取回基石文件中相关文件，拉回 业主qna 中的必要 direction 作为指导，构建完整的上下文认知
    - STEP-3，除了上面的上下文，你还需要专门回到 context/code, context/gemini-cli, context/claude-code 中, 拉取 design 文件提出的上下文 reference，并作为制作 action-plan 的重要依据
    - STEP-4，在得到全部上下文支持后，你会进行独立的 reasoning，判断我们当前话题下的功能要求，完成该 TODO 要求的代码执行的设计
    - STEP-5，你会按照 docs/templates/action-plan.md 模板的要求，输出你的设计为 action-plan 文件
4. 按照上面 STEP 循环，完成全部的锚定 todo 后，你会对全部的 action-plan 文件进行一次 coherence and consistency 核查，确保所有 action-plan 文件符合基石文件的要求，符合 owner direction
5. 在审核完全部 action-plan 文件后，你才会创建基石文件中要求的 README.md

---

基于我的上述要求，请按照 todo 的规划，串行完成 more-intelligence 阶段的 MI1 → MI9 这 9个 执行文件的制作。在全部工作完毕后，向我报告。
你不得跨阶段工作，一个工作阶段的 TODO 循环完成后，才能进入下一个阶段循环。并且每次进行新的 action-plan 设计时，你都会按照 todo 循环重新拉取必要的上下文。
所有文件均输出至 docs/action-plan/more-intelligence/ 目录下。
