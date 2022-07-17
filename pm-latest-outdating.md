---
title: pm-latest-outdating
tags: [latest, outdating, pm]
created: 2021-01-07T17:28:02.251Z
modified: 2021-01-07T17:28:28.482Z
---

# pm-latest-outdating

# outdating

- meteor
# discuss
- ## 放弃私有云？华为云回应一切__202006
- 与其说华为云放弃私有云，不如说华为云放弃私有云基础软件部分的纯私有化部署；
- 私有云对华为来说是低效的业务，放弃小市场，华为云瞄准的是更大的市场空间，
- 混合云是华为云的未来，也是目前云计算行业争夺的焦点，华为云终于理清了自己未来的路，或者说，华为内部统一了对云业务的意见。
- GaussDB 是华为基于开源数据库Postgresql研发而成，经过十几年的内核级别代码修改
  - 高斯数据库分为多个版本，GaussDB 100，主打 OLTP（Online Transaction Processing） 在线事务处理，对标 Oracle 及其他关系型数据库，落地于招商银行（掌上生活）。
  - GaussDB 200，主打 OLAP（Online Analytical Processing） 在线分析处理，对标 Teradata 及其他分布式数据库，落地于工商银行及浙江移动。
  - GaussDB 300，300产品在内部PK中落败，目前已停止研发，未来华为主打 100 和 200。后来GaussDB 100 被命名为 GaussDB T，GaussDB 200 被命名为 GaussDB A，目前这两款数据库都在华为官网能找到。

- 华为退出GaussDB数据库业务的原因：
  1、在当前形势下，华为战略重心需要收缩，重点肯定是鲲鹏。摊子太大，不聚焦就是死，因此内部的资源投入重心不会发散；
  2、无论是技术实力、竞争力和市场空间等维度，GaussDB都比不过华为公有云，最终被华为公有云淘汰。GuassDB数据库起步晚，尚未成熟，且数据库核心竞争力不足技术不多。
  3、数据库是银行的核心，核心系统的数据库替换会非常谨慎，在银行立样板点，需要很长的时间验证，华为等不起；
