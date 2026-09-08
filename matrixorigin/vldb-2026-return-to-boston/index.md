---
title: "回到波士顿 —— VLDB 2026 见闻，52年的数据技术变迁和新的黄金时代"
author: 张祖羽
description: "MatrixOrigin 张祖羽博士的 VLDB 2026 现场见闻：52 年后回到波士顿的怀旧环节、Reynold Xin 与周靖人的两场 Keynote、Agent 时代的数据系统趋势与 GPU 数据库的兴起，以及 ContextPipe 获得 ADS 2026 Oral Paper Award。"
tags: ["行业洞察", "VLDB", "Agent", "ContextPipe", "Astra"]
keywords: ["VLDB 2026", "Boston", "Agentic", "第三个黄金时代", "GPU Database", "Sirius", "ContextPipe", "Astra", "ADS 2026"]
date: "2026-09-08T18:00:00+08:00"
publishTime: "2026-09-08T18:00:00+08:00"
image:
  "1": "/images/blog-covers/technical.png"
  "235": "/images/blog-covers/technical.png"
lang: zh
status: draft
---

# 回到波士顿 —— VLDB 2026 见闻，52年的数据技术变迁和新的黄金时代

*张祖羽 博士 现场见闻 | MatrixOrigin* 

（张祖羽博士2019年在UW-Madison获得博士学位，研究方向是Database Systems。UW-Madison 数据库组培养了无数顶尖学者与工业界领袖，包括David DeWitt和Raghu Ramakrishnan这样的数据库泰斗，这群校友和教授在国际学术界（如 SIGMOD、VLDB）极具影响力，常被戏称为Wisconsin DB Mafia）


---

### VLDB 是个什么会

VLDB，全称 **International Conference on Very Large Data Bases**，国际超大规模数据库会议。1975 年就创办了，和 SIGMOD、ICDE 并称数据库领域的三大顶级会议。今年已经是第52年举办了。第一届就是在Boston办的，后来为了跟Sigmod另外一个美国本土为主的会打差异化，就一直在别的地方办了。

今年是51年后第二次回到Boston。所以会议也安排了一次特别的怀旧活动。请一众该领域的学术大佬共同回忆1975年以及后来这么多年数据技术的变迁，包括大家熟悉的已经80多岁的图灵奖获得者 Michael Stonebraker (C位)，还有我们公司CTO田丰博士的导师David Dewitt（Stonebraker左边的那位）。

![Return to Boston 特别环节合影：Michael Stonebraker、David DeWitt 等](./images/return-to-boston-panel.jpeg)


这个会议的名字本身其实就几乎代表了整个数据技术发展的整个历史。**Very Large Data Bases** 超大规模的数据库。这几个词在 1975 年被写进会议名的时候，是一句宣言：**我们要处理的数据，已经超出了当下的系统能够舒服处理的规模。**

这句话放到今天依然适用：**数据的规模，永远在超出系统的能力。** 所以这个名字52年没改过，也不需要改——因为里面的每一个词，都在被一代一代地重新定义：

- **Very Large**：1975 年是几十 MB，今天是 EB。这个形容词是相对的，它的参照系一直在往前跑。
- **Data**：从结构化的记录，到日志、到向量、到图、到非结构化文本，到今天的LLM模型。
- **Base**：从单机上的一个文件，到分布式集群，到云上的 Lakehouse，到今天我们开始认真讨论的新东西 Agent。

一个会议能开五十二年还没有失去焦点，靠的就是这一点：**它守的不是一项技术，是一个问题。** 技术会过时，问题不会。

**而今年这届 VLDB，我认为是这个问题被重新提问的一年。** 会上最被反复引用的一句话是"我们正处在数据管理的第三个黄金时代"，而这个新时代的名字叫 **Agentic**. Agent 已经开始深度的影响数据技术的过去，现在和未来。

* 面向过去，企业已经沉淀的大量legacy的数据库系统及数据跟Agent如何结合。
*  面向现在，当下的新型数据基础设施如何设计，以满足Agent负载对数据的使用方式。
*  面向未来，在Agent高速应用的发展趋势下，数据基础设施还应该思考哪些核心问题来适应未来。


