# CCMD vs. SDD —— 收敛还是发散?(by Opus · 业主裁定 + 证据化重审)

> **文档对象**:owner 的 **CCMD**(Conductor-driven, Code-as-truth, Multi-agent, Development)方法论 与业界 **SDD**(Spec-Driven Development)的系统性对比,核心争点:**两者会随模型变强而收敛,还是会发散?**
> **作者**:Claude Opus 4.8(业主裁定记录 + 8 路 web 证据 + 独立 reasoning;承接并修正 `nano-agent-vs-SDD.md`)
> **日期**:2026-05-31
> **文档性质**:`eval / general-purpose`(辨证对比,**冻结零决策**;记录业主裁定为权威立场,不另立新决策)
> **文档状态**:`draft | reviewed | superseded`
> **结构来源(dogfood 自身模板)**:`eval-general-purpose` 共有脊 + `eval-retrospective §2 根因表`(用于我自己的 convergence 误判复盘)+ `design §6 Tradeoff` + `design §10 Value Verdict`
> **上游权威输入**:
> - `nano-agent-vs-SDD.md`(v0.1)— 同源不同宗 / 真源认识论反转 / 4 条借鉴;**本文修正其 §7「收敛」结论**
> - **业主裁定(2026-05-31)** — 三支柱发散论(§1,权威立场)
> - `value-proposition-of-template-docs.md`(v0.2)、`workflow-tracks.md`、本会话 context-rot 研究线
> - web 证据:注意力复杂度 / 长上下文衰减(NoLiMa/RULER)/ MoA & Self-MoA / 专家路由 / Gemini 分级定价 / SDD 批评面(附录 A)

---

## 0. TL;DR / 一句话结论(相对 nano-agent-vs-SDD.md 的反转)

**业主是对的:CCMD 与 SDD 不会收敛,会发散。我此前的「模型越强越收敛」判断,把两条不同的轴混为一谈了。**

- 我之前(nano-agent-vs-SDD §7)说:"模型越强越 stateful → 诚实税下降 → 向 SDD 的 spec-primacy 收敛"。**这条只在「单任务的脚手架剂量」这条轴上成立**——模型越强,每个任务需要的仪式越少(我们这一季的减重就是它)。
- 但它**错误地外推到了「架构」这条轴**:是否要用 fleet + 文档为记忆 + 指挥 + fresh-context 扇出,**根本不由单模型能力决定**,而由**模型间的异质性**决定。异质性与「单模型多强」正交,且被一个有竞争的多模型市场**结构性地保证、甚至放大**。
- 业主的三支柱——**注意力机制异质 / 价值生态位异质 / 价格成本结构异质**——都不随能力上升而消失。第三支柱(成本)尤其致命:**独占式长上下文是二次方计算 + 阶梯式超线性定价 + 衰减式质量;CCMD 的有界 fresh-context 扇出是线性成本 + 高召回区间。任务越大,差距越大——这是发散,不是收敛。**

**裁定(§7)**:**微观收敛、宏观发散,净发散。** 单任务的脚手架剂量随模型变强而收敛;但 fleet + 文档为记忆 + fresh-context 扇出这套**宏观架构**,随模型变强、任务变大,反而**更经济、更必要**。真正收敛的唯一条件是「单一模型同时满足:最便宜 + 无限上下文平价 + 无限上下文零腐朽 + 零系统性偏差 + 市场垄断」——五个独立小概率事件的合取,近乎测度为零。**市场抵制单一文化,所以两支不收敛。**

---

## 1. 业主裁定(修饰后记录 · 权威立场)

> 以下三支柱是 owner 于 2026-05-31 对我「收敛论」的纠正,修饰润色后**作为权威立场记录**。本文其余部分是我对它的证据化重审与系统化(§2–§7),不改其结论。

**核心命题**:模型必有各自的能力上限与边界;异质性不是过渡期的缺陷,而是**永久的结构特征**。因此「把一切交给一个足够强的模型一次成型」不成立,CCMD 与 SDD 不会收敛。

