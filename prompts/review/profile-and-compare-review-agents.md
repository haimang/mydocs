现在，请你理解这几份文件

clients/web/docs/code-review/web-v90/RWX20-RWX22-reviewed-by-opus.md
clients/web/docs/code-review/web-v90/RWX15-reviewed-by-opus.md
clients/web/docs/code-review/web-v90/RWX15-reviewed-2nd-pass-by-opus.md
clients/web/docs/code-review/web-v90/RWX12-RWX14-reviewed-by-opus.md
clients/web/docs/code-review/web-v90/RWX7-RWX11-reviewed-by-opus.md
clients/web/docs/code-review/web-v90/RWX5-RWX11-reviewed-by-opus.md

---

这几份文件，不单单只是 opus 的 code-review。重点在文档底部的 unified-findings 以及 verified-findings，以及最终的修复日志
现在，owner 希望可以请你在阅读这些内容后，对每一个 review agent 进行画像分析
你可以参考 docs/templates/legacy/code-review-eval.md 这份文件中的输出要求，对 minimax, opus, GPT, deepseek 以及 kimi 这 5 个 agent 进行独立分析

每一个 agent 都需要提供模板内的主要内容，并 focus on 下面的话题
1 - 其代码审查的风格
2 - 代码审查的精度
3 - 相较于其他 review-agent 的优点（附带证据）
4 - 主要缺点和盲点（附带证据）
5 - 价值 matrix 表格
6 - 对 agent 审核画像的总结

在整个 eval 的最后，附加一个完整的 verdict，提供在不同场景下，不同业务推进进度上，应该如何组合不同的 agent 进行工作
并提供一个完整的价值对比 matrix 给 5 个 agent 放在一起做 comparison

请把 eval 文件写入 docs/owner-decisions/compare-5-review-agents-0608-by-opus.md
