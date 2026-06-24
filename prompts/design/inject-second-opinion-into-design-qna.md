我们的 Opus 已经完成了全部 Design 文件的制作，所有的 more-intelligence 阶段的设计文件，已经落盘于

docs/design/more-capabilities/
请阅读文件夹内的全部文件，并同时取回 docs/charter/plan-more-capabilities.md 基石文件作为 full-picture 理解

---

在理解了全部的上下文后，你会执行下面的循环
- STEP 1，理解全部的 MCD1-MCD7 合计 7 份 design 文件
- STEP 2，从 MCD1 开始，拉取 MCD1 拥有的全部上下文，包括基石文件，相关的 eval 文件
- STEP 3，使用 sub-agent 开始调取真实代码，通过代码与 MCD1 中的全部 owner qna 进行碰撞，进行问题求解
- STEP 4，在 docs/design/more-capabilities/MCX-qna.md 找到 MCD1 中 qna 的对应内容，将你在 STEP 3 中得到的 reasoning，以及解答，注入到 GPT second opinion 处
- STEP 5，执行下一个 MCD 文件的 qna 循环

---

你会从 MCD1 开始，到 MCD7 结束。为每一个 design 文件创建一个 todo，然后在 todo 内循环上下文拉取，sub-agent 代码碰撞，qna 求解，second opinion 注入的这个循环
你只能一个一个 design 文件进行处理，不得多 design 同时注入内容。严禁跨 design 文件进行上下文拉取和输出。

这样，保证在回答一个 MCD 文件的时候，上下文都是和当前 MCD 相关的。
请从 MCD1 开始，回答所有问题，注入 second opinion，直到 qna 全部填写完毕。
如果 qna 与设计文件有不符的，以 MCX-qna 中的问题为最终标准。

