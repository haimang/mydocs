我们开始 grounding-truth 1st-wave 的 action-plan 的内容设计与文档输出。你会使用 /workflows 作为输出工具，编排专用的 sub-agent 进行文档输出
在输出 action-plan 的时候，你务必循序下面的原则

1. 使用 docs/eval/grounding-truth/1st-wave/pre-charter-qna.md 内冻结的真相，作为 action-plan 输出的最高 authority
2. 使用 docs/eval/grounding-truth/1st-wave/final-execution-plan.md 最终确定的方案
3. 使用 docs/eval/grounding-truth/1st-wave/reference-anchor-index.md 作为上下文的索引文件，并要求 sub-agent 对 reference-anchor 进行充分的理解
4. 你会根据上面的要求，为每一个 sub-agent，定制其专用的 PROMPT 用于对应 ap 的分析和输出工作。你会要求每一个 sub-agent 进行独立的代码核验后，充分拉取回上下文后，才会进入撰写工作
5. 输出的 action-plan，必须严格遵守 docs/templates/action-plan.md 模板的格式要求与内容安排

---

请首先自己理解 qna 以及 final-execution-plan 带来的 scope。然后按照要求为每个 sub-agent 定制精准的独立 PROMPT
使用 dynamic workflows 的功能，按照模板约束，完成全部 action-plan 的分析与撰写，并输出至 docs/action-plan/grounding-truth/1st-wave
在所有 action-plan 完成后，workflows 会安排独立的审查，执行 action-plan 与 qna 的交叉核对，事实认知审查。并修复找到的所有问题
