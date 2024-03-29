---
title: pm-documentation-ssg-workspace
tags: [documentation, pm, pmgr, static-site-generator]
created: 2020-08-04T06:26:13.984Z
modified: 2021-05-14T14:33:13.599Z
---

# pm-documentation-ssg-workspace

# guide

- related products
  - docusaurus
# faq

## not-yet

- 根据包含中文的markdown文件名生成url时，因为浏览器显示到地址栏时会进行编码，所以url拷贝出来会变得特别长，此时在文章中引用很可能污染文档内容

## 是否该添加trailing slash

- https://github.com/slorber/trailing-slash-guide
- 不同解决方案提供商的实现不同，没有统一标准
- 选择能配置该选项的方案，尽量保证一致性
# features
- core/核心功能
  - 读取markdown内容生成DOM，然后渲染

- block style editor
- 对于包含数据(表格)的文档，实现类似cboard的数据联动
  - 文档block实现为展示块和控制块
  - 在控制块更新数据，所有展示块的内容都会更新

- 标题元数据提取
  - 时间、地点、人物
# draft
- sidenote
  - 显示在右边toc左侧的批注
# extensions
- static-site-generator
# discuss-stars
- ## [如何看待美团效仿亚马逊，内部汇报拒用 PPT 而改用 Word?](https://www.zhihu.com/question/340219070/answers/updated)
- 拒用PPT，就是减少形式主义，把更多的精力投入到工作本身
- 近日，PPT遭多家名企抵制
  - 字节跳动，不提倡用PPT进行工作汇报
  - 美团、微信，纷纷直接禁用PPT
# discuss
- ## 

- ## 

- ## I took a walk today to think about our docs site, ended up convinced that I needed to remove the site from our monorepo. 
- https://twitter.com/steveruizok/status/1711083978277466541
  - 合并还是不合并，需要尝试和实践
- The issue is that we need to make changes to the docs site (in production) without updating the site in a way that publishes unreleased changes.
  - Because the api json files are pulled from the packages in the monorepo, they default consume those new changes.
  - What this has meant in the past is either having a separate branch for the production version of the docs, which needs to be merged back to main whenever there are changes, or else not being able to update the prod version until we make a release.
- I've sort of got the inverse problem with the Redux docs sites. We've got 3 libs, 3 repos, 3 separate docs sites, w/ some overlap in content but mostly different

- ## [如何看待字节跳动的飞书（LARK）的前景？](https://www.zhihu.com/question/362435888/answers/updated)
- 看了下评论里大多都是在以自身作为c端用户的视角评价这几个tob产品，说实话连门都没摸到，看起来很尴尬

- 个人人为前景并不取决于产品，更多的取决于三个点：领导人、组织能力、对手犯错。
  - 产品影响前景的点在高手对决中占比并不高，因为产品很难拉开足够大的差距，但是领导人和组织能力以及对手给的机会足够能。
  - 对对手的充分了解是第三个了解才不会误判才能减少犯错。有利于找到比较好的节点，换道超车，而不是一味比拼人力和抄袭。
- 飞书有两个亮点可以圈可点：
  - 飞书文档和视频，目前最好用，没有之一；
  - OKR的产品和理念可以带动中小企业的管理模式升级。

- 大型企业这一块，就是和MSFT/GG直接竞争。
  - O365+Team/Gsuite也是日程/IM/VC/文档的组合。M家文档差一点，G家IM/VC差一点，不过都在狠追。
  - 另外M的Bot Framework / G的DialogFlow 都是在Bot方向的投资，并且已经有很大的生态系统和成熟的培训系统。
  - Lark如果要做这个高值大单，那就要靠卖企业文化/用户体验/更快速的产品更新和变通性/渠道。
- 另外一边的中小微企业，直接竞争的还是Slack。
  - Slack最成功的地方也是Bot/API/生态系统，和基本大型的软件都有链接。
  - 如果能把字节AI和视频的技术优势带进去那就是很独特的卖点。
- 第三块就是被很多这些企业忽视的前端劳力，没电脑，没账户，甚至临时工。
  - 体量巨大，单价/利润极低，拼的完全是手机端。
  - 对文档需求不高，最有用就是IM和自动化的Bot。

- 做toB不得不提华为。
  - 华为为了迁移对手的客户，宁可自己受点损失帮助客户迁移。
  - 字节如果在企业协同或者说tob这块有非常坚定的战略规划，那就要下功夫和成本去铺，
  - 明确自己的优势，不要局限在企业协同工具上，将规模做上去，这块不可能会是一家独大的局面，
  - 但是如果规模长期做不上去就会面临“来往”之类的结局。哪怕是在某些垂直领域里打开局面也是好的。
  - 尤其是对他的独特优势有强需求的垂直领域。
  - tob的产品竞争就是价值（解决方案、产品优势）+项目运作+客户关系。
  - 飞书应该在后两个上面加强投入，在标杆客户上不计成本的投入。在解决方案和产品优势上寻求突破点。

- 钉钉确实挺恐怖的。
  - 在阿里的同学都能明白，这个产品基本打通了阿里的一切业务，不管从工作流，信息流，业务流，都已经做到了跑得很远。
  - 你在阿里的时间越长你越会觉得他恐怖。
  - 但是这个问题的核心在于阿里是否能往上下游去走，让别的公司像阿里一样，把公司跑在钉钉上。
  - 1. 以自己的能力整合掉其他公司的人财物系统
  - 2. 以开放平台的方式整合掉人财物。
  - 如果第一个做成了，那阿里就又开辟了一个新的战场。（比如政务钉钉）
- 作为负责过pmo团队的人，我曾经相帮前司寻找一款能支持千人开发团队的工具，可以沉淀业务协同作战，调研过很多产品。
  - 最后没有选钉钉、企业微信和lark最大的问题在于业务本身和这几家均存在竞争关系，而核心数据使用第三方产品均无法保证安全。
  - 私有化部署是我们前几年就存在的需求。
  - 现在看到微信已经这么做了，最主要还是政府项目的安全需求。
- 但是，我觉得lark还是有机会的，毕竟钉钉的1500万客户里边，估计独角兽规模的公司不太多，
  - 大的公司比如美团，百度，京东，都在做自己的内部系统，其他1-10美金亿规模的，属于用别人的不放心，用自己的没能力，在中间上不来下不去，这部分需求其实并没有得到很好的满足。
- 蓝信只是早，和360的安全背景，论研发能力，三个蓝信也不如一个钉钉能打
  - 很多政府在用钉钉，不过是私有化部署的，数据归政府所有
- 我们先是老板带头用起钉钉，用习惯后感觉还不错。现在又全员转企业微信。
  - 目前的体验企业微信内部应用还没钉钉完善。但架不住客户都在微信啊。
  - 企业微信管理内部可能和钉钉没太多差别，但管理外部客户对钉钉就是降维打击了。
  - 之前客户的信息都在销售的个人微信上，现在企微出来，公司完全可实现将所有销售手里的客户微信导到企业微信了。
# docs-solutions-products
- [ShowDoc](https://www.showdoc.com.cn/)
  - 一个非常适合IT团队的API文档、技术文档工具
  - https://github.com/star7th/showdoc
    - 基于PHP实现
