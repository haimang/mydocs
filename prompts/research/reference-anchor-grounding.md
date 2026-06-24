我们将继续利用 docs/templates/eval-reference-anchor.md 作为输出模板以及内容约束，开始上下文锚定研究工作

我们下面的研究对象为 RA-02 - 存储面（transcript 再架构）
你的调查工具和方法主要是下面 3 条路径:

1. 多轮次，深度，追问式的 web-search。你将不满足进行一轮 web-search。你会在第一轮 web-search 得到基本信息后，展开更深度的检索，得到深度内容和相关分析
2. 对 context/ 下的参考系，发起深度调查。其中 cf-agents 为必须调查的内容，其他参考系你根据本次研究对象，进行内聚分析后，仅对相关的参考系进行深度分析。分析可参考的业务逻辑，踩坑记录，以及测试用例。
3. 对 nano-agent 的相关代码区域，d1 schema，以及 rpc 接口部分，进行深度的整理与分析

---

我们进行 reference-anchor 的目的是为了确定当前的代码真值。并通过 web-search 和内部 context 勘探，提供深度的正例/反例，以及可直接借鉴的代码实践，供我们后续开发进行参考
你会在全面理解工作目标以及本次研究的主题后，对 context/ 勘察完毕后，定制带有专用 PROMPT 的深度探查 sub-agent fleet，展开深度检索
sub-agent 会被要求输出 file:line 级别精度的证据

在检索信息回归后，你会汇聚全部的内容，再次展开深度推理，并进行独立的事实核查后
根据 file:line 证据，根据我们的研究对象要求，在模板的约束下，分析并撰写 RA-02-transcript.md