---

### Keynote Speech：数据管理的新黄金时代

今年的两场 keynote，都是华人主导的内容。从两个方向回应了同一个问题：当 AI 开始大规模使用数据，AI 模型又需要大量的数据来训练，数据系统需要怎样满足？

**Reynold Xin：数据库工程迎来了第三个黄金时代**

第一个Keynote Speech是由Databricks 的华人科学家 **Reynold Xin** 带来的，Databricks也是近十年来最成功的一家商业数据基础设施公司。他的演讲题目是

> **The Three Golden Ages of Database Engineering: From SIGMOD '85 to the Agentic Era**

他将整个数据库发展的历史列举了三个黄金时代：

- **第一个黄金时代**，关系模型和早期关系系统。核心议题是"如何把声明式的查询正确、高效地执行出来"。查询优化器、事务、代价模型，这一整套家底都是那时候攒下的。
- **第二个黄金时代**，大数据。分布式、列存、云上的存算分离，最终在 Lakehouse 这个架构上收敛。这一代人解决的是"规模"。
- **第三个黄金时代**，也就是现在——**agentic era**。新的负载进来了：operational analytics、向量检索，以及大量由模型而不是由人发起的请求。他在这个基础上讲了Databricks的 Lakebase 和 LTAP这套东西。

一个领域走过五十多年，很多基础问题确实似曾相识，但使用系统的人、运行的任务、资源的约束都在变化。旧问题会因此获得新的难度，也会重新打开设计空间。

**周靖人：模型训练的数据工程账本**

第二个Keynote Speech是由阿里巴巴的**周靖人博士**带来的，周靖人其实是AI科学家，所以是从大模型训练的角度来看待数据工程，他的题目是：

> **Efficient and Reliable Systems for Building Foundation Models at Scale**

这一场信息密度极高，是我这几天做笔记最多的一场。

![周靖人博士 Keynote 后合影](./images/keynote-jingren-zhou.jpg)

内容主体是从 Qwen 和 Wan 这两条模型线的实际研发经验出发，讲万亿参数规模的模型在训练和部署上，系统层面到底要解决什么问题：分布式计算怎么切、大规模集群上的**容错**怎么做（规模到了之后，故障不是异常而是常态），以及在云上怎么去平衡**吞吐、延迟、成本、可用性**这四个互相拉扯的目标。

其实预训练这件事，已经彻底变成了一个关于电力、集群、故障恢复和调度效率的工程问题，而且是一个只有极少数玩家玩得起的工程问题。这场 keynote 对在场大多数人（学术界、创业公司、以及像我们这样的小团队）最有价值的部分是这句话：

**预训练的门确实关上了，但 post-training 和 inference 这两扇门还开着，而且开得不小。**

这个判断我完全同意，而且想把它说得更具体一点：

1. **post-training 是"领域知识+系统能力"的战场，不是"算力"的战场。** 它要的是高质量、有结构、可追溯的数据 pipeline。这恰恰是数据管理这个学科五十年来一直在干的事。
2. **inference 是一个彻头彻尾的系统问题。** KV cache 怎么管、怎么复用、怎么在多租户之间调度，prompt 的哪一部分该缓存、哪一部分必须重算——这些问题的形状，和数据库里的 buffer pool、物化视图、查询结果缓存，是同构的。我们这些做过存储引擎的人看这些问题，是有天然优势的。
3. 也就是说，**小玩家的机会不在"更大"，在"更准"和"更省"**。你没法比别人多烧十倍的卡，但你可以在同一个任务上少花 30% 的 token。



---

### 会议其他见闻和感受

这一周下来，能明显感觉到一个趋势：传统的数据库研究——性能优化、运维、优化器算法这些课题——仍然在继续，但大量的目光和研究资源已经被彻底吸引到 AI 和 Agent 上了。