- **支柱一 · 注意力机制异质 ⇒ 局部所见不同。** 不可能所有模型的注意力机制相同。即使都宣称 1M 上下文,在 **sliding window、KV cache 量化、token indexing** 上的差异,会让模型扫描文档的方式分化——**看的是同一份代码,局部看到的东西却完全不同**。所以多模型交叉,不是给弱模型补课,而是覆盖**彼此不重叠的盲区**。
- **支柱二 · 价值/生态位异质 ⇒ 永久分工。** 不可能所有模型价值相同。人类社会天然分工;若人类仍是凌驾于 AI 之上的**指挥者**,则 AI 必须按人类的社会规则与组织形式构建,**差异化就不可避免**。价值不同 → 生态位价值取向不同 → 有的在此处强、有的在彼处专。**把所有事交给同一个模型,不合适。**
- **支柱三 · 价格/成本结构异质 ⇒ 成本发散。** 你在价值评定里因「消耗大量 token」给我们扣分,但我们恰恰是**省钱的办法**:它消除模糊空间、让不确定变确定、降低人类参与、提高一次做对的概率——**省的是返工的钱**。而且**我们的费用线性增长**:用多少是多少,业务多时唤醒多个 stateless agent 在 fresh context 下工作。**SDD 若要一个模型担同样的职责,费用是随 context window 指数式上涨的——最贵的就是 context window。我们不仅不收敛,在费用上还会发散。**

> **业主一句话**:模型有边界,价值有分工,成本会发散——所以 CCMD 不是 SDD 的过渡形态,是它在「多无状态异构模型 + 一个指挥」约束下的稳定解。

---

## 2. 我此前的误判与根因(retrospective 复盘 · 诚实先行)

> dogfood `eval-retrospective`:把我「收敛论」的认知失误固化成可检索的学习化石,根因追到机制层。

**一句话**:我把「**单任务脚手架剂量**」的收敛,错误外推成了「**宏观架构**」的收敛——这两条轴正交,前者随能力收敛,后者随异质发散。

| 编号 | 根因 | 类型 | 为什么会发生 |
|------|------|------|--------------|
| **R1** | **轴混淆**:把「每任务需要多少仪式」(dose 轴)与「是否要 fleet+文档+扇出」(architecture 轴)当成同一条轴 | 认知混淆 | 我们这季确实在减重(combo 轨/charter-lite),我把这个真实的 dose 收敛信号,误读成了「整套架构会向单 agent 收敛」 |
| **R2** | **把异质当能力缺口**:默认「多模型 panel」是为了补单模型的弱,于是推「模型变强→panel 失去意义」 | 边界错置 | 忽略了 ensemble 的价值来自**盲点去相关**(diversity),而非**补强**(accuracy);diversity 不随单体变强而消失(§3.1) |
| **R3** | **成本账只算了 token 量,没算成本曲线的形状** | 信息缺失 | 把「我们消耗更多 token」当成减分项,没区分**每任务 token 量**(我们确实更高)与**成本随规模的曲线**(独占式是超线性、我们是线性)——后者才是发散的来源(§3.3) |
| **R4** | **默认市场会出现单一最强模型** | 认知混淆 | 收敛论隐含「赢家通吃的单一文化」假设;现实是有竞争的多供应商市场,**结构性地维持异质**(§4) |

**教训(可迁移)**:下次判断「两种方法会不会收敛」,先问——**收敛的是剂量还是架构?驱动差异的是能力差距(会随时间缩小)还是结构异质(不会)?成本比较的是总量还是曲线形状?**

---

## 3. 三支柱的证据化深究(web + 独立 reasoning)

### 3.1 支柱一:注意力机制异质 ⇒ 盲点不可约 ⇒ panel 是永久结构(非临时拐杖)

**证据(机制层,业主直觉被技术现实证实)**:
- **架构层就不同**:GQA(Llama 用 8 个 KV head 对 64 个 query head)、**sliding-window attention**(Mistral 每层只看最近 ~4096 token,**每层有效窗口被窗口大小而非全长 bound**)、**KV cache 量化**(FP8/INT8/INT4,甚至 SKVQ 把 key 压到 2-bit)——这些都直接改变模型在长程上**实际能取到什么**。两个模型读同一份 128K 代码,有效注意到的子集**本就不同**。
- **效果层可测**:NoLiMa(ICML 2025)显示 **12 个模型里 11 个在 32K 处掉到基线性能的 50% 以下**,GPT-4o 从 99.3% 掉到 69.7%;"lost in the middle" 未解;**有效上下文 << 标称上下文**。每个模型的衰减曲线形状**因架构而异**。

