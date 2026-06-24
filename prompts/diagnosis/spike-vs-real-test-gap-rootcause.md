我希望，你可以详细了解一下下面文件夹中的内容
bug-report/0513/
以及这份文件 .tmp/bug-report/0514-batch-01/analysis-report.md

---

然后对我们最新的 web-v60 后端代码进行审查，判断我们的 spike 文件，为什么提前暴露出问题，为什么要等 owner 进行真人测试，这些问题才暴露
如果都要 owner 进行真人测试才能暴露，我们的 spike 还有什么意义呢

我们之前的阶段，甚至还专门做过详细的水桶分析，看来当时的分析，一点用处都没有
比如 docs/eval/product-enhancement/spike/water-level-after-PEX5-by-opus.md ⬅️ 花费了大量的时间，结果看上去对我们后端没有得到任何实际的价值。既没有发现 bug，也没有发现真实链路上的断点和盲点

请重新完整的对我们现在的后端 spike 进行分析。回答我的问题：为什么我们之前的 spike 与真实测试的差别这么大？为什么没有办法提前验证出真实路径的断点？
请详细 reasoning，结合真实代码作为证据，进行完整，完全的客观诚实分析

请把分析报告写入：docs/eval/web-v60-BSS-backend/backend-spike-analysis-after-BSSB6-by-deepseek.md