看 workshop 的排布就够了。周一还是经典阵容：ADMS、AIDB、QDB、TPCTC，动辄第十几届。到了周五，画风完全变了：**ADS**（Agentic Data Systems 与 Data-Centric AI 联合研讨会，也就是我们 present 的这个，由清华李国良老师主导）、**VecDB**（第 2 届向量数据库）、**Agents + Graphs**、**DASHSys**（human-in-the-loop 的 Agent 系统）、**CDMS**（可组合数据管理），甚至还有量子计算与数据管理的 **QCDKM**。

**Data Agents**

主会场最热的一场 panel 是 **"Data Agents: Rethinking Data Systems in the AI Agent Era"**，清华李国良老师和港科广罗宇宇组织，讨论的核心是企业几十年沉淀下来的 legacy 数据怎么让 Agent 用起来。我听下来的感受是：**最显眼的问题是 NL2SQL，但最难的问题不是。** 让模型写出一条能跑的 SQL 已经不算难了；难的是让 Agent 知道这家企业到底有哪些数据、每个字段什么意思、哪些能用哪些不能用。catalog、元数据、语义层、数据质量——数据库社区做了几十年、一直觉得"不够性感"的活，突然成了 Agent 能不能落地的第一道门。另一场 panel **"Publish or Ship? The Research-to-Production Gap in Data Systems"** 从另一个角度戳了同一个地方：legacy 系统的改造从来不是论文问题，是工程问题，这道鸿沟在 Agent 时代只会更宽。

**GPU Database**

**另一件被提得很多的事，是 GPU 正在从 AI 专属走向传统数据负载。** ADMS 这个专做硬件加速的 workshop 开到第 17 届，前十几届基本是学术圈自己在玩 GPU join、GPU sort；今年主会场专门开了一场 panel，**"HW-SW Co-Design for Databases in the Age of AI-for-Systems"**，NVIDIA 的人坐在台上，旁边是 Google、Microsoft 和 TUM、BU 的人。背后是 NVIDIA 实打实的投入：cuDF 做 GPU 上的 DataFrame，cuVS 做 GPU 上的向量检索，和 Meta 一起把 Velox 做成 GPU-native，IBM 把 Presto 搬上多 GPU 集群报出最高 6 倍的性价比，Voltron Data 的 Theseus 干脆做了一个分布式 GPU 查询引擎。

这里面也包括 **Sirius**——我们在 UW-Madison 的好朋友于向遥教授的项目，一个 GPU-native 的 SQL 引擎：复用 DuckDB 的解析器和优化器，执行层用 cuDF 整个搬到 GPU 上，通过 Substrait 接入其他系统。TPC-H 1TB 上对 CPU 版 DuckDB 做到了 9 倍的性价比，还刷新了 ClickBench 的纪录。现在 SiriusDB 也和 NVIDIA 深度合作、全力推进这个项目，目标就一个：**把数据库的通用负载也搬到 GPU 上去。** 不是只加速某几个算子，是整个引擎。

今年 8 月 NVIDIA 把整个 RAPIDS 并进了 CUDA-X 品牌——意思很清楚：**数据处理不再是 CUDA 的外围应用，是平台本身的一部分。** 为什么是现在？企业手里的 GPU 已经多到训练之外有大量空档，AI pipeline 里数据准备早就是瓶颈，而当 Agent 把分析、向量检索和事务混进同一个负载，"一块硬件跑全部"就有了吸引力。对数据库人来说，一批老问题换了参数重新出现——数据搬运的代价、内存层次、算子设计——只是 PCIe 换成了 NVLink，DRAM 上面多了一层 HBM。

![VLDB 2026 Boston 主会场合影，左一为 David DeWitt](./images/vldb-2026-group-photo.jpeg)

**我的一些思考**

把这几天的笔记收拢一下，比起结论，我带回来更多的是三个问题。它们其实全都是数据库人擅长的领域，只是问题的背景变了。