**reasoning(为什么这条不随能力收敛)**:ensemble 的收益 = **基学习器准确度 × 多样性**。模型变强提升的是准确度,**不会消除多样性**——只要架构不同(GQA vs SWA、不同 RoPE 外推、不同量化),系统性盲区就**去相关**。即使是超人模型,也带着训练/架构绑定的**相关系统性偏差**;panel 的价值正是**去相关这些偏差**,而这与单体多强无关。

**诚实边界(Self-MoA 反例,不回避)**:近期 Self-MoA(2025-02)指出——当**一个模型显著占优、且任务同质**时,混入较弱模型会**拉低平均质量**,单模型高温采样的 Self-MoA 反而更好(AlpacaEval 2.0 上 +6.6%)。这**不推翻**支柱一,而是给它**划界**:
> **按生态位路由,按模糊度开 panel。** 在「一个模型明显占优的同质切片」上,别硬混弱模型(用 Self-MoA 式自洽);在**异质、高模糊、高风险、跨域**的工作(安全 + 迁移 + 架构混在一起——正是 CCMD 的主场)上,异质 panel 的去相关收益压倒一切。owner 的 fleet 用在后者,合理。

### 3.2 支柱二:价值/生态位异质 ⇒ 比较优势 ⇒ 分工是均衡而非缺口

**证据(路由前沿正收敛到 owner 的直觉)**:
- 专门化的小模型在对齐任务上**可与/超过**大模型;"smaller, highly specialized models + 路由" 被多篇 2025–2026 工作列为方向(MoDEM、HierRouter、学习式路由)。
- 学习式路由可**匹配/超过单体性能,同时把对昂贵模型的依赖降低 >67%**;三层路由(便宜 triage → 中档 → 顶级综合)是标准范式。

**reasoning(比较优势 = 即使存在绝对最强模型,分工仍是最优)**:这是 Ricardo 的比较优势,不是能力缺口。
> 即便某模型在**所有**任务上**绝对**最强,只要它的 token 有**机会成本/价格溢价**(顶级模型更贵、>200K 还要再翻倍,见 §3.3),把它的**比较劣势**任务交给便宜的专才,**整体成本更低**。指挥者把强模型留给真正需要它的瓶颈,其余下放——**这是经济均衡,不会因为强模型更强而消失。**

owner 的「人类是指挥、AI 按人类组织形式构建」**正是 principal-agent 框架**:只要人类还是 principal,组织就镜像人类组织——而人类组织**永远分工**。分工是结构,不是过渡。

### 3.3 支柱三:价格/成本结构异质 ⇒ 发散(最强、最可证伪的一条)

**先做诚实修正**:owner 说 SDD「指数式」上涨——**严格说计算是二次方(O(n²) prefill 自注意力),不是指数**。但**结论不变,且修正后更强**,因为成本由三层叠加:

1. **计算层(二次方)**:自注意力 prefill 是 **O(n²)**;KV cache 随长度线性膨胀(LLaMA-70B@128K 基础 KV cache 达 1280GB)。"128K 不是 32K 的 4 倍开销——二次方把部署从可行推向昂贵到禁止。"
2. **定价层(阶梯超线性,实测)**:Gemini 3 Pro / 2.5 Pro / 3.1 Pro **超过 200K context,输入单价直接翻倍**($2→$4 / $1.25→$2.50),且**一旦超阈值,输入+输出全部按长上下文价计**。定价本身就是**向上的阶跃函数**,不是平价。
3. **质量层(腐朽税,负边际回报)**:NoLiMa 32K 掉到 <50%;更狠的是 2025-10 的发现——**即使 100% 完美检索,长度本身仍让性能掉 13.9%–85%**。所以独占式长上下文是**花更多的钱,买更差的结果**。

