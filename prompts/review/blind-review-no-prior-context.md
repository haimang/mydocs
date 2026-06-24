现在，请你扫描整个 web-v50 ux-alignment 阶段的工作。请严格按照我的要求进行代码审查。请执行下面的步骤

1. 构建必要的背景认知
- 原始后端eval评估 → clients/web/docs/eval/web-v50/analysis-on-backend-alignment-by-opus.md
- 原始前端eval评估 → clients/web/docs/eval/web-v50/analysis-on-frontend-alignment-by-GPT.md
- Owner direction qna → clients/web/docs/eval/web-v50/pre-charter-qna.md

2. 在对原始分析理解的基础上，理解下面两份基石文件
- 前端基石 → clients/web/docs/charter/web-v50-ux-alignment-frontend.md
- 后端基石 → docs/charter/plan-web-v50-ux-alignment-backend.md

---

请在仅了解上面这些文件的情况下，对前后端代码进行审查工作。你不得查看前后端在 web-v50 阶段的 design，action-plan，以及 closure 文件
owner同时禁止你阅读我们上一轮的 full review 以及 fix-01 审查报告，及对应closue文件中的内容，你会完全，完整的重新进行代码审查和评估
你的目标是，严格的审查我们的代码，判断代码是否符合基石文件，以及背景 eval，以及 owner qna 中判定的 web-v50 目标

你审查的范围包括了前端、后端，数据库 DDL 的全部内容
你会比照 context/open-webui/ 中的结构，来判定前端的适配是否正确

请把你对 web-v50 代码实现中的断点，盲点，逻辑错误，与 owner-direction 相悖的所有问题进行审查
然后批判性地撰写审查报告至：docs/code-review/web-v50-ux-alignment-backend/web-v50-full-2nd-pass-review-by-GPT.md

你在撰写文档的时候必须独立思考，仅使用你自己的reasoning，不会考虑其他同事，比如 Kimi，Deepseek，或 GPT 的分析报告，并禁止阅读我们上一轮的 full-review
注意使用 docs/templates/code-review.md 作为输出模板
