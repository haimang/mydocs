我们其他 3位 同事已经对我们 grounding-truth / 1st-wave 的 GTF1-GTF8 工作进行了 第1轮 的合并评估和审查, 他们的评审记录在

docs/code-review/grounding-truth/GTF1-GTF8-reviewed-by-GPT.md
docs/code-review/grounding-truth/GTF1-GTF8-reviewed-by-kimi.md
docs/code-review/grounding-truth/GTF1-GTF8-reviewed-by-deepseek.md

请完整阅读 4份 文件后，将同事的全部 review-analysis 中报告的问题平铺出去，进行对比和认知。合并同类问题并创建问题清单台账
然后你会 item-by-item 核查存在问题, 对照我们当前真实的代码，相关阶段的设计与执行文件

1. 首先，将全部问题平铺，合并同类，构建 unified-findings 问题汇聚台账。在 UF 的基础上，你会对每一个问题进行分析，理解并验证其有效性
2. 接着，将全部验证的 verified-findings 构建为台账表格，并把你得到的 UF 与 VF 台账与分析，使用[verified-findings 台账模板]，记录在 docs/code-review/grounding-truth/GTF1-GTF8-review-VF-ledger.md
3. 在 VF-ledger 落盘后，你会将真 [ partial fix ] / [ delivery gap ] 等内容进行全部的修复和更新
4. 将更新/修复执行完毕后，进行完全，完整的 test↔️fix 循环
5. 前序任务完成后，使用修复日志模板，将你的修复日志与整体回应 append 至 VF-ledger 文件底部
6. 对于真实的，必要的 deferred 内容，你会创建/更新 docs/issue/grounding-truth/GTF1-GTF8-deferred-items-ledger.md 用于台账记载

---
注意: unified-findings 使用 UF 作为编号头部，而 verified-findings，使用 VF 作为编号头部。这样来区分 UF 与 VF
注意: verified-findings 台账模板 = docs/templates/review-findings-ledger.md
注意: 修复回应章节模板 = docs/templates/code-review-respond.md
---

你会构建为上面的工作，锚定顺序执行的 task。然后依照绑定的 DAG 执行顺序，完成上面的核查与代码修复工作