**CCMD 的成本曲线(线性 + 高召回区间)**:把总信息量 `N` 切成大小有界 `c` 的 fresh-context 切片(`N/c` 个),每片 O(c²),总成本 ≈ `(N/c)·c² = N·c = O(N)` **对总信息量线性**;对照独占式 O(N²)。**而且每片都跑在上下文曲线的廉价+高召回区间,永远不付腐朽税。** 业务多时唤醒更多 stateless agent——**费用按使用量线性叠加**,正是 owner 说的「用多少是多少」。

> **所以发散是真的,且比 owner 说的更硬:不是「线性 vs 指数」,是「线性且高召回」vs「二次方计算 + 阶梯定价 + 衰减质量」。任务越大,鸿沟越宽。** 这把 value-prop v0.2 给我们扣的「token 成本」分**反转**了:我们每任务 token 可能更多,但**成本随规模的曲线**,与**一次做对省下的返工**,都站在 CCMD 这边。

**诚实counterweight(不回避)**:Anthropic 自报多 agent 研究系统 token 成本约为单 agent 的 **~15 倍**;CCMD 还要付**协调开销**(写/读文档、`每个 TODO 重拉上下文`、panel 冗余、指挥者的人类时间)。所以:
- **CCMD 的常数项/截距高**——小任务上,单 agent SDD 更便宜。
- **交叉点随任务规模/模糊度/时间跨度右移**——任务越大越长越模糊,独占式的超线性 + 腐朽税越吃不消,CCMD 的线性 + 高召回越占优。
> owner 的成本主张是**规模(斜率)主张**,在斜率上 owner 赢;我补上诚实的**截距**——CCMD 不是「永远更便宜」,是「**越大越省、且省在最贵的返工与腐朽上**」。

**与 context-rot 研究线的接口**:CCMD 的 fresh-context 扇出,本质是对 context rot 的**结构性防御**——它同时有**质量红利**(不进衰减区)和**成本红利**(不进超线性区)。这条正好接上本会话的 context-defending 研究:**供给侧不再开环堆 context,而是用有界 fresh context 把腐朽挡在门外。**

---

## 4. 核心取舍轴:收敛 vs 发散(design §6 Tradeoff 辩证)

**我们(修正后)主张「净发散」,而非 nano-agent-vs-SDD.md v0.1 的「随模型变强收敛」。**

- **为什么发散**:把方法论的差异拆成两条正交轴——
  - **剂量轴(per-task scaffolding)**:随单模型变强 → **收敛**(仪式变少,我们已在减重)。
  - **架构轴(fleet + 文档为记忆 + 指挥 + fresh-context 扇出)**:由**模型间异质性**驱动(注意力/生态位/价格),与单模型能力**正交**;有竞争的多模型市场结构性维持甚至放大它 → **发散**。
  - **合成**:`净 = 微观收敛 ⊕ 宏观发散`。对任何非平凡系统,宏观项主导 → **净发散**。
- **我们接受的代价**:① 承认 CCMD 截距高,小任务上 SDD-单 agent 更省(§3.3);② 文档+协调是真开销,需持续蒸馏减重压住剂量轴。
- **真正收敛的充要条件(几乎测度为零)**:存在一个**单一**模型,同时满足——(a) 每 token 最便宜、(b) 无限上下文**平价**(无 §3.3 阶梯)、(c) 无限上下文**零腐朽**(无 NoLiMa 衰减)、(d) **零系统性偏差**(无需 panel 去相关)、(e) **市场垄断**(无更便宜专才值得路由)。五条独立小概率的**合取**;且 (e) 与有竞争的市场直接冲突。**只要市场拒绝单一文化,两支就不收敛。**

> **第二取舍(承自 nano-agent-vs-SDD §7)**:spec 为真 vs 代码为真。这条**独立于收敛/发散**仍成立:开发者是无持久记忆的异构集群,代码是唯一不幻觉的真相,文档做记忆+协调并持续对账。发散论**强化**了它——既然不会收敛到「单强 agent 从 spec 重生成」,代码为真就不是过渡,是稳定锚。

