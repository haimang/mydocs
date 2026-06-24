下面，请把你找到出现问题的业务簇，作为探查的方向，对 context/ 下的内容进行详细的探查，我们来看看别人是怎么做的

首先，我们确定分析的方向为 context/cf-agents，context/just-bash，以及 context/claude-code
然后，你会确定调查的主题，并构建对应的 sub-agent，对每一个 context 文件夹发起调查
接着，你会把调查的结论进行平铺和总结，进行独立的 reasoning，并与我们已经完成的分析进行碰撞
最后，你会判断对 context 调查，如何影响我们的分析结论，如何影响我们推荐我们的工作清单，如何更好的，站在全局角度对之前预定的工作进行调整

---

请讲你对 context/ 探查的分析， 使用你对 context 分析得到的结论，对 .tmp/bug-report/0525-batch-01/analysis-report-by-GPT.md 这份原始分析报告进行 critique
然后把你的辨证，全局，多角度，包含具体执行建议改进的分析，写入 .tmp/bug-report/0525-batch-01/context-eval.md