**第一，Agent 的 Trace 和记忆是不是一种新的数据类型？** 今天的Agent除了用数据，本身也在产生数据。对话历史、工具调用的返回、中间推理的痕迹——今天大多被当成日志随手扔掉，或者粗暴塞进一个向量库。但它们有生命周期、有一致性要求、有访问模式、会被反复读；而且读它的不再是人写的程序，而是模型自己——突发、长尾、高度依赖上文。这就是一种需要被正经管理的数据，而现有的 cache 模型、admission control、QoS 划分，没有一个是为这种读法设计的。

**第二，Agent 时代的"正确性"到底是什么？** 数据库里"正确"是可以证明的——可串行化、快照隔离。Agent 系统里的"正确"是：返回的上下文足够支撑模型做出正确判断。这是一个统计意义上的、和下游任务绑定的定义，整个社区都还没想清楚怎么形式化。可串行化当年也不是天上掉下来的，是有人先把它写清楚了，后面几十年的系统才有了共同的标尺。这一轮也一样：**谁先定义，谁就占住了位置。**

**第三，成本和可观测性能不能成为一等公民？** 过去我们优化延迟和吞吐，现在多出来两个目标：token 成本和缓存命中。它们经常和延迟冲突——为了省 token 做的裁剪，可能要多花几次 LLM 调用——这是典型的多目标权衡，正是代价模型和优化器的活。更麻烦的是，Agent 负载下一个 bug 可能从不报错，只体现在账单上；执行过程不可回放，这件事就没法管。而当 Agent 真的大规模跑起来，决定它能不能商业化的恰恰是单位任务成本。

---

### 我们的工作：ContextPipe，用数据库人的手艺做 Agent Infra

9 月 4 日，最后一天，ADS Workshop，轮到我们上台。

![ContextPipe 报告现场：Motivation](./images/contextpipe-talk-motivation.jpg)


我们做的事，一句话就能说清：**把 Agent 的上下文组装，当成一次数据库查询来执行。**

Agent 每次调用模型之前，都要决定往 prompt 里塞什么、按什么顺序、什么时候把历史压缩掉——而这一切发生在一个硬性的上下文窗口预算和一个对字节敏感的 prompt cache 之下。今天大多数 harness 里，这段逻辑散落在 prompt builder、临时的压缩例程和各家 provider 的适配层里，没人说得清一次调用为什么花了那么多 token。

我们的观察是：**这件事和关系数据库执行一条查询，在结构上是同构的**——同样是硬预算、同样有分层缓存、同样靠统计信息做决策。所以我们把数据库人最熟的那套东西原样搬了过来：一个数据源 catalog、一个确定性的缓存感知优化器、一份 EXPLAIN ANALYZE 式的执行追踪。上下文因此变得可审计、可回放、可隔离故障。

ContextPipe 就是我们对这句话的实践：**用数据库人擅长的工程能力，去设计和打造 AI Agent 的基础设施。**

![ContextPipe 报告现场：Astra 与 Terminal-Bench 结果](./images/contextpipe-talk-astra-benchmark.jpg)

从Benchmark的结果上来看，在 SWE-bench Pro 的子集上，相比追加式的上下文策略，**ContextPipe 把总 token 用量降低 31%，LLM 调用次数降低 23%，响应时间降低 9%**——代价是 KV cache 命中率有所下降。而把这套思路做进产品之后，也就是我们最近基于ContextPipe的思想开源的 Astra， 在 Terminal-Bench 2.1上用同样的GLM5.2模型，对Deepseek Harness，PI和Hermes这样的开源Harness框架领先了 5-10 个百分点，Medium 档的领先尤其明显：**当任务的上下文开始变长、变杂，显式规划的收益就出来了。**


会议结束时，ContextPipe 拿到了 **ADS 2026 Oral Paper Award**。一个由数据库社区的人组成的评审群体，认可了"用数据库的思路去做 Agent 基础设施"这个方向是成立的，也显示了整个数据社区的人都在与时俱进，拥抱Agentic的golden era。


![ADS 2026 Oral Paper Award](./images/ads-2026-oral-paper-award.jpg)
*ADS 2026 Oral Paper Award。*