---

## 5. 系统性对比矩阵(升级 nano-agent-vs-SDD §4/§8)

> 在原 7 条差异之上,把本次三支柱补成显式轴,并标注**该轴随模型变强是收敛(→)还是发散(↔/⤧)**。

| # | 轴 | SDD(spec 为真 · 单强 agent) | CCMD(代码为真 · 指挥 + fleet) | 随能力↑ | 证据 |
|---|----|------------------------------|-------------------------------|---------|------|
| 1 | **真源认识论** | spec 真源,代码可重生成 | 代码真源,文档为记忆+对账 | ↔ 稳定分叉 | nano-vs-SDD §4 |
| 2 | **每任务脚手架剂量** | 低(工具内置) | 高,但**在减重** | **→ 收敛** | 本会话 combo 轨 |
| 3 | **注意力/盲点覆盖** | 单模型盲区随长度暴露 | 异质 panel **去相关盲区** | **⤧ 发散** | NoLiMa;GQA/SWA/KV量化;MoA |
| 4 | **生态位/分工** | 单 agent 全包 | 比较优势路由,各担专长 | **⤧ 发散** | 专家路由 -67% 成本 |
| 5 | **成本曲线(规模)** | O(n²) 计算 + 阶梯定价 + 腐朽税 | **O(N) 线性**扇出 + 高召回区间 | **⤧ 发散** | Gemini >200K 翻倍;二次方注意力 |
| 6 | **成本截距(小任务)** | **低**(单 agent) | 高(协调+文档,~15× token) | — CCMD 输 | Anthropic 多 agent ~15× |
| 7 | **质量随长度** | 进衰减区(rot) | fresh-context 不进衰减区 | **⤧ 发散** | "完美检索仍掉 13.9–85%" |
| 8 | **跨会话记忆** | 单 session,不直接解 | 文档=外部记忆,抗 compaction | ↔ | value-prop v0.2 |
| 9 | **角色切换** | 单 session 内切角色困扰 | 不同模型各担一角,规避 | ↔ | SDD 批评面 |
| 10 | **迁移/重生成** | spec-as-truth **天生强** | 弱(§6 借「重生成 spec」补) | ↔ SDD 占优 | marmelab/isoform |
| 11 | **演化/僵化** | 重前期 spec,易僵化(瀑布) | 三态成熟链 + 对账,随码演化 | ↔ | ThoughtWorks Radar「Assess」 |
| 12 | **市场结构假设** | 隐含趋向单一强模型 | 显式多供应商异质 | **⤧ 发散** | §4 |

**读法**:**唯一收敛的是第 2 行(剂量)**;第 3/4/5/7/12 行——即业主三支柱及其衍生——**全部发散**;其余稳定分叉或各自占优。**发散轴数量级压倒收敛轴 → 净发散。**

---

## 6. 仍可借鉴(守住 code-as-truth;借鉴不拉向收敛)

> 承自 nano-agent-vs-SDD §6,但补一句关键限定:**这些借鉴是「在发散侧把局部做更好」,不是「向 SDD 收敛的台阶」。**

| # | 借鉴点 | 来源 | 用法(守住代码为真 + 发散架构) | 价值 |
|---|--------|------|-------------------------------|------|
| 1 | **迁移用「重生成 spec」** | SDD spec-as-regenerable | 全局仍代码为真;**仅迁移类**(smind CF→Python)引入行为级 regeneration spec,把「原↔新行为对账」设为 closure 硬闸。**注意:这恰恰要在 fresh-context 扇出里逐切片对账**,不是塞进一个独占式大窗——借的是 spec 形态,不是 spec-primacy | 高 |
| 2 | **EARS 验收记法** | Kiro | `design-neo §6 验收格栅` 采 `WHEN <trigger> THE SYSTEM SHALL <response>`,让收口机器可测 | 中-高 |
| 3 | **slash/CLI 工效** | Spec Kit | 把 `.anote/` prompt 库包成 slash/薄 CLI(降本 + 灭 `cf-agents` 笔误),但保留 NL 库,**不学工具锁定** | 中 |
| 4 | **单一 /constitution** | Spec Kit | 每项目一份显式宪章(canon README + charter 硬纪律),利于 smind 式跨项目迁移 | 中 |

