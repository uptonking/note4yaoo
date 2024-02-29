---
title: lib-db-app-community-work-repeat
tags: [community, database]
created: 2023-10-27T06:53:39.428Z
modified: 2023-10-27T06:54:11.911Z
---

# lib-db-app-community-work-repeat

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-db-roadmap/future
- ## 

- ## 🔥 [The Future Database | Hacker News_202205](https://news.ycombinator.com/item?id=31481175)
- 
- 
- 

# discuss-regularly
- ## 

- ## 

- ## [我与 RisingWave 的 2023：成长，竞争，与商业化 - 知乎 _202312](https://zhuanlan.zhihu.com/p/674968361)
- 我于 2021 年年初创立了 RisingWave 这家流计算数据库公司。2023 年的临近尾声，也意味着 RisingWave 即将结束第三个年头，并踏入第四年的征程。
  - 三年到底有多长？瑞幸咖啡作为全球最快 IPO 的公司，从创立到上市使用了 17 个月；趣头条使用了 2 年 3 个月；拼多多使用了 2 年 10 个月。三年对于这些公司来说，足以从无到有，从有到上市。
  - 然而， 对于一家数据库公司来说，3 年只是算一个起步：Snowflake，这家史上市值最高的 SaaS 公司，于 2012 年 7 月成立，到 2015 年才推出了云上数仓（也就是今天大家熟知的产品）， 而在 2014 年获得了种子用户。
- 作为一个从零开始开发数据库的公司，RisingWave 的前两年几乎都是在系统开发中度过：我们对市场、销售的投入几乎为零，几乎所有公司资源都投向了工程与产品研发。
  - 而在即将过去的 2023 年，尽管我们保持了对市场、销售的较低投入，但我们在各个维度上都实现了快速增长，并逐步将公司带入可持续发展的轨道

- 从我过去三年的经验来看，对于一个较为早期的数据库项目来说，其从“让开发者了解”到“在企业落地”之间，有着巨大的鸿沟，而这一鸿沟几乎肯定需要人的介入才可能被弥补上。
  - RisingWave 的第一个企业级生产环境部署是在 2023 年年初（2022 年下半年开始沟通，历经将近半年时间）。
- 我们是如何向潜在用户推销 RisingWave 的呢？
  - 说来也很简单：我们不断说服 Apache Flink 的资深用户测试环境中使用 RisingWave 为 Flink SQL job 做测试与 debug。
  - 而这正是为什么我们在之后一段时间的宣传中会反复提及 Flink 的原因（注：RisingWave 从产品形态上与 Flink 有较大的差异化，因此与 Flink 做直接对比并非最恰当的宣传口径，我会在后面详细展开）。
- 我认为，RisingWave 如果想要实现超线性增长，那么很大程度上需要借助于开源的力量。
  - 我认为开源从本质上意味着更快赢得用户信任，并大幅降低用户尝试门槛。
  - 早期的传统 SaaS 产品都要求用户直接联系销售团队、进行电话沟通之后，才能试用产品。
  - 新兴的 SaaS 产品将“人”这个因素从试用流程中剔除，允许用户直接输入个人信息便能够免费注册、免费试用。
  - 数据库等企业级软件需要存储企业数据，而几乎所有企业都对数据安全敏感。因此，不少企业都对使用 SaaS 产品有严格的审批流程。即便企业愿意尝试使用新的 SaaS 产品，通常一开始都只愿意使用小规模测试数据来进行试错。
  - 开源允许企业用户在自己的环境中几乎无风险的部署、使用产品。用户无需顾虑自己的数据安全、无需与任何销售打交道
- RisingWave 目前正处在需要实现超线性增长的阶段。开源的重要性不言而喻。但这并不意味着开源是唯一。除了产品本身需要保持高质量之外，高质量的内容创作与真诚的用户沟通也是实现超线性增长的不可或缺的支柱。如果要问我作为 CEO，在 2023 年花费时间最多的事情是什么，那其实就是这两项。
- 关于 RisingWave 与 Flink 的性能讨论
  - RisingWave 自始至终的定位一直是流处理数据库，而非流计算引擎，因此从本质上来讲，与 Flink 有竞争，但并非纯粹替代关系。
  - RisingWave 使用的口号一直是“让流计算平民化”，也就是大幅降低流计算门槛
- 与阿里 Flink 团队的小伙伴关于性能对比的讨论完全是意料之外。
  - 公众在短期内可能对结果产生浓厚兴趣，但在长期来讲，没有人还记得结果，只记得了这两个产品进行过对比。
  - 因此，这场 RisingWave 与 Flink 关于性能的讨论的结局，从一开始就已经确定了，那就是强化了公众对两个产品关联度的印象。至于性能到底如何，只不过是一个短期的技术性讨论罢了。“All you need is attention”。这是一个云厂商高管在这事情发生之后对我说的话。
