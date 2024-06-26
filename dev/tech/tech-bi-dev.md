---
title: tech-bi-dev
tags: [bi]
created: 2024-05-28T12:37:59.504Z
modified: 2021-01-01T20:20:18.269Z
---

# tech-bi-dev

# guide

- ref
  - [精读《前端与BI》](https://zhuanlan.zhihu.com/p/82665657)
# discuss
- ## 

- ## 

- ## Code-first products present an unreasonably effective interface to AI models, because AIs excel at generating the very code these products run on.
- https://twitter.com/medriscoll/status/1760758205855224041
  - Today's release of Rill 0.41 introduces a related, powerful side effect of our BI-as-code philosophy:  You can now create an operational dashboard from any data source with just one click, thanks to an integration with GPT-3.5 Turbo.
  - 示例动画效果很好

- ## 一哥们分享通过 DSL 来生成特定领域 (BI) sql, 下面有人出来说这样的方式并没有解决底下 db 的问题
- https://twitter.com/Ehco1996/status/1752885599789629519
  - 最近我的想法改变了, 有些事情从根上就没法解决

- 这东西适合在公司里面自己做KPI，不适合对外吹嘘自己技术多强
- 我觉得做一层指标抽象的 DSL 还是挺有意义的，约束一下查询模式，可以做一些预计算啥的，有元信息做数据治理也方便。通过 DSL 生成 SQL 做可视化就看不懂图啥了

- 做业务的，考虑的是先跑起来，看市场反馈调整；从技术角度，考虑的是扩展性、稳定性这些，总之别让自己以后背锅难受。只能说都没错，最后调和一下就是不要over engineering , 但感觉原帖自嗨自捧的成分偏多。

- DSL/DAX之类的作用都是在SQL之上构建一个接近业务分析人员能理解的语义层。那么谁能比自然语言表达语义更适合用户呢？LLM

- bi系统的核心难点就是多表关联时，数据爆炸性增长导致查询效率低下。确实必须要解决底层db的瓶颈，否则这个系统就是前端花里胡哨，实际难用要死的垃圾系统。

- 的确没啥意义，为SQL做抽象的唯一原因就是db之间sql各有各的实现，这种抽象本质上就是牺牲每种db的独有特性，牺牲了独有特性也就牺牲了该db的优势，根本得不偿失，这也是以前很多orm框架面临的问题，通过定制也只能解决一部分问题，所以现在随着语言有动态能力，不少框架都可以直接sql操作了。

- ## [技术人员眼中的BI —— BI简介](https://zhuanlan.zhihu.com/p/234727408)
1. 数据可视化 （Data Visualization）
  - 所谓颜值即正义，数据可视化作为大家对BI的第一认知，肯定是一个非常重要的点。
  - 可视化图形丰富程度
  - 表格的支持（明细表、二维表，Pivot Table，条件样式等）
  - 拖拽式配置
  - 各种自定义（展示样式，日期数值格式化等）
  - 页面布局（dashboard layout）
  - 预制主题 （深色主题，浅色主题）
  - 颜色运用（颜色色系搭配，对色盲人群友好）
  - 自定义图形开发能力
  - Story Telling
2. 数据集成 （Data Integrations）
  - 有了可视化的皮，我们还要内部有货，还要有很多货。所以，BI还要看能对接多少数据源，并且对接的难度和灵活度。
  - 常见关系型数据库对接（是直连还是只能导入）
  - 常见文件格式的对接（CSV，Excel等）
  - Web Services对接 （泛指，包含SOAP和REST等）
  - 异构数据源融合
  - Public API支持自定义数据对接
  - JSON 等半结构化支持
  - SAP BW 等 MDX 类型支持
  - 大数据系统对接（Hive，Spark，Presto等）
3. 分析挖掘（Analytics）
  - 有了数据，有了可视化等原材料，我们需要有个米其林大厨来加工：
  - Filter，Sort等基本操作
  - 联动，下钻
  - 高级辅助计算：同环比计算，百分比
  - Grouping分组
  - Window Function等OLAP分析
  - 自定义函数
  - 运算速度
  - 预测分析
  - What If 分析
  - 高级Freeform分析（自定义SQL）
  - 因子挖掘，归因分析
4. 内容分发 (Distribution)
  - 有了内容和结果，我们要把好不容易做好的美食分发到企业内的每个人手中：
  - 移动端支持
  - 导出CSV/Excel等能力
  - 导出到 SFTP/网盘 等能力
  - 定时调度能力
  - 数据预警
  - 邮件订阅
5. 企业集成(Enterprise Integerations)
  - 数据有了价值，但是BI是企业中的良好市民，需要做很多企业相关集成：
  - 用户、用户组管理
  - 行列权限
  - LDAP等账号集成
  - 企业微信、钉钉等集成
  - 企业审计
  - 数据备份
6. 部署方式（Deployment）
  - 在决定部署前，还有一个比较重要的事项需要考虑：
  - 基于公有云
  - 私有化部署
  - 混合型
- 总结
  - BI系统涉及内容还是非常广的。

    - 曾经有人问我，BI系统的最核心内容是什么？我说不是可视化，不是数据处理，也不是数据对接，
    - 而是：如何把这么多复杂的点串到一起，而还能保证整体系统的一致体验。

  - 写文章的目标并不是让大家都能在公司中自研一套BI系统 （大多数时候，自研的代价远比采购一套观远BI高的多），

    - 而是软件研发的领域大多相互关联，很多BI中的思想可能也能用来解决各行各业中的实际问题，
    - （比如：前文中的用软件工程思想来组织SQL，比如：使用数据库或编译原理中的思想来做BI）