---

## 7. Value Verdict(design §10 · 收敛/发散维度评分)

> 较 nano-agent-vs-SDD §8,新增「随能力演化方向」与「成本曲线/规模」两维,并把成本分按 §3.3 反转后重判。

| 评估维度 | SDD | CCMD | 一句话(变动理由)|
|----------|-----|------|------|
| 反 vibe-coding 结构纪律 | 5 | 5 | 同源 |
| 单人单 agent / 小任务工效 | **5** | 3 | SDD 截距低(§3.3 第 6 行)|
| 成本曲线 · 规模(大任务)| 2.5 | **5** | ↑ 反转:CCMD 线性 vs SDD 二次方+阶梯+腐朽 |
| 注意力盲点覆盖 | 2.5 | **5** | 异质 panel 去相关,不随能力消失 |
| 生态位分工 / 比较优势 | 2 | **5** | 路由 -67% 成本;Ricardo 均衡 |
| 长程质量 / 抗腐朽 | 2.5 | **5** | fresh-context 不进衰减区 |
| 跨会话记忆 / 抗 compaction | 2.5 | **5** | 文档=外部记忆 |
| 迁移 / 重生成 | **5** | 2.5→**3.5** | SDD 天生强;CCMD 用 §6.1 借鉴补 |
| 上手 / onboarding | **4** | 2.5 | SDD 工具社区成熟 |
| **随模型变强的演化方向** | 趋单一 | **趋 fleet** | **核心:净发散,非收敛** |
| **综合(各自 régime)** | **4** | **4.6** | ↑ 成本/盲点/分工三轴反转后上修 |

> **给 owner 的一句话裁定**:你纠正得对——**不收敛,净发散**,且发散在最关键的**成本曲线**上。我之前把「剂量收敛」错当「架构收敛」,根因是把异质当能力缺口、把 token 总量当成本曲线(§2)。CCMD 在「多无状态异构模型 + 一个指挥 + 代码诚实 + 有界 fresh context」这个 régime 是**稳定解**,不是 SDD 的过渡形态。该向 SDD 借的仍是那四样(尤以迁移重生成 spec 补 smind 保真缝),但**借法要落在 fresh-context 扇出里,不向 spec-primacy 与独占式长上下文靠拢**。

---

## 8. 一句话结论与给 owner 的(非冻结)决策点

**一句话**:CCMD 与 SDD 同源不同宗,且**不会收敛——会发散**。收敛的只有「单任务脚手架剂量」(随模型变强变轻,我们在减重);而「fleet + 文档为记忆 + 指挥 + fresh-context 扇出」这套**架构**由**注意力异质、生态位异质、价格异质**三条结构性力量驱动,与单模型能力正交,被竞争市场维持甚至放大。第三支柱(成本)最硬:**独占式长上下文 = 二次方计算 + 阶梯定价 + 腐朽质量;CCMD = 线性扇出 + 高召回区间。任务越大,越发散。** 真正收敛需要一个「最便宜 + 无限平价 + 零腐朽 + 零偏差 + 垄断」的单一模型,近乎测度为零。

**3 个决策点(交 owner,不在本文冻结)**:
1. **是否把「净发散」立为方法论的官方自我定位**(写入 README/value-prop),取代 nano-agent-vs-SDD §7 的「收敛」结论?
2. **是否把「按生态位路由、按模糊度开 panel」(§3.1 Self-MoA 边界)显式写成 fleet 调度纪律**——避免在同质切片上硬混弱模型?
3. **迁移类「重生成 spec」(§6.1)是否要求逐 fresh-context 切片对账**(而非独占式大窗),作为守住发散侧的硬约束?

---

## 附录 A · 来源(Sources)