- 当企业考虑降本时，往往会暂停掉一切探索性业务，如探索更实时的计算、更新颖的设计等等。
- 不少朋友向我提出，RisingWave 是否会考虑蹭 AI 的热度。
  - 我是明确反对的。
  - RisingWave 是一家数据公司，不是一家 AI 公司。我们只会帮助 AI 公司实现数据实时化（例如在线特征工程等），但不会直接转型触碰 AI。
  - 首先，我一直坚持专业的人做专业的事。我是数据库专业的，对 AI 的理解仅仅是皮毛，无法真正理解 AI 用户的需求。
  - 其次，一家公司（尤其在早期阶段）开始做转型的时候，往往意味着他们对之前业务的否定。而我对 RisingWave 的前景充满信心，并认为业务上还有足够大的发展空间，没有必要通过 AI 的热度来寻找更多空间。尽管我的专业技能不足以支撑我直接入场 AI，但我还是会反复思考 AI 与 RisingWave 结合的可能性，在时机成熟时，作出改变。
- 构筑信任的最重要的因素之一便是时间。时间越久，信任感越长。而时间正是创业公司所缺失的。
  - 我认为所谓为人圆滑，指的是换位思考，站在对方的立场上从对方角度说话。
  - 与其一味从自己角度表达观点（“我要卖货我要卖货！”），不如多从他人角度考虑如何最大化利益（“我卖的货能够帮助别人解决什么问题？”）。
  - 当然了，这个世界是复杂的，我没有意图、也没有办法去说服所有人。但我还是希望能够独立思考，做真实的自己。

- 对于 RisingWave 的 2024 年，我并没有什么过多的想法。对于我来说，我所追寻的并不是什么星辰大海，而是仅仅期待脚踏实地将每一个生产案例做好做精，并按照既定路线实现商业化增长方面的目标。

- ## [Confluent收购Immerok：我的观点 - 知乎_202301](https://zhuanlan.zhihu.com/p/597220515)

- ## [重新思考流处理与流数据库 - 知乎](https://zhuanlan.zhihu.com/p/600701331)

- ## [RisingWave的2022年年终复盘与展望 - 知乎](https://zhuanlan.zhihu.com/p/593169897)

- ## [投资实时数据系统最前沿：走进Current 2022 - 知乎](https://zhuanlan.zhihu.com/p/574022136)

- ## ⏰ [Databases in 2022: A year in review | OtterTune](https://ottertune.com/blog/2022-databases-retrospective)

- ### 👥🔥 [Databases in 2022: A Year in Review | Hacker News_202301](https://news.ycombinator.com/item?id=34220524)
- There are a number of ideas in the database space that the industry is adopting across the board:
  - Separation of storage and compute (Neon, AlloyDB, Aurora). Every cloud database should built one. It's a big undertaking, but benefits are undeniable.
  - Good query processor for analytics (Snowflake, Velox, Singlestore)
  - Open source. Especially in OLTP open source == trust
  - HTAP. Can run mixed workload (Singlestore, Unistore): both OLTP (apps) and OLAP (reporting). This has always been a dream, but we still live in the world of dedicated systems: E.g. Snowflake and Postgres.
  - Shared nothing sharding (Vitess). This is the most controversial as you lose compatibility with the mothership (MySQL for Vitess). So it's unclear this will be the dominant architecture in the future. I think the world may get to "dynamic sharding" where storage stays separate and compute can be multinode and the user can easily and instantly change the number of nodes.

- ClickHouse has switchable IO engines: - read; - pread; - mmap; - pread_threadpool; 

- 
- 

- ## [投资数据库领域：2021年总结（NoSQL、图、时序） - 知乎](https://zhuanlan.zhihu.com/p/453556881)

- ## ⏰ [投资数据库领域：2021年总结（OLTP、OLAP、streaming） - 知乎](https://zhuanlan.zhihu.com/p/452628664)

- ## ⏰ [Databases in 2021: A year in review | OtterTune](https://ottertune.com/blog/2021-databases-retrospective)
- 
- 
- 

- 👥🔥 [Databases in 2021: A Year in Review | Hacker News_202112](https://news.ycombinator.com/item?id=29731885)
- 
- 

- ## ⏰ [Database Review 2021 | Hacker News_202211](https://news.ycombinator.com/item?id=33558509)
- 📝 [Database Review 2021 and 2022 Prediction_202202](https://www.bytebase.com/blog/database-review-2021/)

- 
- 
- 

- ## 🗳️ [Poll: What database does your company use? | Hacker News_201106](https://news.ycombinator.com/item?id=2684620)

> polled at 201106

- mysql      2432
- postgresql 1239
- sql-server 839
- mongo      683
- oracle     535
# discuss
- ## 

- ## 

- ## 

- ## 🎯🔥 [Building a Database in the 2020s (2022) | Hacker News_202304](https://news.ycombinator.com/item?id=35491682)
- 
- 
- 
- 

- ## 🎯🔥 [A database for 2022 | Hacker News_202204](https://news.ycombinator.com/item?id=30883015)
- 
- 
- 

- ## 🛢️🔥 [Recently minted(创造) database technologies that I find intriguing | Hacker News_202006](https://news.ycombinator.com/item?id=23531825)
- 
- 
- 