- **注意力复杂度 / 成本**:[Quadratic Attention Bottleneck (Brenndoerfer)](https://mbrenndoerfer.com/writing/quadratic-attention-bottleneck-transformers-long-sequences)、[KV caching explained (Lienhart)](https://medium.com/@plienhar/llm-inference-series-3-kv-caching-unveiled-048152e461c8)、[KV Cache Optimization Strategies (arXiv)](https://arxiv.org/pdf/2603.20397)、[The Sparse Frontier (arXiv)](https://arxiv.org/html/2504.17768v2)
- **长上下文衰减**:[NoLiMa (ICML 2025)](https://icml.cc/virtual/2025/poster/46685)、[Context Length Alone Hurts Despite Perfect Retrieval (arXiv 2510.05381)](https://arxiv.org/html/2510.05381v1)、[Lost in the Middle (emergent property, arXiv 2510.10276)](https://arxiv.org/pdf/2510.10276)、[Evaluating Long Context (Onn Yun Hui)](https://onnyunhui.medium.com/evaluating-long-context-lengths-in-llms-challenges-and-benchmarks-ef77a220d34d)
- **注意力机制异质**:[SKVQ: Sliding-window KV Quantization (arXiv)](https://arxiv.org/html/2405.06219v3)、[DuoAttention (arXiv)](https://arxiv.org/pdf/2410.10819)、[LLM Long-Context & KV Cache (youngju.dev)](https://www.youngju.dev/blog/llm/2026-03-07-llm-long-context-kv-cache-optimization.en)
- **MoA / Self-MoA**:[Mixture-of-Agents enhances LLM (ICLR 2025)](https://proceedings.iclr.cc/paper_files/paper/2025/file/5434be94e82c54327bb9dcaf7fca52b6-Paper-Conference.pdf)、[Rethinking MoA / Self-MoA (arXiv 2502.00674)](https://arxiv.org/abs/2502.00674)、[LLM ensembles & MoA (bdtechtalks)](https://bdtechtalks.com/2025/02/17/llm-ensembels-mixture-of-agents/)
- **专家路由 / 比较优势**:[MoDEM (arXiv 2410.07490)](https://arxiv.org/pdf/2410.07490)、[HierRouter (arXiv 2511.09873)](https://arxiv.org/pdf/2511.09873)、[Learned Routing among Expert Models (arXiv 2511.06441)](https://arxiv.org/pdf/2511.06441)、[AI Model Router (MindStudio)](https://www.mindstudio.ai/blog/what-is-ai-model-router-optimize-cost-llm-providers)
- **分级定价**:[Gemini API Pricing (Google)](https://ai.google.dev/gemini-api/docs/pricing)、[Gemini API Pricing 2026 (aicostcheck)](https://aicostcheck.com/blog/google-gemini-pricing-guide-2026)
- **context rot / 多 agent 成本**:[Context Engineering (Anthropic, via digitalapplied)](https://www.digitalapplied.com/blog/context-engineering-agent-reliability-playbook-2026)、[Mitigating Context Rot (Medium)](https://medium.com/ai-pace/context-engineering-mitigating-context-rot-in-ai-systems-21eb2c43dd18)、[More Tokens Makes Agents Worse (MorphLLM)](https://www.morphllm.com/context-engineering)
- **SDD 批评面**:[The Limits of SDD (Isoform)](https://isoform.ai/blog/the-limits-of-spec-driven-development)、[SDD: The Waterfall Strikes Back (marmelab)](https://marmelab.com/blog/2025/11/12/spec-driven-development-waterfall-strikes-back.html)、[Spec-driven development (Thoughtworks)](https://thoughtworks.medium.com/spec-driven-development-d85995a81387)

## 附录 B · 版本历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | 2026-05-31 | Opus 4.8 | 初稿:记录业主三支柱发散裁定(§1)+ 我的 convergence 误判复盘(§2,根因 R1–R4)+ 三支柱证据化(§3,含 Self-MoA/Anthropic 15× 诚实 counterweight)+ 收敛vs发散取舍(§4,净发散 + 测度为零收敛条件)+ 系统对比矩阵升级(§5,12 轴标演化方向)+ 借鉴限定(§6)+ Verdict 成本分反转上修(§7,综合 4.6)。**修正 `nano-agent-vs-SDD.md` §7 的「收敛」结论为「净发散」。** |
</content>
</invoke>
